<template>
  <app-layout>
    <template #header>
      <h2 class="font-semibold text-xl text-gray-800 leading-tight">
        Edit File
      </h2>
    </template>
    <div class="max-w-7xl mx-auto sm:px-6 lg:px-8 py-4">
      <div class="">
        <div
          class="
            text-center
            bg-red-100
            border border-red-400
            text-red-700
            px-4
            py-2
            rounded
          "
          role="alert"
          v-if="isError"
        >
          {{ firstError }}
        </div>
        <form @submit.prevent="submit">
          <div class="grid grid-cols-2">
            <div class="p-2 mr-2 mb-2 mt-4 ml-6 flex flex-wrap">
              <label class="my-2 mr-8 text-right w-36 font-bold"
                >File No :</label
              >
              <input
                type="text"
                v-model="form.file_no"
                class="
                  pr-2
                  pb-2
                  w-full
                  lg:w-2/4
                  rounded-md
                  placeholder-indigo-300
                "
                label="file_no"
                placeholder="Enter File No :"
              />
              <!-- <div v-if="errors.file_no">
                {{ errors.file_no }}
              </div> -->
            </div>

            <div class="p-2 mr-2 mb-2 mt-4 ml-6 flex flex-wrap">
              <label class="my-2 mr-8 text-right w-36 font-bold"
                >File Code :</label
              >
              <input
                type="text"
                v-model="form.file_code"
                class="
                  pr-2
                  pb-2
                  w-full
                  lg:w-2/4
                  rounded-md
                  placeholder-indigo-300
                "
                label="file_code"
                placeholder="Enter File Code :"
              />
              <div v-if="errors.file_code">
                {{ errors.file_code }}
              </div>
            </div>

            <div class="p-2 mr-2 mb-2 mt-4 ml-6 flex flex-wrap">
              <label class="my-2 mr-8 text-right w-36 font-bold">GD No :</label>
              <input
                type="text"
                v-model="form.gd_no"
                class="
                  pr-2
                  pb-2
                  w-full
                  lg:w-2/4
                  rounded-md
                  placeholder-indigo-300
                "
                label="gd_no"
                placeholder="Enter GD No :"
              />
              <div v-if="errors.gd_no">{{ errors.gd_no }}</div>
            </div>

            <div class="p-2 mr-2 mb-2 mt-4 ml-6 flex flex-wrap">
              <label class="my-2 mr-8 text-right w-36 font-bold"
                >Bond No :</label
              >
              <input
                type="text"
                v-model="form.bond_no"
                class="
                  pr-2
                  pb-2
                  w-full
                  lg:w-2/4
                  rounded-md
                  placeholder-indigo-300
                "
                label="bond_no"
                placeholder="Enter Bond No :"
              />
              <div v-if="errors.bond_no">
                {{ errors.bond_no }}
              </div>
            </div>

            <div class="p-2 mr-2 mb-2 mt-4 ml-6 flex flex-wrap">
              <label class="my-2 mr-8 text-right w-36 font-bold"
                >Date Bond :</label
              >
              <input
                type="text"
                v-model="form.date_bond"
                class="
                  pr-2
                  pb-2
                  w-full
                  lg:w-2/4
                  rounded-md
                  placeholder-indigo-300
                "
                label="bond_no"
                placeholder="Enter Date Bond :"
              />
              <div v-if="errors.date_bond">
                {{ errors.date_bond }}
              </div>
            </div>

            <div class="p-2 mr-2 mb-2 mt-4 ml-6 flex flex-wrap">
              <label class="my-2 mr-8 text-right w-36 font-bold"
                >Description :</label
              >
              <input
                type="text"
                v-model="form.description"
                class="
                  pr-2
                  pb-2
                  w-full
                  lg:w-2/4
                  rounded-md
                  placeholder-indigo-300
                "
                label="description"
                placeholder="Enter Description :"
              />
              <div v-if="errors.description">
                {{ errors.description }}
              </div>
            </div>

            <div class="p-2 mr-2 mb-2 mt-4 ml-6 flex flex-wrap">
              <label class="my-2 mr-8 text-right w-36 font-bold"
                >Vessel :</label
              >
              <input
                type="text"
                v-model="form.vessel"
                class="
                  pr-2
                  pb-2
                  w-full
                  lg:w-2/4
                  rounded-md
                  placeholder-indigo-300
                "
                label="vessel"
                placeholder="Enter Vessel :"
              />
              <div v-if="errors.vessel">{{ errors.vessel }}</div>
            </div>

            <div class="p-2 mr-2 mb-2 mt-4 ml-6 flex flex-wrap">
              <label class="my-2 mr-8 text-right w-36 font-bold"
                >Gross Weight :</label
              >
              <input
                type="text"
                v-model="form.gross_wt"
                class="
                  pr-2
                  pb-2
                  w-full
                  lg:w-2/4
                  rounded-md
                  placeholder-indigo-300
                "
                label="gross_wt"
                placeholder="Enter Gross Weight :"
              />
              <div v-if="errors.gross_wt">
                {{ errors.gross_wt }}
              </div>
            </div>

            <div class="p-2 mr-2 mb-2 mt-4 ml-6 flex flex-wrap">
              <label class="my-2 mr-8 text-right w-36 font-bold"
                >Net Weight :</label
              >
              <input
                type="text"
                v-model="form.net_wt"
                class="
                  pr-2
                  pb-2
                  w-full
                  lg:w-2/4
                  rounded-md
                  placeholder-indigo-300
                "
                label="net_wt"
                placeholder="Enter Net Weight :"
              />
              <div v-if="errors.net_wt">{{ errors.net_wt }}</div>
            </div>

            <div class="p-2 mr-2 mb-2 mt-4 ml-6 flex flex-wrap">
              <label class="my-2 mr-8 text-right w-36 font-bold">BL No :</label>
              <input
                type="text"
                v-model="form.bl_no"
                class="
                  pr-2
                  pb-2
                  w-full
                  lg:w-2/4
                  rounded-md
                  placeholder-indigo-300
                "
                label="bl_no"
                placeholder="Enter BL No :"
              />
              <div v-if="errors.bl_no">{{ errors.bl_no }}</div>
            </div>

            <div class="p-2 mr-2 mb-2 mt-4 ml-6 flex flex-wrap">
              <label class="my-2 mr-8 text-right w-36 font-bold"
                >VIR No :</label
              >
              <input
                type="text"
                v-model="form.vir_no"
                class="
                  pr-2
                  pb-2
                  w-full
                  lg:w-2/4
                  rounded-md
                  placeholder-indigo-300
                "
                label="vir_no"
                placeholder="Enter VIR No :"
              />
              <div v-if="errors.vir_no">{{ errors.vir_no }}</div>
            </div>

            <div class="p-2 mr-2 mb-2 mt-4 ml-6 flex flex-wrap">
              <label class="my-2 mr-8 text-right w-36 font-bold"
                >Index No :</label
              >
              <input
                type="text"
                v-model="form.index_no"
                class="
                  pr-2
                  pb-2
                  w-full
                  lg:w-2/4
                  rounded-md
                  placeholder-indigo-300
                "
                label="index_no"
                placeholder="Enter Index No :"
              />
              <div v-if="errors.index_no">
                {{ errors.index_no }}
              </div>
            </div>

            <div class="p-2 mr-2 mb-2 mt-4 ml-6 flex flex-wrap">
              <label class="my-2 mr-8 text-right w-36 font-bold"
                >Insurance :</label
              >
              <input
                type="text"
                v-model="form.insurance"
                class="
                  pr-2
                  pb-2
                  w-full
                  lg:w-2/4
                  rounded-md
                  placeholder-indigo-300
                "
                label="insurance"
                placeholder="Enter Insurance :"
              />
              <div v-if="errors.insurance">
                {{ errors.insurance }}
              </div>
            </div>

            <div class="p-2 mr-2 mb-2 mt-4 ml-6 flex flex-wrap">
              <label class="my-2 mr-8 text-right w-36 font-bold">LC No :</label>
              <input
                type="text"
                v-model="form.lc_no"
                class="
                  pr-2
                  pb-2
                  w-full
                  lg:w-2/4
                  rounded-md
                  placeholder-indigo-300
                "
                label="lc_no"
                placeholder="Enter LC No :"
              />
              <div v-if="errors.lc_no">{{ errors.lc_no }}</div>
            </div>

            <div class="p-2 mr-2 mb-2 mt-4 ml-6 flex flex-wrap">
              <label class="my-2 mr-8 text-right w-36 font-bold"
                >Amount :</label
              >
              <input
                type="number"
                v-model="form.amount"
                class="
                  pr-2
                  pb-2
                  w-full
                  lg:w-2/4
                  rounded-md
                  placeholder-indigo-300
                "
                label="amount"
                placeholder="Enter Amount :"
              />
              <div v-if="errors.amount">{{ errors.amount }}</div>
            </div>

            <!-- <div class="p-2 mr-2 mb-2 mt-4 ml-6 flex flex-wrap">
                            <label class="my-2 mr-8 text-right w-36 font-bold"
                                >Sale Tax :</label
                            >
                            <input
                                type="number"
                                v-model="form.s_tax"
                                class="
                                    pr-2
                                    pb-2
                                    w-full
                                    lg:w-2/4
                                    rounded-md
                                    placeholder-indigo-300
                                "
                                label="s_tax"
                                placeholder="Enter Sale Tax :"
                            />
                            <div v-if="errors.s_tax">{{ errors.s_tax }}</div>
                        </div> -->

            <div class="p-2 mr-2 mb-2 mt-4 ml-6 flex flex-wrap">
              <label class="my-2 mr-8 text-right w-36 font-bold"
                >Quantity :</label
              >
              <input
                type="number"
                v-model="form.qty"
                class="
                  pr-2
                  pb-2
                  w-full
                  lg:w-2/4
                  rounded-md
                  placeholder-indigo-300
                "
                label="qty"
                placeholder="Enter Quantity :"
              />
              <div v-if="errors.qty">{{ errors.qty }}</div>
            </div>

            <div class="p-2 mr-2 mb-2 ml-6 flex flex-wrap">
              <label class="my-2 mr-8 text-right w-36 font-bold"
                >Select Agent :</label
              >
              <multiselect
                class="rounded-md border border-black lg:w-2/4"
                v-model="form.agent_id"
                :options="agents"
                placeholder="Select Agent"
                label="name"
                track-by="id"
              ></multiselect>
              <div v-if="errors.agent_id">
                {{ errors.agent_id }}
              </div>
            </div>

            <div class="p-2 mr-2 mb-2 ml-6 flex flex-wrap">
              <label class="my-2 mr-8 text-right w-36 font-bold"
                >Select Importer :</label
              >
              <multiselect
                class="rounded-md border border-black lg:w-2/4"
                v-model="form.importer_id"
                :options="importers"
                placeholder="Select Importer"
                label="name"
                track-by="id"
              ></multiselect>
              <!-- <div v-if="errors.importer_id">
                {{ errors.importer_id }}
              </div> -->
            </div>

            <div class="p-2 mr-2 mb-2 ml-6 flex flex-wrap">
              <label class="my-2 mr-8 text-right w-36 font-bold"
                >Select Client :</label
              >
              <multiselect
                class="rounded-md border border-black lg:w-2/4"
                v-model="form.client_id"
                :options="clients"
                placeholder="Select Client"
                label="name"
                track-by="id"
              ></multiselect>
              <div v-if="errors.client_id">
                {{ errors.client_id }}
              </div>
            </div>

            <div
              class="
                px-4
                py-2
                bg-gray-100
                border-t border-gray-200
                flex flex-row
                justify-center
                ml-16
              "
            >
              <button
                class="
                  border
                  bg-indigo-300
                  rounded-xl
                  px-4
                  py-2
                  ml-4
                  mt-4
                  lg:w-2/4
                "
                type="submit"
              >
                Update File
              </button>
            </div>
          </div>
        </form>
      </div>
    </div>
  </app-layout>
</template>

<script>
import AppLayout from "@/Layouts/AppLayout";
import Label from "../../Jetstream/Label.vue";
import Multiselect from "@suadelabs/vue3-multiselect";

export default {
  components: {
    AppLayout,
    Multiselect,
  },

  props: {
    errors: Object,
    file: Object,

    agents: Array,
    importers: Array,
    clients: Array,

    agent: Array,
    importer: Array,
    client: Array,
  },

  data() {
    return {
      agents: this.agents,
      importers: this.importers,
      clients: this.clients,

      form: this.$inertia.form({
        file_no: this.file.file_no,
        file_code: this.file.file_code,
        gd_no: this.file.gd_no,
        bond_no: this.file.bond_no,
        date_bond: this.file.date_bond,
        description: this.file.description,
        vessel: this.file.vessel,
        gross_wt: this.file.gross_wt,
        net_wt: this.file.net_wt,
        bl_no: this.file.bl_no,
        vir_no: this.file.vir_no,
        index_no: this.file.index_no,
        insurance: this.file.insurance,
        lc_no: this.file.lc_no,
        amount: this.file.amount,
        s_tax: this.file.s_tax,
        qty: this.file.qty,

        // agent_id: this.file.agent_id,
        // importer_id: this.file.importer_id,
        // client_id: this.file.client_id,
        agent_id: this.agent,
        importer_id: this.importer,
        client_id: this.client,
      }),
    };
  },

  methods: {
    submit() {
      this.$inertia.put(route("files.update", this.file.id), this.form);
    },
  },
  watch: {
    errors: function () {
      if (this.errors) {
        this.firstError = this.errors[Object.keys(this.errors)[0]];
        this.isError = true;
      }
    },
  },
};
</script>
