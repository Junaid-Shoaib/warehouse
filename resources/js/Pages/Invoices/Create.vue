<template>
  <app-layout>
    <template #header>
      <h2 class="font-semibold text-xl text-gray-800 leading-tight">
        Create Invoice
      </h2>
    </template>
    <div
      v-if="$page.props.flash.success"
      class="bg-yellow-600 text-white text-center"
    >
      {{ $page.props.flash.success }}
    </div>
    <div
      v-if="$page.props.flash.warning"
      class="bg-yellow-600 text-white text-center"
    >
      {{ $page.props.flash.warning }}
    </div>

    <div class="max-w-7xl mx-auto sm:px-6 lg:px-8 py-4">
      <div class="">
        <form @submit.prevent="form.post(route('invoices.store'))">
          <!-- <div class="p-2 mr-2 mb-2 mt-4 ml-6 flex flex-wrap">
            <label class="my-2 mr-8 text-right w-36 font-bold">File No :</label>
            <select
              v-model="form.file_id"
              class="
                pr-2
                pb-2
                w-full
                lg:w-1/4
                rounded-md
                placeholder-indigo-300
              "
            >
              <option v-for="file in files" :key="file.id" :value="file.id">
                {{ file.file_no }}
              </option>
            </select>
            <div v-if="errors.file_id">{{ errors.file_id }}</div>
          </div> -->

          <div class="p-2 mr-2 mb-2 ml-6 flex flex-wrap">
            <label class="my-2 mr-8 text-right w-36 font-bold"
              >Select File :</label
            >
            <multiselect
              style="width: 25%"
              class="rounded-md border border-black"
              v-model="form.file_id"
              :options="files"
              placeholder="Select File"
              label="file_no"
              track-by="id"
            ></multiselect>
            <div
              class="
                ml-2
                bg-red-100
                border border-red-400
                text-red-700
                px-4
                py-2
                rounded
                relative
              "
              role="alert"
              v-if="errors.file_id"
            >
              {{ errors.file_id }}
            </div>
          </div>

          <div class="p-2 mr-2 mb-2 mt-4 ml-6 flex flex-wrap">
            <label class="my-2 mr-8 text-right w-36 font-bold">Date:</label
            ><input
              type="date"
              v-model="form.date"
              class="
                pr-2
                pb-2
                w-full
                lg:w-1/4
                rounded-md
                placeholder-indigo-300
              "
              label="date"
              placeholder="xyz"
            />
            <div
              class="
                ml-2
                bg-red-100
                border border-red-400
                text-red-700
                px-4
                py-2
                rounded
                relative
              "
              role="alert"
              v-if="errors.date"
            >
              {{ errors.date }}
            </div>
          </div>

          <div class="p-2 mr-2 mb-2 mt-4 ml-6 flex flex-wrap">
            <label class="my-2 ml-4 mr-5 text-right w-38 font-bold"
              >Sales Tax Excluded :</label
            >
            <input
              v-model="form.tax_status"
              name="tax_status"
              type="radio"
              value="0"
              class="pr-2 pb-2 rounded-md placeholder-indigo-300"
            />

            <label class="my-2 ml-2 mr-5 text-right w-38 font-bold"
              >Sales Tax Included :</label
            >
            <input
              v-model="form.tax_status"
              name="tax_status"
              type="radio"
              value="1"
              class="pr-2 pb-2 rounded-md placeholder-indigo-300"
            />

            <label class="my-2 mr-5 text-right w-16 font-bold">None :</label>
            <input
              v-model="form.tax_status"
              name="tax_status"
              type="radio"
              value="2"
              class="pr-2 pb-2 rounded-md placeholder-indigo-300"
            />
          </div>

          <div class="p-2 mr-2 mb-2 mt-4 ml-6 flex flex-wrap">
            <label class="my-2 mr-8 text-right w-36 font-bold">Amount:</label
            ><input
              type="number"
              @change="cal_s_tax"
              v-model="form.amount"
              class="
                pr-2
                pb-2
                w-full
                lg:w-1/4
                rounded-md
                placeholder-indigo-300
              "
              label="date"
              placeholder="10,000"
            />
            <div
              class="
                ml-2
                bg-red-100
                border border-red-400
                text-red-700
                px-4
                py-2
                rounded
                relative
              "
              role="alert"
              v-if="errors.amount"
            >
              {{ errors.amount }}
            </div>
          </div>

          <div
            v-if="form.tax_status != 2"
            class="p-2 mr-2 mb-2 mt-4 ml-6 flex flex-wrap"
          >
            <label class="my-2 mr-8 text-right w-36 font-bold">Sales Tax:</label
            ><input
              type="number"
              v-model="form.s_tax"
              class="
                pr-2
                pb-2
                w-full
                lg:w-1/4
                rounded-md
                placeholder-indigo-300
              "
              readonly
              label="date"
              placeholder="0"
            />
            <div v-if="errors.s_tax">{{ errors.s_tax }}</div>
          </div>

          <div class="p-2 mr-2 mb-2 mt-4 ml-6 flex flex-wrap">
            <label class="my-2 mr-8 text-right w-36 font-bold">Total:</label
            ><input
              type="number"
              v-model="form.total"
              class="
                pr-2
                pb-2
                w-full
                lg:w-1/4
                rounded-md
                placeholder-indigo-300
              "
              readonly
              label="date"
              placeholder="0"
            />
            <div v-if="errors.total">{{ errors.total }}</div>
          </div>

          <div
            class="
              px-4
              py-2
              bg-gray-100
              border-t border-gray-200
              flex
              justify-center
              items-center
            "
          >
            <button
              class="border bg-indigo-300 rounded-xl px-4 py-2 ml-4 mt-4"
              type="submit"
              :disabled="form.processing"
            >
              Create Invoice
            </button>
          </div>
        </form>
      </div>
    </div>
  </app-layout>
</template>

<script>
import AppLayout from "@/Layouts/AppLayout";
import { useForm } from "@inertiajs/inertia-vue3";
import Multiselect from "@suadelabs/vue3-multiselect";

export default {
  components: {
    AppLayout,
    Multiselect,
  },

  props: {
    errors: Object,
    files: Array,
  },

  setup(props) {
    const form = useForm({
      tax_status: 0,
      file_id: null,
      date: new Date().toISOString().substr(0, 10),
      amount: null,
      s_tax: 0,
      total: null,
    });
    return { form };
  },

  watch: {
    amount: function (new_Value, old_Value) {
      console.log("hello");
    },
    //   if (this.errors) {
    // this.firstError = this.errors[Object.keys(this.errors)[0]];
    // this.isError = true;
    //   }
  },

  methods: {
    cal_s_tax() {
      if (this.form.tax_status == 2) {
        this.form.s_tax = 0;
      } else if (this.form.tax_status == 0) {
        this.form.s_tax = parseInt((this.form.amount * 13) / 100).toFixed(2);
      } else {
        this.form.s_tax = parseInt(
          this.form.amount - this.form.amount / 1.13
        ).toFixed(2);
        this.form.amount = parseInt(this.form.amount - this.form.s_tax).toFixed(
          2
        );
      }
      this.form.total = (
        parseInt(this.form.amount) + parseInt(this.form.i_tax)
      ).toFixed(2);
    },
  },

  //   computed: {
  //     total() {
  //       return this.form.amount + this.form.s_tax;
  //     },
  //   },
};
</script>
