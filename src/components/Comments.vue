<template>
  <v-form ref="form" v-model="valid" lazy-validation>
    <v-text-field
      v-model="name"
      :counter="20"
      :rules="nameRules"
      color="#435b71"
      placeholder="name"
      prepend-inner-icon="mdi-account-settings-outline"
      filled
      required
    ></v-text-field>

    <v-text-field
      v-model="email"
      :rules="emailRules"
      color="#435b71"
      placeholder="email"
      prepend-inner-icon="mdi-at"
      filled
      required
    ></v-text-field>

    <v-select
      v-model="select"
      :items="items"
      :rules="[(v) => !!v || 'Item is required']"
      color="#435b71"
      placeholder="choose reason"
      prepend-inner-icon="mdi-bullhorn-outline"
      filled
      required
    ></v-select>

    <v-textarea
      v-model="meessage"
      :rules="[(v) => !!v || 'Item is required']"
      color="#435b71"
      filled
      rows="4"
      placeholder="type comment..."
    ></v-textarea>
    <v-row>
      <v-col cols="12" md="4">
        <v-btn
          :disabled="!valid"
          color="success"
          class="mr-4"
          @click="validate"
          block
        >
          Send
        </v-btn>
      </v-col>
      <v-col cols="12" md="4">
        <v-btn color="error" class="mr-4" @click="reset" block>
          Reset Form
        </v-btn>
      </v-col>
      <v-col cols="12" md="4">
        <v-btn color="warning" @click="resetValidation" block>
          Reset Validation
        </v-btn>
      </v-col>
    </v-row>
  </v-form>
</template>

<script>
import emailjs from "emailjs-com";

export default {
  data: () => ({
    userId: "user_lu9iDjdEdPJh0rnNkgQXa",
    templateId: "editifyjs",
    serviceId: "service_editifyjs",
    valid: true,
    name: "",
    nameRules: [
      (v) => !!v || "Name is required",
      (v) => (v && v.length <= 20) || "Name must be less than 20 characters",
    ],
    email: "",
    emailRules: [
      (v) => !!v || "E-mail is required",
      (v) => /.+@.+\..+/.test(v) || "E-mail must be valid",
    ],
    meessage: "",
    select: null,
    items: ["Issue", "Comment", "Proposal", "Greeting"],
  }),

  methods: {
    validate() {
      if (this.$refs.form.validate()) {
        this.sendEmail();
      }
    },
    reset() {
      this.$refs.form.reset();
    },
    resetValidation() {
      this.$refs.form.resetValidation();
    },
    sendEmail() {
      try {
        emailjs.send(
          this.serviceId,
          this.templateId,
          {
            name: this.name,
            email: this.email,
            message: this.name + "\t" + this.email + "\t" + this.meessage,
          },
          this.userId
        );
        console.log("Mail sent!");
      } catch (error) {
        console.log({ error });
      }
      // Reset form field
      this.name = "";
      this.email = "";
      this.message = "";
    },
  },
};
</script>