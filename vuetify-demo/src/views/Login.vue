<template>
  <v-container fluid>
    <v-overlay class="align-center justify-center" :model-value="isLoading">
      <v-progress-circular color="white" indeterminate v-if="isLoading">
      </v-progress-circular>
    </v-overlay>
    <v-row justify="center">
      <v-col md="4">
        <v-card class="p-8">
          <v-card-item>
            <v-card-title class="text-center">Login Here</v-card-title>
            <v-form @submit.prevent="submit">
              <v-text-field
                v-model="form.email"
                :rules="[rules.required]"
                prepend-inner-icon="mdi-email"
                label="Email"
              ></v-text-field>

              <v-text-field
                type="password"
                v-model="form.password"
                :rules="[rules.required]"
                prepend-inner-icon="mdi-key"
                label="Password"
              ></v-text-field>

              <v-checkbox
                v-model="form.remember"
                color="red"
                label="Remember me"
                value="red"
                hide-details
              ></v-checkbox>

              <v-btn
                class="mt-2"
                variant="elevated"
                color="red-darken-1"
                type="submit"
                block
              >
                <span>Submit</span>
              </v-btn>
            </v-form>
          </v-card-item>
          <v-card-action>
            <div class="mx-4">
              <v-btn block to="/register">Register</v-btn>
            </div>
          </v-card-action>
        </v-card>
      </v-col>
    </v-row>
  </v-container>
</template>

<script setup lang="ts">
import { ref } from "vue";

const form = ref({
  email: "",
  password: "",
  remember: "",
});

const isLoading = ref(false);

function submit() {
  if (form.value.email === "") {
    return;
  }
  isLoading.value = true;
  setTimeout(() => {
    isLoading.value = false;
    alert(JSON.stringify(form.value));
  }, 3000);
}

const rules = {
  required: (value) => !!value || "Required.",
  email: (value) => {
    const pattern =
      /^(([^<>()[\]\\.,;:\s@"]+(\.[^<>()[\]\\.,;:\s@"]+)*)|(".+"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/;
    return pattern.test(value) || "Invalid e-mail.";
  },
};
</script>
