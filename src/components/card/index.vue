<template>
  <v-card class="d-flex flex-wrap justify-space-between">
    <v-hover>
      <template v-slot:default="{ hover }">
        <v-img
          class="d-none d-md-flex"
          :src="customer.image"
          style="margin-left: 1px"
        >
          <v-fade-transition>
            <v-overlay v-if="hover" color="#b2b9c4" absolute>
              <v-btn
                color="primary"
                class="mr-3 text-capitalize"
                large
                @click="$refs.file.click()"
                >edit</v-btn
              >
              <input
                v-show="false"
                type="file"
                id="file"
                ref="file"
                v-on:change="handleFileUpload()"
              />
              <v-btn color="primary" class="text-capitalize" large>view</v-btn>
            </v-overlay>
          </v-fade-transition>
        </v-img>
      </template>
    </v-hover>

    <div class="d-flex flex-no-wrap align-top px-md-2">
      <div class="py-md-2">
        <v-card-title class="font-md-weight-bold">
          {{ customer.name }}
        </v-card-title>

        <v-card-subtitle class="subtitle-1 text--secondary pb-0">
          @{{ customer.username }}
        </v-card-subtitle>

        <v-card-subtitle>
          <a>"{{ customer.company.catchPhrase }}"</a>
        </v-card-subtitle>
      </div>
      <v-hover class="ma-3 d-xs-flex d-md-none justify-end">
        <template v-slot:default="{ hover }">
          <v-avatar size="125" tile class="rounded">
            <v-img
              class="mx-auto"
              :src="customer.image"
              style="margin-left: 1px"
              rounded
            >
              <v-fade-transition>
                <v-overlay v-if="hover" color="#b2b9c4" absolute>
                  <v-btn
                    color="primary"
                    class="mr-3 text-capitalize"
                    large
                    @click="$refs.file.click()"
                    >edit</v-btn
                  >
                  <input
                    v-show="false"
                    type="file"
                    id="file"
                    ref="file"
                    v-on:change="handleFileUpload()"
                  />
                  <v-btn color="primary" class="text-capitalize" large
                    >view</v-btn
                  >
                </v-overlay>
              </v-fade-transition>
            </v-img>
          </v-avatar>
        </template>
      </v-hover>
    </div>
    <v-card-text class="pt-0 px-md-5">
      <div>
        <v-icon color="#015989" class="mr-3">mdi-email-outline</v-icon>
        <p class=" d-inline-block">
          {{ customer.email }}
        </p>
      </div>

      <div class="d-flex">
        <v-icon color="#015989" class="mr-3 d-inline"
          >mdi-map-marker-outline</v-icon
        >
        <p class=" d-inline-block addressText">{{ fullAddress }}</p>
      </div>

      <div>
        <v-icon color="#015989" class="mr-3">mdi-phone-outline</v-icon>
        <p class=" d-inline-block">{{ customer.phone }}</p>
      </div>

      <div>
        <v-icon color="#015989" class="mr-3">mdi-web</v-icon>
        <p class=" d-inline-block">{{ customer.website }}</p>
      </div>

      <div>
        <v-icon color="#015989" class="mr-3"
          >mdi-briefcase-variant-outline</v-icon
        >
        <p class=" d-inline-block">{{ customer.company.name }}</p>
      </div>

      <div class="d-flex">
        <v-icon color="#015989" class="mr-3 d-inline"
          >mdi-transmission-tower</v-icon
        >
        <p class=" d-inline-block">{{ customer.company.bs }}</p>
      </div>
    </v-card-text>
  </v-card>
</template>

<script>
export default {
  props: ["customerProp"],
  data: function () {
    return {
      customer: this.customerProp,
      overlay: false,
    };
  },
  methods: {
    // If want to upload
    //   handleFileUpload() {
    //     this.file = this.$refs.file.files[0];
    //   },
    //   submitFile() {
    //     let formData = new FormData();
    //     formData.append("file", this.file);
    //     this.$axios
    //       .post("../assets/images/", formData, {
    //         headers: {
    //           "Content-Type": "image/*",
    //         },
    //       })
    //       .then(function () {
    //         console.log("SUCCESS!!");
    //       })
    //       .catch(function () {
    //         console.log("FAILURE!!");
    //       });
    //   },
  },
  computed: {
    fullAddress: function () {
      return (
        this.customer.address.street +
        ", " +
        this.customer.address.suite +
        ",\n" +
        this.customer.address.city +
        ", " +
        this.customer.address.zipcode +
        ",\n" +
        this.customer.address.geo.lat +
        ", " +
        this.customer.address.geo.lng
      );
    },
  },
};
</script>
