<template>
    <div class="page">
      <h4>Thêm Liên hệ</h4>
      <ContactForm
        :contact="contact"
        @submit:contact="addContact"
        :showFavorite="true"
      />
      <p>{{ message }}</p>
    </div>
</template>
  
<script>
import ContactForm from "@/components/ContactForm.vue";
import ContactService from "@/services/contact.service";

export default {
    components: {
        ContactForm,
    },
    data() {
        return {
            contact: {
                name: "",
                email: "",
                address: "",
                phone: "",
                favorite: false,
            },
            message: "",
        };
    },
    methods: {
        async addContact(data) {
            try {
                await ContactService.create(data); // Thay thế bằng create(data) để thêm liên hệ mới
                this.message = "Liên hệ đã được thêm thành công.";
                // Reset form
                this.contact = {
                    name: "",
                    email: "",
                    address: "",
                    phone: "",
                    favorite: false,
                };
            } catch (error) {
                console.error("Error adding contact:", error);
                this.message = "Đã xảy ra lỗi khi thêm liên hệ.";
            }
        },
    },
};
</script>
  
<style scoped>
/* CSS cho trang ContactAdd.vue */
.page {
    max-width: 600px;
    margin: 0 auto;
    padding: 20px;
}
</style>
