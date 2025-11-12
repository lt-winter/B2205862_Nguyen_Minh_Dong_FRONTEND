<template>
  <div v-if="contact" class="page">
    <h4>Thêm Liên hệ</h4>
    <ContactForm :contact="contact" @submit:contact="addContact" />

    <div class="d-flex gap-3 mt-4 align-items-center justify-content-center">
      <div v-if="message" class="alert alert-success" role="alert">
        <p class="text-success m-0 fw-bold">{{ message }}</p>
      </div>

      <router-link :to="{ name: 'contactbook' }">
        <span v-if="message" class="badge text-bg-primary">
          Trở về trang chủ
        </span>
      </router-link>
    </div>
  </div>
</template>

<script>
import ContactForm from "../components/ContactForm.vue";
import ContactService from "../services/contact.service";

export default {
  components: {
    ContactForm,
  },
  data() {
    return {
      contact: {},
      message: "",
    };
  },
  methods: {
    async addContact(data) {
      try {
        await ContactService.create(data);
        this.$router.push({ name: "contactbook" });
      } catch (error) {
        console.log(error);
      }
    },
  },
  created() {},
};
</script>
