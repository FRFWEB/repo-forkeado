<script setup>
import AuthenticatedLayout from "@/Layouts/AuthenticatedLayout.vue";
import ListItems from "@/Components/Amadeus/Inventory/ListItems.vue";
import { Head } from "@inertiajs/vue3";
import { ref } from "vue";

const props = defineProps({
    customroute: {
        type: String,
        default: () => "inventory.show",
    },
    items: {
        type: Array,
        default: () => [],
    },
    loan_agreement: {
        type: String,
        default: () => "",
    },
});

let modal = ref(false);
const openModal = () => {
    modal.value = true;
};

const closeModal = () => {
    modal.value = false;
};

const submitAddNewItem = () => {
    console.log("submit modal");
};
</script>

<template>
    <Head title="Inventario" />

    <AuthenticatedLayout :croute="customroute">
        <!-- LIST OF INVENTORY -->
        <div class="mx-auto">
            <h3>Lista de inventario</h3>
            <div v-for="item in items" :key="item.id">
                <ListItems
                    :type="item.type"
                    :name="item.name"
                    :brand="item.brand"
                    :itemId="item.id"
                    :status="item.status"
                />
            </div>
        </div>

        <!-- Modal -->

        <div v-if="modal == true">
            <div
                class="fixed top-0 flex right-0 justify-center items-center w-full h-screen bg-slate-900 bg-opacity-50 z-20"
            >
                <div
                    class="2xl:w-2/4 xl:w-1/3 lg:w-2/5 md:w-1/2 sm:w-1/2 xs:w-4/5 px-12 py-4 border-4 border-blue-500 rounded-3xl bg-white shadow-lg shadow-violet-500"
                >
                    <div class="flex justify-end">
                        <div class="flex-1 p-1">
                            <button
                                @click="closeModal()"
                                class="block ml-auto mr-3"
                            >
                                <span>
                                    <i
                                        class="fa fa-times text-2xl text-blue-500"
                                        aria-hidden="true"
                                    ></i>
                                </span>
                            </button>
                        </div>
                    </div>
                    <div class="flex flex-row">
                        <div class="flex-1">
                            <h3
                                class="2xl:text-2xl xl:text-2xl lg:text-xl md:text-xl sm:text-xl xs:text-xl text-center text-blue-500 font-bold mb-4"
                            >
                                Añadir item
                            </h3>
                        </div>
                    </div>
                    <div class="flex flex-row justify-center">
                        <div class="basis-1/2 mx-4">
                            <div>
                                <div>
                                    <label class="font-semibold text-lg"
                                        >Tipo de item</label
                                    >
                                    <select
                                        name=""
                                        id=""
                                        class="w-100 rounded-2xl my-2 border-2 border-blue-500 text-blue-500 text-center"
                                    >
                                        <option value="">Seleccionar</option>
                                    </select>
                                </div>
                                <div>
                                    <label class="font-semibold text-lg"
                                        >Marca</label
                                    >
                                    <input
                                        v-model="item_brand"
                                        type="text"
                                        class="w-100 rounded-2xl my-2 border-2 border-blue-500 text-center"
                                        placeholder="Marca"
                                    />
                                </div>
                            </div>
                        </div>
                        <div class="basis-1/2 mx-4">
                            <div>
                                <label class="font-semibold text-lg"
                                    >Nombre</label
                                >
                                <input
                                    v-model="item_name"
                                    type="text"
                                    class="w-100 rounded-2xl my-2 border-2 border-blue-500 text-center"
                                    placeholder="Usuario"
                                />
                            </div>
                            <div>
                                <label class="font-semibold text-lg"
                                    >Modelo</label
                                >
                                <input
                                    v-model="item_model"
                                    type="text"
                                    class="w-100 rounded-2xl my-2 border-2 border-blue-500 text-center"
                                    placeholder="Modelo"
                                />
                            </div>
                        </div>
                    </div>
                    <div class="flex flex-row">
                        <div class="basis-1/5 mx-4">
                            <div>
                                <label class="font-semibold text-lg"
                                    >N. de serie</label
                                >
                                <input
                                    v-model="item_serial"
                                    type="number"
                                    class="w-100 rounded-2xl my-2 border-2 border-blue-500 text-center"
                                    placeholder="00000"
                                />
                            </div>
                        </div>
                        <div class="basis-1/5 mx-4">
                            <div>
                                <label class="font-semibold text-lg"
                                    >Fecha compra</label
                                >
                                <input
                                    v-model="item_date"
                                    type="date"
                                    class="w-100 rounded-2xl my-2 border-2 border-blue-500 text-center"
                                    placeholder="Marca"
                                />
                            </div>
                        </div>
                        <div class="basis-1/5 mx-4">
                            <div>
                                <label class="font-semibold text-lg"
                                    >Valor</label
                                >
                                <input
                                    v-model="item_value"
                                    type="number"
                                    class="w-100 rounded-2xl my-2 border-2 border-blue-500 text-center"
                                    placeholder="0000"
                                />
                            </div>
                        </div>
                        <div class="basis-1/5 mx-4">
                            <div>
                                <label class="font-semibold text-lg"
                                    >Cantidad</label
                                >
                                <input
                                    v-model="item_cant"
                                    type="number"
                                    class="w-100 rounded-2xl my-2 border-2 border-blue-500 text-center hover:border-blue-700"
                                    placeholder="1"
                                />
                            </div>
                        </div>
                    </div>
                    <div class="flex flex-row mt-5">
                        <div class="basis-1/2 mx-4">
                            <div>
                                <div>
                                    <button
                                        class="block w-100 rounded-2xl py-2 border-2 border-blue-500 hover:bg-blue-600 hover:border-blue-700 hover:text-white text-blue-500 font-bold outline-none"
                                    >
                                        Añadir imagen
                                    </button>
                                </div>
                            </div>
                        </div>
                        <div class="basis-1/2 mx-4">
                            <div>
                                <button
                                    @click="submitAddNewItem()"
                                    class="block w-100 py-2 rounded-2xl text-white bg-blue-500 hover:bg-blue-600 font-bold outline-none"
                                >
                                    Añadir
                                </button>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>

        <!-- Button trigger modal -->
        <div
            class="absolute bottom-9 right-8 cursor-pointer"
            @click="openModal()"
            id="add_item_modal"
        >
            <div>
                <span
                    class="px-3 py-1 text-white rounded-full font-bold bg-blue-600 text-3xl"
                    >+</span
                >
            </div>
        </div>
    </AuthenticatedLayout>
</template>

<style scoped>
.icon-size {
    font-size: 15px;
}

input[type="number"]::-webkit-inner-spin-button {
    -webkit-appearance: none;
}
</style>
