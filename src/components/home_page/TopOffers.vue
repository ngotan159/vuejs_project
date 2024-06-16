<template>
  <div class="top-offers bg-grey-lighten-4 py-8">
    <v-container fluid class="pt-5">
      <v-row>
        <v-col cols="4" class="by-0 pr-6" style="height: 300px">
          <v-hover v-slot="{ isHovering, props }">
            <div
              class="parent"
              v-bind="props"
              style="overflow: hidden; height: 100%; border-radius: 7px"
            >
              <img
                src="@/assets/images/playstations.webp"
                :style="`width: 100%;height: 100%; cursor: pointer; transition: 0.7s all ease-in-out; scale: ${
                  isHovering ? 1.1 : 1
                }`"
                alt=""
              />
            </div>
          </v-hover>
        </v-col>
        <v-col cols="4" class="by-0 pr-6" style="height: 300px">
          <v-hover v-slot="{ isHovering, props }">
            <div
              class="parent"
              v-bind="props"
              style="overflow: hidden; height: 100%; border-radius: 7px"
            >
              <img
                src="@/assets/images/headset.webp"
                :style="`width: 100%;height: 100%; cursor: pointer; transition: 0.7s all ease-in-out; scale: ${
                  isHovering ? 1.1 : 1
                }`"
                alt=""
              />
            </div>
          </v-hover>
        </v-col>
        <v-col cols="4" class="by-0 pr-6" style="height: 300px">
          <v-hover v-slot="{ isHovering, props }">
            <div
              class="parent"
              v-bind="props"
              style="overflow: hidden; height: 100%; border-radius: 7px"
            >
              <img
                src="@/assets/images/chairs.webp"
                :style="`width: 100%;height: 100%; cursor: pointer; transition: 0.7s all ease-in-out; scale: ${
                  isHovering ? 1.1 : 1
                }`"
                alt=""
              />
            </div>
          </v-hover>
        </v-col>
      </v-row>
      <v-row class="mt-5">
        <v-col cols="6" class="mt-3 pl-2 py-0">
          <v-hover v-slot="{ isHovering, props }">
            <div
              class="parent"
              v-bind="props"
              style="overflow: hidden; height: 100%; border-radius: 7px"
            >
              <img
                src="@/assets/images/iphones.webp"
                :style="`width: 100%;height: 100%; cursor: pointer; transition: 0.7s all ease-in-out; scale: ${
                  isHovering ? 1.1 : 1
                }`"
                alt=""
              />
            </div>
          </v-hover>
        </v-col>
        <v-col cols="6" class="mt-3 pr-2 py-0">
          <v-hover v-slot="{ isHovering, props }">
            <div
              class="parent"
              v-bind="props"
              style="overflow: hidden; height: 100%; border-radius: 7px"
            >
              <img
                src="@/assets/images/laptops.webp"
                :style="`width: 100%;height: 100%; cursor: pointer; transition: 0.7s all ease-in-out; scale: ${
                  isHovering ? 1.1 : 1
                }`"
                alt=""
              />
            </div>
          </v-hover>
        </v-col>
      </v-row>
    </v-container>
  </div>
</template>
