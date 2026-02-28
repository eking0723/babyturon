<script setup lang="ts">
import { useSeoMeta, useHead } from '@vueuse/head';
const title = "Baby Turon | Home";
const description = "Easier life!";
useSeoMeta({
 title: () => title,
 description: () => description,
 charset: "utf-8",
 viewport: "width=device-width, initial-scale=1.0"
});
useHead({
 link: [
 {rel: 'icon', type: 'image/png', href: '/logo.png'},
 {rel: 'stylesheet', href: '/reset.css'}
 ]
});</script>
template>
 <client-only>
<NavBar />
 <Welcome />
<Copyright />
 </client-only>
</template>