<template>
  <Nav />
  <div class="card justify-content-center m-5 p-2 border-3 bg-gradient text-bg-dark" style="background-color: rgb(4, 20, 36);">
    <div class="row g-0">
      <div class="col-md-4">
        <img :src="avatar_url" v-if="avatar_url" alt="Profile picture" class="img-fluid rounded-start pb-3" style="width: 400px; height: 400px; object-fit: cover;">
        <button class="btn btn-primary m-2" @click="editToggleAvatar">Edit Avatar</button>
          <div v-if="inputUpdateAvatar">
            <input  @change="fileManager" type="file" />
            <button class="btn btn-primary btn-block mb-4" @click="uploadFile">Upload File</button>
          </div>
      </div>
      <div class="col-md-8">
        <div class="card-body">
          <h5 class="card-title mb-5">{{ username }}</h5>
          <h6 class="mb-4">Location: {{ location }}</h6>
          <h6 class="mb-4">Byography: {{ bio }}</h6>
          <h6 class="mb-4">Website: <a target="_blank" :href="website">{{ website }}</a></h6>
          <Profile @updateProfileEmit="hundleUpdateProfile" />
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { supabase } from "../supabase";
import { onMounted, ref, toRefs, watch } from "vue";
import { useUserStore } from "../stores/user";
import Nav from "../components/Nav.vue";
import Profile from "../components/Profile.vue";
import Swal from 'sweetalert2';

const userStore = useUserStore();
const username = ref(null);
const website = ref(null);
const location = ref(null);
const bio = ref(null);
const file = ref();
const fileUrl = ref();
const inputUpdateAvatar = ref(false);
const avatar_url = ref(null);


const editToggleAvatar = () => {
  inputUpdateAvatar.value = !inputUpdateAvatar.value;
};

const fileManager = (event) => {
  file.value = event.target.files[0];
  console.log(event);
  console.log(file.value);
};

const hundleUpdateProfile = (updatedProfileData) => {
  username.value = updatedProfileData.full_name;
  website.value = updatedProfileData.website;
  location.value = updatedProfileData.location;
  bio.value = updatedProfileData.bio;
  avatar_url.value = updatedProfileData.avatar_url;
};

const uploadFile = async () => {
  if (!file.value) {
    console.log("aqui llego");
    return;
  }
  const { data } = await supabase
        .from('profiles')
        .select("avatar_url")
        .eq("user_id", supabase.auth.user().id);

  const deleteUrl = data[0].avatar_url;
  // console.log(deleteUrl);
  const { error: urlDeleteError } = await supabase.storage
    .from("profile-img")
    .remove([deleteUrl]);

  if (urlDeleteError) {
    console.error("Error deleting file:", urlDeleteError);
    return;
  }
  console.log("File succesfully upload.");

  const timestamp = Date.now();
  const filePath = `profiles/${timestamp}-${file.value.name}`;
  const { error: uploadError } = await supabase.storage
    .from("profile-img")
    .upload(filePath, file.value);
  if (uploadError) {
    console.error("Error uploading file:", uploadError);
    return;
  }
  console.log("File succesfully upload.");

  const { data: urlData, error: urlError } = await supabase.storage
    .from("profile-img")
    .getPublicUrl(filePath);
  console.log(urlData);
  if (urlError) {
    console.error("Error getting public URL:", urlError);
    return;
  }

  fileUrl.value = urlData.publicURL;
  console.log(fileUrl.value);

  const { error: updateError } = await supabase
    .from("profiles")
    .update({ avatar_url: fileUrl.value })
    .eq("user_id", supabase.auth.user().id);

  if (updateError) {
    console.error("Error updating profile:", updateError);
    return;
  }
  console.log("Profile successfully updated.");
  Swal.fire({
        icon: 'success',
        title: 'Success', 
        showConfirmButton: false,
        timer: 1000
    })
  await userStore.fetchUser();
  editToggleAvatar();
};

async function getProfile() {
  await userStore.fetchUser();
  username.value = userStore.profile.full_name;
  website.value = userStore.profile.website;
  location.value = userStore.profile.location;
  bio.value = userStore.profile.bio;
  avatar_url.value = userStore.profile.avatar_url;
}

watch(
  () => userStore.profile,
  (updatedProfileData) => {
    avatar_url.value = updatedProfileData.avatar_url;
  },
  { deep: true }
);

onMounted(() => {
  getProfile();
});

</script>

<style></style>
