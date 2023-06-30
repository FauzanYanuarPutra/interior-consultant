<template>
<div>
  <div class="flex justify-between items-center relative mt-5 p-5  w-full  z-20">
    <div class="">
      <div class="px-2 py-1 border-[1px] border-white text-white judul text-sm" v-show="!isOpen">THIS INTERIOR</div>
    </div>
    <div class=" md:hidden toggle-wrap  flex justify-end  z-20 " @click="toggleSidebar" :class="{ active: isOpen }">
      <span class="toggle-bar "></span>
    </div>
    <div class="md:flex hidden text-white">
      <a href="https://muhammadfauzan.netlify.app/" class="font-bold  md:mx-5 lg:mx-8 text-[18px] mont">
        <span class=" inline-block border-b-[2px] pb-1">Home</span>
      </a>
      <a href="https://muhammadfauzan.netlify.app/" class=" md:mx-5 lg:mx-8 text-[18px] mont">Collection</a>
      <a href="https://muhammadfauzan.netlify.app/" class=" md:mx-5 lg:mx-8 text-[18px] mont">About</a>
      <a href="https://muhammadfauzan.netlify.app/contact" class=" md:mx-5 lg:mx-8 text-[18px] mont">Contact</a>
    </div>
  </div>

  <div id="content" :class="{ 'slide-open': isOpen }" class="pt-[30px] mx-5 text-white md:flex md:mx-20  justify-between items-center z-20">
    <div class="md:w-[35%]  pr-4">
      <h1 class=" text-[36px] md:text-[48px] font-[500] lora ">Modern interior</h1>
      <p class="my-5 mont font-[400] ">A full-Service redential & commercial interior design and staging company offering professional organizing & echo-services.</p>
      <a href="https://muhammadfauzan.netlify.app/" class="font-bold mont flex items-center">Read more
        <svg class="ml-2 w-5" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg" fill="#000000">
          <g id="SVGRepo_bgCarrier" stroke-width="0"></g>
          <g id="SVGRepo_tracerCarrier" stroke-linecap="round" stroke-linejoin="round"></g>
          <g id="SVGRepo_iconCarrier">
            <title></title>
            <g id="Complete">
              <g id="arrow-right">
                <g>
                  <polyline data-name="Right" fill="none" id="Right-2" points="16.4 7 21.5 12 16.4 17" stroke="#ffffff" stroke-linecap="round" stroke-linejoin="round" stroke-width="2"></polyline>
                  <line fill="none" stroke="#ffffff" stroke-linecap="round" stroke-linejoin="round" stroke-width="2" x1="2.5" x2="19.2" y1="12" y2="12"></line>
                </g>
              </g>
            </g>
          </g>
        </svg>
      </a>
    </div>
    <div class=" flex justify-center md:justify-end">
      <div class="relative my-10 w-[391px] md:w-[400px] lg:w-[600px]  ">
        <img :src="'photo1.png'" alt="" class="w-full ">
        <div class="absolute bottom-[-60px] box-shadow right-1  sm:right-2 md:right-3 px-5 py-3 bg-[#181719]">
          <div class="flex">
            <div class="pr-5"><img :src="'photo2.png'" alt="" class="w-10 rounded-full "></div>
            <div>
              <h1 class="mont font-medium text-sm">Aliza Webber</h1>
              <p class="mont text-[12px] mt-[1px] text-[#828282]">Interior designer</p>
            </div>
          </div>
          <div class="my-5 w-[70%] font-bold lora text-[18px] lg:text-[24px]">
            Designed in 2020 by Aliza Webber
          </div>
        </div>
      </div>
    </div>
  </div>

  <h1 class="mt-[100px] py-10 flex justify-center text-white">Created By <a href="https://muhammadfauzan.netlify.app/" class="underline mx-2">Fauzan</a>- devChallenges.io</h1>

</div>
<transition name="slide" >
  <div v-if="isOpen" class="sidebar text-center text-white fixed  top-0 left-0 bottom-0 right-0 bg-[#181719] overflow-y-auto flex justify-center items-center">
    <div>
      <a href="https://muhammadfauzan.netlify.app/" class="block font-bold my-4 text-[18px]">
        <span class=" inline-block border-b-[2px] pb-1">Home</span>
      </a>
      <a href="https://muhammadfauzan.netlify.app/" class="block my-4 text-[18px] mont">Collection</a>
      <a href="https://muhammadfauzan.netlify.app/" class="block my-4 text-[18px] mont">About</a>
      <a href="https://muhammadfauzan.netlify.app/contact" class="block my-4 text-[18px] mont">Contact</a>
    </div>
  </div>
</transition>
</template>

<script>
import {
  ref,
  onMounted,
  onUnmounted
} from 'vue';
import {
  RouterLink,
  RouterView
} from 'vue-router';

export default {
  data() {
    return {
      isMati: true
    };
  },
  components: {
    RouterLink,
    RouterView,
  },
  setup() {
    const isOpen = ref(false);
    const isResized = ref(false);

    function disableScroll() {
      document.documentElement.style.overflow = 'hidden';
      document.body.style.overflow = 'hidden';
    }

    function enableScroll() {
      document.documentElement.style.overflow = 'auto';
      document.body.style.overflow = 'auto';
    }

    function handleResize() {
      const maxWidth = 768; // Define the maximum width
      const isSmallScreen = window.innerWidth <= maxWidth;

      if (!isResized.value) {
        isOpen.value = isSmallScreen;
        isResized.value = true;
      } else if (isOpen.value && !isSmallScreen) {
        isOpen.value = false;
        enableScroll();
      }
    }

    onMounted(() => {
      window.addEventListener('resize', handleResize);
      handleResize(); // Initial check
      isOpen.value = false; // Set isOpen to false initially
    });

    onUnmounted(() => {
      window.removeEventListener('resize', handleResize);
    });

    function toggleSidebar() {
      if (isOpen.value) {
        // Close the sidebar with animation before updating isOpen
        enableScroll();
        setTimeout(() => {
          isOpen.value = false;
        }, 500); // Adjust the duration to match the animation duration in CSS
      } else {
        isOpen.value = true;
        disableScroll();
      }
    }

    return {
      isOpen,
      toggleSidebar,
    };
  },
};
</script>

<style>
.judul {
  font-family: 'Crimson Pro',
    serif;
}

.mont {
  font-family: 'Montserrat',
    sans-serif;
}

.lora {
  font-family: 'Lora', serif;

}

.box-shadow {
  box-shadow: 0px 4px 4px 0px rgba(0, 0, 0, 0.25);

}

body {
  background-color: #181719;
}

.toggle-wrap {
  padding: 10px;
  position: relative;
  cursor: pointer;
  /* float: left; */
  right: 0;

  /* disable selection */
  -webkit-touch-callout: none;
  -webkit-user-select: none;
  -khtml-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
}

.toggle-bar,
.toggle-bar::before,
.toggle-bar::after,
.toggle-wrap.active .toggle-bar,
.toggle-wrap.active .toggle-bar::before,
.toggle-wrap.active .toggle-bar::after {
  transition: all 0.2s ease-in-out;
}

.toggle-bar {
  width: 34px;
  margin: 10px 0;
  position: relative;
  border-top: 4px solid white;
  display: block;
}

.toggle-bar::before,
.toggle-bar::after {
  content: "";
  display: block;
  background: white;
  height: 4px;
  width: 34px;
  position: absolute;
  top: -13px;
  transform: rotate(0deg);
  transform-origin: 13%;
}

.toggle-bar::after {
  top: 5px;
}

.slide-open #content {
  transform: translateX(250px);
  /* Adjust the value to match the sidebar width */
}

.toggle-wrap.active .toggle-bar {
  border-top: 6px solid transparent;
}

.toggle-wrap.active .toggle-bar::before {
  transform: rotate(45deg);
}

.toggle-wrap.active .toggle-bar::after {
  transform: rotate(-45deg);
}

.slide-enter-active {
  animation: slideIn 0.5s forwards;
}

.slide-leave-active {
  animation: slideOut 0.5s forwards;
}

@keyframes slideIn {
  0% {
    transform: translateX(100%);
  }

  100% {
    transform: translateX(0);
  }
}

@keyframes slideOut {
  0% {
    transform: translateX(0);
  }

  100% {
    transform: translateX(100%);
  }
}
</style>
