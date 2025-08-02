<template>
  <section class="bg-green-50">
    <div class="container m-auto max-w-2xl py-24">
      <div
        class="bg-white px-6 py-8 mb-4 shadow-md rounded-md border m-4 md:m-0"
      >
        <form @submit.prevent="handleSubmit">
          <h2 class="text-3xl text-center font-semibold mb-6">Edit Job</h2>
          <div class="mb-4">
            <label class="block text-gray-700 font-bold mb-2">Title</label>
            <input
              v-model="form.title"
              type="text"
              name="title"
              id="title"
              class="border rounded w-full py-2 px-3 mb-2"
              placeholder="eg. Beautiful Apartment In Miami"
              required
            />
          </div>
          <div class="mb-4">
            <label for="type" class="block text-gray-700 font-bold mb-2">
              Job Type
            </label>
            <select
              v-model="form.type"
              name="type"
              id="type"
              class="border rounded w-full py-2 px-3"
              required
            >
              <option value="Full-Time">Full Time</option>
              <option value="Part-Time">Part Time</option>
              <option value="Remote">Remote</option>
              <option value="Internship">Internship</option>
            </select>
          </div>
          <div class="mb-4">
            <label for="description" class="block text-gray-700 font-bold mb-2"
              >Description</label
            >
            <textarea
              v-model="form.description"
              name="description"
              id="description"
              class="border rounded w-full py-2 px-3"
              rows="4"
              placeholder="Add job desc"
            ></textarea>
          </div>
          <div class="mb-4">
            <label for="salary" class="block text-gray-700 font-bold mb-2"
              >Salary</label
            >
            <select
              v-model="form.salary"
              name="salary"
              id="salary"
              class="border rounded w-full py-2 px-3"
              required
            >
              <option value="Under $50K">Under $50K</option>
              <option value="$50K - $60K">$50K - $60K</option>
              <option value="$70K - $80K">$70K - $80K</option>
              <option value="$90K - $100K">$90K - $100K</option>
              <option value="$110K - $120K">$110K - $120K</option>
            </select>
          </div>
          <div class="mb-4">
            <label class="block text-gray-700 font-bold mb-2">Location</label>
            <input
              v-model="form.location"
              type="text"
              name="location"
              id="location"
              class="border rounded w-full py-2 px-3 mb-2"
              placeholder="Company Location"
              required
            />
          </div>
          <h3 class="">Company Information</h3>
          <div class="mb-4">
            <label class="block text-gray-700 font-bold mb-2"
              >Company name</label
            >
            <input
              v-model="form.company.name"
              type="text"
              name="company_name"
              id="company_name"
              class="border rounded w-full py-2 px-3 mb-2"
              placeholder="Company name"
              required
            />
          </div>
          <div class="mb-4">
            <label
              for="company_description"
              class="block text-gray-700 font-bold mb-2"
              >Company Description</label
            >
            <textarea
              v-model="form.company.description"
              name="company_description"
              id="company_description"
              class="border rounded w-full py-2 px-3"
              rows="4"
              placeholder="Add job desc"
            ></textarea>
          </div>
          <div class="mb-4">
            <label class="block text-gray-700 font-bold mb-2"
              >Company Emails</label
            >
            <input
              v-model="form.company.contactEmail"
              type="email"
              name="company_email"
              id="company_email"
              class="border rounded w-full py-2 px-3 mb-2"
              placeholder="Company email"
              required
            />
          </div>
          <div class="mb-4">
            <label class="block text-gray-700 font-bold mb-2"
              >Company Contact</label
            >
            <input
              v-model="form.company.contactPhone"
              type="tel"
              name="company_contact_phone"
              id="company_contact_phone"
              class="border rounded w-full py-2 px-3 mb-2"
              placeholder="Company phone"
              required
            />
          </div>
          <button
            type="submit"
            class="bg-green-600 w-full text-white p-2 text-center font-bold rounded-xl"
          >
            Edit Job
          </button>
        </form>
      </div>
    </div>
  </section>
</template>
<script setup>
import { onMounted, reactive } from "vue";
import axios from "axios";
import { useToast } from "vue-toastification";
import { useRoute } from "vue-router";
import router from "@/router";
const toast = useToast();
const route = useRoute();
let form = reactive({
  type: "Full-Time",
  title: "",
  description: "",
  salary: "",
  location: "",
  company: {
    name: "",
    description: "",
    contactEmail: "",
    contactPhone: "",
  },
});
const handleSubmit = async () => {
  try {
    const updateJob = {
      type: form.type,
      title: form.title,
      description: form.description,
      salary: form.salary,
      location: form.location,
      company: {
        name: form.company.name,
        description: form.company.description,
        contactEmail: form.company.contactEmail,
        contactPhone: form.company.contactPhone,
      },
    };
    let res = await axios.put(`/api/jobs/${route.params.id}`, updateJob);
    toast.success("Job edited successfully");
    router.push(`/jobs/${res.data.id}`);
  } catch (error) {
    toast.error("Error in editing job");
    console.log("Error fetching job", error);
  }
};
const setEdit = async () => {
  try {
    const res = await axios.get(`/api/jobs/${route.params.id}`);
    form.type = res.data.type;
    form.title = res.data.title;
    form.description = res.data.description;
    form.salary = res.data.salary;
    form.location = res.data.location;
    form.company = {
      name: res.data.company.name,
      description: res.data.company.description,
      contactEmail: res.data.company.contactEmail,
      contactPhone: res.data.company.contactPhone,
    };
  } catch (error) {
    console.log("Error in setting edit data", error);
  }
};
onMounted(async () => {
  await setEdit();
});
</script>
