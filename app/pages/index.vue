<script setup lang="ts">
import * as v from "valibot";
import type { FormSubmitEvent } from "@nuxt/ui";
import { useRouter } from "vue-router";

const schema = v.object({
  name: v.pipe(v.string(), v.minLength(1, "Must be at least 1 character")),
  password: v.pipe(v.string(), v.minLength(8, "Must be at least 8 characters")),
});

type Schema = v.InferOutput<typeof schema>;

const state = reactive({
  name: "",
  password: "",
});

const toast = useToast();
const router = useRouter();
async function onSubmit(event: FormSubmitEvent<Schema>) {
  try {
    const response = await fetch("http://localhost:5139/api/auth/login", {
      method: "POST",
      headers: {
        "Content-Type": "application/json",
      },
      body: JSON.stringify({
        name: state.name,
        password: state.password,
      }),
    });

    if (!response.ok) {
        
      console.log("Login gagal!");
    }

    const data = await response.json();
    console.log("Login berhasil:", data);
    localStorage.setItem("token", data.token);
    toast.add({
      title: "Success",
      description: "Login berhasil.",
      color: "success",
    });
    router.push("/dashboard");
  } catch (err) {
    toast.add({
      title: "Error",
      description: err instanceof Error ? err.message : "Login gagal",
      color: "error",
    });
    console.log(err);
  }
}
</script>

<template>
<div class="min-h-screen flex items-center justify-center">
    <div class="flex flex-col items-center mb-6">
      <h2 class="text-2xl font-semibold text-gray-200 tracking-wide">Inventory Management System</h2>
      <p class="text-lg text-gray-400">Manage your inventory efficiently</p>
    </div>
    
    <UCard class="w-full max-w-md p-6 mx-auto my-auto">
        <UForm
            :schema="schema"
            :state="state"
            @submit="onSubmit"
            class="flex flex-col gap-4"
        >
            <UFormField label="Username" name="username">
                <UInput v-model="state.name" class="mt-2 w-full" />
            </UFormField>
            <UFormField label="Password" name="password">
                <UInput
                    v-model="state.password"
                    type="password"
                    class="mt-2 w-full"
                />
            </UFormField>
            <UButton type="submit" class="mt-2 w-full flex justify-center items-center"> Submit </UButton>
        </UForm>
    </UCard>
</div>
</template>

<style scoped></style>
