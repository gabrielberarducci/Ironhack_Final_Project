<template>
  <Nav />
  <div>
    <h3>Name: {{ username }}</h3>
    <h3>Website: <a target="_blank" :href="website">{{ website }}</a></h3>
    <h3>Location: {{ location }}</h3>
    <h3>Byography: {{ bio }}</h3>
  </div>
  <div>
    <img :src="avatar_url" v-if="avatar_url" alt="Profile picture" />
  </div>
  <div>
    <input  @change="fileManager" type="file" />
    <button class="btn btn-primary btn-block mb-4" @click="uploadFile">Upload File</button>
  </div>
  <Profile @updateProfileEmit="hundleUpdateProfile" />
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
    // username.value = updatedProfileData.full_name;
    // website.value = updatedProfileData.website;
    // location.value = updatedProfileData.location;
    // bio.value = updatedProfileData.bio;
    avatar_url.value = updatedProfileData.avatar_url;
  },
  { deep: true }
);

onMounted(() => {
  getProfile();
});
</script>

<style>
img {
  width: 200px;
  border-radius: 100%;
}
</style>
