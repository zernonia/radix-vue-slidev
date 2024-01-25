---
theme: apple-basic
background: https://source.unsplash.com/collection/94734566/1920x1080
class: text-center
highlighter: shikiji
lineNumbers: false
info: |
  ## Slidev Starter Template
  Presentation slides for developers.

  Learn more at [Sli.dev](https://sli.dev)
drawings:
  persist: false
transition: slide-left
title: Building Component with Primitives
mdc: true
---

---
layout: intro-image-right
image: /radix-vue.png
---

<h1 class="!text-5xl">Building Component with Primitives
</h1>

using Radix Vue

<!-- Unstyled, accessible components for building high‑quality design systems and web apps in Vue. -->

<div class="pt-12">
  <span @click="$slidev.nav.next" class="px-2 py-1 rounded cursor-pointer" hover="bg-white bg-opacity-10">
    By Zernonia
     <!-- <carbon:arrow-right class="inline"/> -->
  </span>
</div>
 

<!--
The last comment block of each slide will be treated as slide notes. It will be visible and editable in Presenter Mode along with the slide. [Read more in the docs](https://sli.dev/guide/syntax.html#notes)
-->

--- 
layout: section
---

# I'm Zernonia

- From Malaysia 🇲🇾
- Frontend Lead at [Troop Travel Inc](https://trooptravel.com/).
- Core maintainer of [Radix Vue](https://radix-vue.com/), [Shadcn Vue](https://www.shadcn-vue.com/)


<div class="flex space-x-2 mt-12 mb-2">
<mdi-github class="w-6 h-6" /> 
<mdi-twitter class="w-6 h-6" /> 
</div>
<a href="https://zernonia.com">@ zernonia</a>


<img src="https://pbs.twimg.com/profile_images/1476010084295716864/xfN1G89G_400x400.jpg" class="absolute rounded-full w-[250px] h-[250px] border border-3 top-[10rem] right-[6rem]">

<!-- Without futher ado, let's build a component -->

---
layout: statement
---

# Let's build a component!


--- 
layout: two-cols
---


# Real world design

<div class="relative mr-8">
  <img src="/design-1.png" class="rounded shadow" />
  <img v-click src="/design-2.png" class="absolute top-0 left-0 rounded shadow" />
</div>


::right::
# <br>

<div v-click>

### User stories

1. Open a popover when button was clicked.
2. User can navigate to profile page.
3. User can search by organization name.
4. User can select the organization.
5. Close popover when click outside or "Escape" key pressed.
6. User can logout with log out button.
 
</div>

<img src="https://d6ce0no7ktiq.cloudfront.net/images/stickers/482.png" class="rounded shadow mt-24 absolute top-0" v-click />
--- 

# Action plan!

<v-clicks>

1. Find `Popover` component in UI library you are using.
2. Find searchable `Listbox` in UI library you are using.
3. Style the component as the design.
 
</v-clicks>

<div v-click class="mt-24">

## Then found out  

<div class="text-red-400 mt-4"> why there's no such component?! </div>
<div class="text-red-400"> why I can't position the popover at the bottom-right?! </div>
<div class="text-red-400"> why I can't extend the `Select` component?!</div>
<div class="text-red-400"> how can I overwrite the styling of this component?!</div>


</div>
 
<div v-click class="absolute text-center top-24 right-24 w-[300px]">
  <img src="https://media1.tenor.com/m/HRtvl-pDzU0AAAAC/ok-bye.gif"> 
  <h2 class="mt-1">I will build from scratch! 😤</h2>
</div>

<!-- - there's always design that component library can't achieve
- ahh why you (component) won't work!!!!
- some native element can't be style
- building a11y component is tough
- why reinvent the wheel? -->

 
--- 
layout: statement
---

# [Demo](https://stackblitz.com/edit/vitejs-vite-zrdcrq?embed=1&file=src%2Fcomponents%2FUserMenu.vue)


---
layout: two-cols
---

# Popover 


```ts
const triggerEl = ref();
const contentEl = ref();
const isOpen = ref(true);

onClickOutside(contentEl, (ev) => {
  if (triggerEl.value.contains(ev.target)) return;
  isOpen.value = false;
});
onKeyStroke('Escape', (e) => {
  e.preventDefault();
  isOpen.value = false;
});
```


```html
<div
  ref="contentEl"
  v-if="isOpen"
  class="absolute left-[105%] bottom-4"
>
  <!--  -->
</div>
```

::right::


<v-clicks>

## Gotcha

<ul>
<li class="text-red-400 mt-4"> If add a dialog component, escape key would close the popover immaturely. </li>
<li class="text-red-400"> The content doesn't auto position in smaller viewport. </li>
<li class="text-red-400"> Accessibility (tab focus, trap focus)</li>
</ul>
</v-clicks>


---
layout: two-cols
---

# Listbox 

 

```html 
<input 
  type="search" 
  v-model="searchTerm"
  placeholder="Search an organization"
/> 
 
<button
  v-for="i in list"
  :key="i"
  @click="selectedItem = i"
>
  <span><!--  --></span>
  <span v-if="selectedItem === i">✔</span>
</button>
 
```

::right::


<v-clicks>

## Gotcha

<ul>
  <li class="text-red-400"> Accessibility (arrow navigation on input, <kbd>Home</kbd>, <kbd>End</kbd>)</li>
</ul>
</v-clicks>


---
layout: statement
---

# What do we do?

<v-clicks>

# Introducing <span class="text-[#13b981]">Radix Vue</span>

</v-clicks>

---

# What is Radix Vue?
<br>

## Unstyled, accessible <span class="text-[#13b981]">primitive</span> components for building <br> high‑quality web app with Vue.
<br>


<v-clicks>

- 💚 Vue, Nuxt supported.
- 🚀 Save time. Ship faster.
- ⌨️ Accessibility out of the box.
- 🧑🏻‍💻 Developer Experience First.
- 🧩 Compatible with other UI Library

</v-clicks>




<!-- 
1. Build for Vue framework, which compatible with any meta framework build on top of Vue.
2. Building on top Radix components will save you time and money, so you can ship a better product faster.
3. WAI-ARIA compliant. Support Keyboard navigation & Focus management.
4. Unstyled, easily customizable and great for building design system and web apps.
 -->

--- 


# Let's swap with Radix Vue


1. Using [Popover](https://www.radix-vue.com/components/popover.html)
2. Using [Combobox](https://www.radix-vue.com/components/combobox.html)  


<div v-click class="flex py-12 text-7xl items-center justify-center">

[Demo](https://stackblitz.com/edit/vitejs-vite-nyjzmt?file=package.json,src%2Fcomponents%2FUserMenu.vue)
</div>

---
layout: two-cols
---

```vue {all|2|12-17|all}
<script setup lang="ts">
import { Popover } from 'radix-vue/namespaced'
</script>

<template>
  <Popover.Root>
    <Popover.Trigger>
      <!-- button -->
    </Popover.Trigger>

    <Popover.Portal>
      <Popover.Content 
        :side="'right'"
        :side-offset="10"
        :align="'end'"
        :align-offset="14"
        prioritize-position
      >
        <!-- content -->
      </Popover.Content>
    </Popover.Portal>
  </Popover.Root>
</template>
```

::right::

<v-clicks>

```vue {all|2|9-13|17-20|all}
<script setup lang="ts">
import { Combobox } from 'radix-vue/namespaced'

const searchTerm = ref('');
const selectedOrganization = ref();
</script>

<template>
  <Combobox.Root 
    v-model="selectedOrganization"
    v-model:searchTerm="searchTerm"
    :open="true"  
    :display-value="() => ''"
  >
    <Combobox.Input />
    <Combobox.Content>
      <Combobox.Item 
        v-for="i in list"
        :key="i"
        :value="i"
      >
        <!-- item -->
        <Combobox.ItemIndicator />
      </Combobox.Item>
    </Combobox.Content> 
  </Combobox.Root>
</template>
```

</v-clicks>

---
layout: statement
---

<img class="mx-auto" src="https://media0.giphy.com/media/l0HlL0dRSoUMP6U8M/giphy.gif?cid=ecf05e47plca201sas880cxplnq0vncviijcmuziuzu67oht&ep=v1_gifs_search&rid=giphy.gif&ct=g">


<!-- So, stop reinvent the wheel, be smart and use Radix Vue -->

---
layout: statement
---


## Ship a complete component now!
# With Radix Vue

<!-- ![Meme](/meme.jpeg) -->

---

# Library around Radix Vue

<br>

## UI Library

<div class="grid grid-cols-3 gap-8 h-36">

<img class="h-full object-cover" src="https://www.shadcn-vue.com/og.png">
<img class="h-full object-cover" src="https://ph-files.imgix.net/56069229-222e-4364-88c6-8c5d4aa0c3e5.png?auto=compress&codec=mozjpeg&cs=strip&auto=format&fit=max&dpr=1">
</div>

<br>

## Starter

<div class="grid grid-cols-3 gap-8 h-36">

<img class="h-full object-cover"  src="https://ui-thing.behonbaker.com/cover.png">
<img class="h-full object-cover"  src="https://supastarter-website-5kzz29gil-sedecon-solutions.vercel.app/images/meta.png">

</div>




---
layout: statement
class: text-center
---

# ⭐️ GitHub / Radix Vue

[Docs](https://radix-vue.com) · [GitHub](https://github.com/radix-vue/radix-vue) · [Discord](https://chat.radix-vue.com)
