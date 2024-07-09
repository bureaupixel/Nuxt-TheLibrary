<script setup  lang="ts">
import { onMounted } from 'vue'
import { Drawer } from 'flowbite'
import Menu from 'vue-material-design-icons/Menu.vue';

/* The on mounted section makes the drawer show and hide */
onMounted(() => {
   // set the drawer menu element
    const $targetEl = document.getElementById('drawer-swipe');
    const $drawerHideButton = document.getElementById('drawer-hide-button');
    const $drawerShowButton = document.getElementById('drawer-show-button');
    // options with default values
    const options = {
        placement: 'right',
        backdrop: true,
        bodyScrolling: true,
        edge: false,
        edgeOffset: '',
        backdropClasses: 'bg-zinc-100 dark:bg-zinc-900 bg-opacity-90 dark:bg-opacity-80 fixed inset-0 z-30',
        onHide: () => { /* console.log('drawer is hidden'); */ },
        onShow: () => { /* console.log('drawer is shown');*/  },
        onToggle: () => { /* console.log('drawer has been toggled');*/  }
    };
    if ($targetEl) {
        /*
        * targetEl: required
        * options: optional
        */
        const drawer = new Drawer($targetEl, options);
        // show the drawer
        drawer.hide();
        $drawerHideButton.addEventListener('click', () => {drawer.hide();})
        $drawerShowButton.addEventListener('click', () => {drawer.show();})
    }
});
</script>

<template>
<!-- drawer init and toggle -->
<div class="flex">
    <div class="flex-auto w-1 pt-3">
    </div>
    <!-- button to hide the drawer -->
    <div class="flex-row  pt-5 pr-5 justify-end">
        <button id="drawer-show-button" type="button" aria-controls="drawer-swipe"  >
            <Menu :size="25"/>
    </button>
    </div>
</div> 
<!-- the drawer itself-->
<div class="max-w-4xl mx-auto">
    <div id="drawer-swipe" class="fixed z-40 h-screen p-4 overflow-y-auto" tabindex="-1" aria-labelledby="drawer-label">
        <!-- Main  button to toggle the drawer -->
        <button id="drawer-hide-button" type="button" aria-controls="drawer-swipe" class="text-gray-400 bg-transparent hover:bg-gray-200 hover:text-gray-900 rounded-lg text-sm p-1.5 absolute top-2.5 right-2.5 inline-flex items-center dark:hover:bg-gray-600 dark:hover:text-white" >
            <svg aria-hidden="true" class="w-5 h-5" fill="currentColor" viewBox="0 0 20 20" xmlns="http://www.w3.org/2000/svg"><path fill-rule="evenodd" d="M4.293 4.293a1 1 0 011.414 0L10 8.586l4.293-4.293a1 1 0 111.414 1.414L11.414 10l4.293 4.293a1 1 0 01-1.414 1.414L10 11.414l-4.293 4.293a1 1 0 01-1.414-1.414L8.586 10 4.293 5.707a1 1 0 010-1.414z" clip-rule="evenodd"></path></svg>
            <span class="sr-only">Close menu</span>
        </button>
        <!-- Title on top of the drawer -->
        <div class="mt-2 mb-5">
            <TitleBlock />
            <Navigation />
        </div>

        <div class="mt-5 mb-5"><Footer /></div>


    </div>
</div>
</template>

<style>
/* color settings for the background of the dark switch section */
#drawer-swipe { background-color: rgba(255, 255, 255, 0.98); width: 50vw;}
.dark-mode #drawer-swipe { background-color:rgba(22, 23, 21, 0.95)}
/* color settings for the rulers of the drawer section */
hr{border-color: #D1D1D1;}
.dark-mode hr{ border-color: aliceblue;}
</style>