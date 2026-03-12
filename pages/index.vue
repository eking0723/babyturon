<script lang="ts"></script>
<template>
 <client-only>
 <NavBar />
 <div id="btMain" class="bt-main"></div>
 <Cookies />
 <Copyright />
 </client-only>
</template>
<script setup lang="ts">
import { useSeoMeta, useHead } from '@vueuse/head';
const title = "Baby Turon | Home";
const description = "A media platform for digital artists.";
useSeoMeta({
 title: () => title,
 description: () => description,
 charset: "utf-8",
 viewport: "width=device-width, initial-scale=1.0"
});

useHead({
 link: [
 {rel: 'icon', type: 'image/png', href: '/logo.png'},
 {rel: 'stylesheet', href: '/reset.css'},
 {rel: 'stylesheet', href: '/custom.css'} ,
 {rel: 'preconnect', href: 'https://fonts.googleapis.com'},
 {rel: 'preconnect', href: 'https://fonts.gstatic.com', crossorigin: ''},
 {rel: 'stylesheet', href: 'https://fonts.googleapis.com/css2?family=Fira+Sans:ital,wght@0,100;0,200;0,300;0,400;0,500;0,600;0,700;0,800;0,900;1,100;1,200;1,300;1,400;1,500;1,600;1,700;1,800;1,900&family=Geom:ital,wght@0,300..900;1,300..900&display=swap'}
 ]});

 const globalDelay = 500;
const allowCookies = useCookie<boolean>("allowCookies", {
 sameSite: "none",
 secure: true,
 maxAge: 60 * 60 * 24,
});
allowCookies.value = allowCookies.value || false;
async function loadModal() {
 const cookieModal = document.getElementById("btCookieModal") as HTMLDivElement;
 const cookieBox = document.getElementById("btCookieBox") as HTMLDivElement;
 const cookieX = document.getElementById("btCookieX") as HTMLDivElement;
 const cookieOK = document.getElementById("btCookieOK") as HTMLDivElement;
 if ( !cookieModal || !cookieBox || !cookieX || !cookieOK ) return;
 if (allowCookies.value === true) {
 allowAllCookies();
 return;
 }
 showCookiePopup();
  cookieX.addEventListener("click", (e) => {
 showCookiePopup(false);
 });
 cookieOK.addEventListener("click", (e) => {
 allowAllCookies();
 });
}
async function showCookiePopup(show: boolean = true) {
 const cookieBox = document.getElementById("btCookieBox") as HTMLDivElement;
 const cookieModal = document.getElementById("btCookieModal") as HTMLDivElement;
 if (!cookieBox || !cookieModal) {
 setTimeout(showCookiePopup, 50);
 return;
 }
 if (!show) {
 cookieBox.classList.add("bt-hidden");
 cookieModal.classList.add("bt-hidden");
 return;
 }

 cookieBox.classList.remove("bt-hidden");
 cookieModal.classList.remove("bt-hidden");
}
let lastCookieClicked = 0;
async function allowAllCookies() {
 if (lastCookieClicked >= Date.now() - globalDelay) return;
 lastCookieClicked = Date.now();
 allowCookies.value = true;
 showCookiePopup(false);
}
onMounted(() => {
 setTimeout(() => {
 loadModal();
 }, 1);
});
 </script>

<style scoped></style>

<style></style>