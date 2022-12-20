<template>
  <v-container>
    <div class="center border">
      <h3>Image Background Remover</h3>
    </div>
    <hr>

  <v-row class="mt-3">
    <v-col lg="5" md="5" sm="12">
    <div class="h center">
      <div class="input-img">
        <div>
          <img :src="imagePreview" class="uploading-image" />
        </div>
        <div class="drop">
        <input type="file" accept="image/*" @change="previewImage" />
        <v-btn plain color="primary">Upload/Drop</v-btn>
      </div>
      </div>
      </div>
      </v-col>
      <v-col>
        <div class=" h center mg">
          <v-btn @click="convertnew()">Convert 🔁</v-btn>
        </div>
      </v-col>
      <v-col lg="5" md="5" sm="12">
        <div class="h center">
          <div class="input-img">
        <div>
          <img
            :src="'data:image/png;base64,' + users"
            class="uploading-image"
          />
        </div>
        <div class="mt-10 center">
        <v-btn plain color="primary"><a download :href="'data:image/png;base64,' + users">
          download</a></v-btn>
        </div>
      </div>
      </div>
      </v-col>
  </v-row>
  </v-container>
</template>

<script>
// import BgRemove from './BgRemove.vue';
export default {
  name: "image-upload-preview",
  data() {
    return {
      image: "",
      imagePreview: "",
      rempreview: "",
    };
  },
  computed: {
    users() {
      return this.$store.state.imgdata;
    },
  },
  methods: {
    previewImage(event) {
      var input = event.target;
      if (input.files && input.files[0]) {
        var reader = new FileReader();
        reader.onload = (e) => {
          this.imagePreview = e.target.result;
        };
        reader.readAsDataURL(input.files[0]);
      }
    },

    convertnew() {
      this.$store.dispatch("convert", this.imagePreview);
    },
    async selectImage(e) {
      const file = e;
      if (!file) return;
      const readData = (f) =>
        new Promise((resolve) => {
          const reader = new FileReader();
          reader.onloadend = () => resolve(reader.result);
          reader.readAsDataURL(f);
        });

      const data = await readData(file);

      this.imagePreview = data;
    },
    async clearImagePreview() {
      this.imagePreview = "";
    },
  },
};
</script>

<style>
.file-input {
  width: 300px;
  margin: 0 auto;
  margin-top: 40px;
}
input[type="file"] {
  width: 350px;
  height: 100px;
  position: absolute;
  opacity: 0;
}
.drop {
  display: flex;
  justify-content: center;
  align-items: center;
  width: 350px;
  height: 100px;
}
.uploading-image {
  height: 350px;
  width: 350px;
  border:none;
  box-shadow: -2px 4px 13px 4px rgba(231,250,255,0.2);
}
.img-area {
  display: flex;
  flex-direction: row;
  justify-content: space-around;
}
a{
  text-decoration: none;
}
.input-img {
  display: flex;
  flex-direction: column;
  gap: 50px;
}
.h {
  height: fit-content;
}
.center {
  display: flex;
  justify-content: center;
  align-items: center;
}
.mg {
  margin: auto auto;
  width: fit-content;
}
.imageh {
  height: 500px;
}
.txt{
  color: white;
font-weight: bold;
}
</style>
