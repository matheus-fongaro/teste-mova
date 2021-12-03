<template>
  <v-row>
    <v-col v-for="n in 3" :key="n" class="d-flex child-flex" cols="12" md="4">
      <v-img src="https://picsum.photos/316/181" lazy-src="https://picsum.photos/7/4">
        <template #placeholder>
          <v-row
            class="fill-height ma-0"
            align="center"
            justify="center"
          >
            <v-progress-circular
              indeterminate
              color="grey lighten-5"
            />
          </v-row>
        </template>
      </v-img>
    </v-col>
  </v-row>
</template>
