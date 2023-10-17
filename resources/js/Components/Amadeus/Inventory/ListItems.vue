<script setup>
import { ref } from "vue";

const props = defineProps({
    status: {
        type: String,
    },
    type: {
        type: String,
    },
    itemId: {
        type: Number,
    },
    brand: {
        type: String,
    },
    name: {
        type: String,
    },
});

// SET BORDER COLOR BOTTON
const setBorderBottom = (status) => {
    switch (status) {
        case "Disponible":
            return "border-green-500";
        case "Prestamo":
            return "border-yellow-500";
        case "Reparación":
            return "border-red-600";
        case "No disponible":
            return "border-black";
        default:
            return "";
    }
};

//SET STATUS ICON
const setStatusIcon = (status) => {
    switch (status) {
        case "Disponible":
            return '<i class="fa fa-check-circle text-green-500" aria-hidden="true"></i>';
        case "Prestamo":
            return '<i class="fa fa-times-circle text-yellow-500" aria-hidden="true"></i>';
        case "Reparación":
            return '<i class="fa fa-info-circle text-red-600" aria-hidden="true"></i>';
        case "No disponible":
            return '<i class="fa fa-exclamation-triangle text-black" aria-hidden="true"></i>';
        default:
            return "";
    }
};

// OPEN DETAILS BY ITEM
let itemDetails = ref(0);
const openItemDetails = (index) => {
    let getItem = document.querySelectorAll("#product_item")[index - 1];
    if (getItem.classList.contains("details-active")) {
        itemDetails.value = 0;
        getItem.classList.remove("details-active");
    } else {
        itemDetails.value = index;
        getItem.classList.add("details-active");
    }
};
</script>

<template>
    <div>
        <div class="shadow-sm sm:rounded-lg amadeus-box">
            <!-- rounded-full -->
            <div
                :class="setBorderBottom(this.status)"
                id="product_item"
                class="p-4 my-5 rounded-4xl border-b-4 shadow-[rgba(17,_17,_26,_0.1)_0px_0px_16px]"
            >
                <div class="grid grid-rows-1 grid-cols-4">
                    <div class="flex justify-center items-center">
                        <div class="flex items-center">
                            <div class="mr-6">
                                <i
                                    class="fa-light fa-music"
                                    aria-hidden="true"
                                ></i>
                            </div>
                            <div>
                                <p class="m-0 font-bold">
                                    {{ this.type }}
                                </p>
                            </div>
                        </div>
                    </div>
                    <div>
                        <span
                            @click="openItemDetails(this.itemId)"
                            class="cursor-pointer text-blue-500"
                            ><p class="m-0 font-bold">
                                {{ this.name }}
                            </p></span
                        >
                    </div>
                    <div>
                        <p class="m-0">{{ this.brand }}</p>
                    </div>
                    <div class="flex justify-center">
                        <div class="mr-6">
                            <p class="m-0 font-bold">
                                {{ this.status }}
                            </p>
                        </div>
                        <div>
                            <span
                                class="icon-size"
                                v-html="setStatusIcon(this.status)"
                            ></span>
                        </div>
                    </div>
                </div>

                <div v-if="itemDetails == this.itemId">
                    <div
                        class="grid grid-cols-5 border-t-2 mt-3 px-5 py-4 text-center"
                    >
                        <div>
                            <div>
                                <p class="m-0 font-bold">Modelo:</p>
                                <p>----</p>
                            </div>
                        </div>
                        <div>
                            <div>
                                <p class="m-0 font-bold">Num de serie:</p>
                                <p>----</p>
                            </div>
                        </div>
                        <div>
                            <div>
                                <p class="m-0 font-bold">Fecha de compra:</p>
                                <p>----</p>
                            </div>
                        </div>
                        <div>
                            <div>
                                <p class="m-0 font-bold">Valor:</p>
                                <p>1200$</p>
                            </div>
                        </div>
                        <div>
                            <div>
                                <p>x1</p>
                            </div>
                        </div>
                    </div>
                    <div
                        class="grid grid-cols-1 border-t-2 mt-2 px-5 py-4 text-center"
                    >
                        <div>
                            <div>
                                <p class="m-0 font-bold text-left pl-5 mb-4">
                                    Obvervaciónes:
                                </p>
                            </div>
                            <div>
                                <a
                                    href="#"
                                    class="m-0 font-bold underline-offset-15 text-center+"
                                >
                                    Ver imagen
                                </a>
                            </div>
                        </div>
                    </div>
                    <div
                        class="grid grid-cols-3 gap-4 border-t mt-3 px-5 py-4 text-center"
                    >
                        <div>
                            <div>
                                <button
                                    class="block w-100 relative rounded-2xl py-2 border-2 border-blue-500 hover:bg-blue-600 hover:border-blue-700 hover:text-white text-blue-500 font-bold outline-none"
                                >
                                    Hisotiral Prestamos
                                    <span
                                        class="text-2xl absolute right-4 top-1"
                                        >+</span
                                    >
                                </button>
                            </div>
                        </div>
                        <div>
                            <div>
                                <button
                                    class="block w-100 relative rounded-2xl py-2 border-2 border-blue-500 hover:bg-blue-600 hover:border-blue-700 hover:text-white text-blue-500 font-bold outline-none"
                                >
                                    Historial Reparaciones
                                    <span
                                        class="text-2xl absolute right-4 top-1"
                                        >+</span
                                    >
                                </button>
                            </div>
                        </div>
                        <div>
                            <div>
                                <button
                                    class="block w-100 py-2 relative rounded-2xl text-white bg-blue-500 hover:bg-blue-600 font-bold outline-none"
                                >
                                    Realizar Prestamo
                                    <span
                                        class="text-2xl absolute right-4 top-1"
                                        >+</span
                                    >
                                </button>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<style scoped></style>
