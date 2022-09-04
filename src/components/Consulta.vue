<template>
    <v-layout style="z-index: 0">
        <v-app-bar>
            <v-avatar>
                <v-img src="/seabanck.png" alt="John"></v-img>
            </v-avatar>
            <v-app-bar-title class="text-h4 mx-4" style="color:#424242;">SeaBank</v-app-bar-title>
            <v-spacer></v-spacer>
            <v-btn @click="toggleTheme"
                :icon="theme.global.name.value == 'dark' ? 'mdi-white-balance-sunny' : 'mdi-weather-night'"></v-btn>
        </v-app-bar>
        <v-main>
            <v-container class="px-10">
                <v-row>
                    <v-col>
                        <v-img src="/pareja2.jpg"></v-img>
                    </v-col>
                </v-row>
                <v-row class="my-10">
                    <v-col md="5" class="px-2">
                        <h2 class="text-h2 mb-10" style="color:#424242;">Más cerca de tu casa propia</h2>
                        <p class=""
                            style="color:#424242; font-size: 24px; letter-spacing: 4px; white-space: normal;font-weight: normal;">
                            Hacer realidad tu plan de la casa propia es nuestro principal objetivo.
                            Desembolsa tu crédito en pocos días, nuestros asesores de créditos hipotecarios te ayudarán
                            en el proceso
                            y estarás respaldado por un Banco seguro y confiable.
                            Inicia la evaluación ingresando algunos datos e inmediatamente puedes saber si tu credito
                            está aprobado.
                        </p>
                    </v-col>
                    <v-col md="1" class="px-2"></v-col>
                    <v-col md="6" sm="6" cols="12">
                        <h2 class="text-h2" style="color:#424242;">Evaluacion de crédito hipotecario</h2>


                        <v-tabs v-model="tab" fixed-tabs color="basil">
                            <v-tab value="one">Datos primarios</v-tab>
                            <v-tab value="two">Datos secundarios</v-tab>
                        </v-tabs>
                        <br>
                        <v-window v-model="tab">
                            <v-window-item value="one">
                                <v-row>
                                    <v-col>
                                        <v-text-field label="Nombre y apellido" variant="outlined" v-model="name">
                                        </v-text-field>
                                    </v-col>
                                    <v-col>
                                        <v-text-field label="Ingresos" variant="outlined" v-model="datosUser.INCOME">
                                        </v-text-field>
                                    </v-col>
                                </v-row>

                                <v-row>
                                    <v-col>
                                        <v-select :items="EMPLOYMENT_STATUS" v-model="datosUser.EMPLOYMENT_STATUS"
                                            label="Estado laboral" variant="outlined">
                                        </v-select>
                                    </v-col>

                                    <v-col>
                                        <v-text-field label="Años de experiencia laboral" variant="outlined"
                                            v-model="datosUser.YRS_WITH_CURRENT_EMPLOYER" type="number"></v-text-field>
                                    </v-col>
                                </v-row>
                                <v-row>
                                    <v-col>
                                        <v-text-field label="Monto" variant="outlined"
                                            v-model="datosUser.PROPERTY_VALUE"></v-text-field>
                                    </v-col>
                                    <v-col>
                                        <v-text-field label="Record crediticio" variant="outlined"
                                            v-model="datosUser.CREDIT_SCORE" type="number"></v-text-field>
                                    </v-col>
                                </v-row>

                            </v-window-item>

                            <v-window-item value="two">
                                <h2 class="text-button" style="color:#424242;">Datos personales</h2>
                                <v-row class="px-2">
                                    <v-col>
                                        <v-select :items="MARITAL_STATUS" v-model="datosUser.MARITAL_STATUS"
                                            label="Estado civil" variant="outlined">
                                        </v-select>
                                    </v-col>
                                    <v-col>
                                        <v-select :items="GENDER" v-model="datosUser.GENDER" label="Género"
                                            variant="outlined">
                                        </v-select>
                                    </v-col>
                                    <v-col>
                                        <v-select :items="EDUCATION" v-model="datosUser.EDUCATION" label="Educación"
                                            variant="outlined">
                                        </v-select>
                                    </v-col>
                                </v-row>
                                <h2 class="text-button" style="color:#424242;">Datos residenciales</h2>
                                <v-row class="px-2">
                                    <v-col>
                                        <v-select :items="RESIDENCE" v-model="datosUser.RESIDENCE" label="Residencia"
                                            variant="outlined">
                                        </v-select>
                                    </v-col>
                                    <v-col>
                                        <v-text-field label="Años en su vivienda actual" variant="outlined"
                                            type="number" v-model="datosUser.YRS_AT_CURRENT_ADDRESS"></v-text-field>
                                    </v-col>
                                    <v-col>
                                        <v-text-field label="Precio promedio del área" variant="outlined"
                                            v-model="datosUser.AREA_AVG_PRICE"></v-text-field>
                                    </v-col>
                                </v-row>



                                <h2 class="text-button" style="color:#424242;">Historial de créditos</h2>
                                <v-divider></v-divider>
                                <br>
                                <v-row>
                                    <v-col>
                                        <v-text-field label="Nro de tarjetas" variant="outlined"
                                            v-model="datosUser.NUMBER_OF_CARDS" type="number"></v-text-field>
                                    </v-col>
                                    <v-col>
                                        <v-text-field label="Deuda en tarjetas" variant="outlined"
                                            v-model="datosUser.CREDITCARD_DEBT" type="number"></v-text-field>
                                    </v-col>
                                    <v-col>
                                        <v-text-field label="Monto de préstamos vigentes" variant="outlined"
                                            v-model="datosUser.LOAN_AMOUNT" type="number"></v-text-field>
                                    </v-col>
                                    <v-col>
                                        <v-text-field label="Nro de préstamos vigentes" variant="outlined"
                                            v-model="datosUser.LOANS" type="number">
                                        </v-text-field>
                                    </v-col>
                                </v-row>
                            </v-window-item>


                        </v-window>


                        <br>




                        <v-btn block color="success" size="large" @click="validar()">Consultar</v-btn>
                    </v-col>
                </v-row>
            </v-container>
        </v-main>
    </v-layout>
</template>
<script setup>
import { useTheme } from 'vuetify'
import { ref } from 'vue'
import Swal from 'sweetalert2'

const theme = useTheme()

const GENDER = ['Male', 'Female']
const EMPLOYMENT_STATUS = ['Employed', 'Medical Leave', 'Retired', 'Disabled', 'Unemployed']
const MARITAL_STATUS = ['Married', 'Divorced', 'Single']
const RESIDENCE = ["Owner Occupier", "Public Housing", "Private Renting", "Living with parents/guardian", "Sheltered"]
const EDUCATION = ["High School or Below", "Bachelor", "College", "Master", "Doctor"]

const datosUser = ref({
    INCOME: '',
    YRS_AT_CURRENT_ADDRESS: '11',
    YRS_WITH_CURRENT_EMPLOYER: '13',
    NUMBER_OF_CARDS: '2',
    CREDITCARD_DEBT: '1100',
    LOAN_AMOUNT: '7300',
    CREDIT_SCORE: '',
    PROPERTY_VALUE: '',
    AREA_AVG_PRICE: '0',
    LOANS: '1',
    GENDER: 'Male',
    EDUCATION: 'College',
    EMPLOYMENT_STATUS: 'Employed',
    MARITAL_STATUS: 'Married',
    APPLIEDONLINE: 'YES',
    RESIDENCE: 'Owner Occupier',
    COMMERCIAL_CLIENT: 'TRUE',
    COMM_FRAUD_INV: 'FALSE'
})

const tab = ref(null)
const name = ref("")


const resultado = ref()
const validar = async () => {
    console.log(datosUser.value)
    try {
        // const response = await fetch('http://localhost:8080/api/evaluate', {
        const response = await fetch('http://localhost:8080/api/evaluate'
            , {
                method: 'POST',
                headers: {
                    'Content-Type': 'application/json'
                },
                body: JSON.stringify(datosUser.value)
            }
        )
        const respuesta = await response.json()

        resultado.value = respuesta.respuesta.predictions[0].values[0][0]


        if (resultado.value == 1) {
            Swal.fire({
                title: 'Felicidades ' + name.value,
                text: "Tu credito esta pre-aprobado",
                icon: 'success',

            });
        } else {
            Swal.fire({
                title: 'Lo sentimos!!',
                text: "Contactate con nuestros asesores para solicitar tu credito",
                icon: 'warning',

            });

        }
        datosUser.value.INCOME = ""
        datosUser.value.YRS_AT_CURRENT_ADDRESS = ''
        datosUser.value.YRS_WITH_CURRENT_EMPLOYER = ''
        datosUser.value.NUMBER_OF_CARDS = ''
        datosUser.value.CREDITCARD_DEBT = ''
        datosUser.value.LOAN_AMOUNT = ''
        datosUser.value.CREDIT_SCORE = ''
        datosUser.value.PROPERTY_VALUE = ''
        datosUser.value.AREA_AVG_PRICE = ''
        datosUser.value.GENDER = ''
        datosUser.value.EDUCATION = ''
        datosUser.value.EMPLOYMENT_STATUS = ''
        datosUser.value.MARITAL_STATUS = ''
        datosUser.value.RESIDENCE = ''

        console.log(respuesta.respuesta.predictions[0].values[0][0])
    } catch (error) {
        console.error(error)
    }



}


const toggleTheme = () => theme.global.name.value = theme.global.current.value.dark ? 'light' : 'dark'

</script>

<style>
/* Helper classes */
.bg-basil {
    background-color: #FFFBE6 !important;
}

.text-basil {
    color: #1e9e19 !important;
}
</style>