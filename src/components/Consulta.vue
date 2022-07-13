<template>
    <v-layout style="z-index: 0">
        <v-app-bar>
            <v-avatar>
                <v-img src="/seabanck.png" alt="John"></v-img>
            </v-avatar>
            <v-app-bar-title class="text-h4 mx-4" style="color:#424242;">SeaBanck</v-app-bar-title>
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
                    <v-col md="6" class="px-5">
                        <h2 class="text-h2" style="color:#424242;">Haz realidad el sueno de la casa propia</h2>
                        <p class="text-h4 font-weight-light text-medium-emphasis my-10">
                            El levantamiento de hipoteca es un proceso que se debe seguir luego de haber pagado el total
                            de las cuotas de tu crédito hipotecario para certificar que tu inmueble está libre de
                            hipoteca.
                        </p>
                        <p class="text-h4 font-weight-light text-medium-emphasis my-10">
                            El levantamiento de hipoteca es un proceso que se debe seguir luego de haber pagado el total
                            de las cuotas de tu crédito hipotecario para certificar que tu inmueble está libre de
                            hipoteca.
                        </p>
                    </v-col>
                    <v-col md="6" sm="6" cols="12">
                        <h2 class="text-h2" style="color:#424242;">Evaluacion de credito</h2>
                        <h2 class="text-button" style="color:#424242;">Datos pernales</h2>
                        <v-divider></v-divider>
                        <br>
                        <v-row>
                            <v-col>
                                <v-select :items="GENDER" v-model="datosUser.GENDER" label="Genero" variant="outlined">
                                </v-select>
                            </v-col>
                            <v-col>
                                <v-select :items="MARITAL_STATUS" v-model="datosUser.MARITAL_STATUS"
                                    label="Estado civil" variant="outlined">
                                </v-select>
                            </v-col>
                            <v-col>
                                <v-select :items="EDUCATION" v-model="datosUser.EDUCATION" label="Educacion"
                                    variant="outlined">
                                </v-select>
                            </v-col>
                        </v-row>
                        <h2 class="text-button" style="color:#424242;">Datos recidenciales</h2>
                        <v-divider></v-divider>
                        <br>
                        <v-row>
                            <v-col>
                                <v-select :items="RESIDENCE" v-model="datosUser.RESIDENCE" label="Residencia"
                                    variant="outlined">
                                </v-select>
                            </v-col>
                            <v-col>
                                <v-text-field label="Anos en su vivienda actual" variant="outlined" type="number"
                                    v-model="datosUser.YRS_AT_CURRENT_ADDRESS"></v-text-field>
                            </v-col>
                        </v-row>
                        <v-row>
                            <v-col>
                                <v-text-field label="Valor de la propiedad" variant="outlined"
                                    v-model="datosUser.PROPERTY_VALUE"></v-text-field>
                            </v-col>
                            <v-col>
                                <v-text-field label="Precio promedio del area" variant="outlined"
                                    v-model="datosUser.AREA_AVG_PRICE"></v-text-field>
                            </v-col>
                        </v-row>
                        <h2 class="text-button" style="color:#424242;">Datos laborales</h2>
                        <v-divider></v-divider>
                        <br>
                        <v-row>
                            <v-col>
                                <v-select :items="EMPLOYMENT_STATUS" v-model="datosUser.EMPLOYMENT_STATUS"
                                    label="Estado laboral" variant="outlined">
                                </v-select>
                            </v-col>
                            <v-col>
                                <v-text-field label="Ingresos" variant="outlined" v-model="datosUser.INCOME">
                                </v-text-field>
                            </v-col>
                            <v-col>
                                <v-text-field label="Anos de experiencia laboral" variant="outlined"
                                    v-model="datosUser.YRS_WITH_CURRENT_EMPLOYER" type="number"></v-text-field>
                            </v-col>
                        </v-row>

                        <h2 class="text-button" style="color:#424242;">Datos del credito</h2>
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
                                <v-text-field label="Monto de prestamos soliicitado" variant="outlined"
                                    v-model="datosUser.LOAN_AMOUNT" type="number"></v-text-field>
                            </v-col>
                        </v-row>

                        <v-row>
                            <v-col>
                                <v-text-field label="Record crediticio" variant="outlined"
                                    v-model="datosUser.CREDIT_SCORE" type="number"></v-text-field>
                            </v-col>
                            <v-col>
                                <v-text-field label="Creditos vigentes" variant="outlined" v-model="datosUser.LOANS"
                                    type="number">
                                </v-text-field>
                            </v-col>
                        </v-row>
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
const theme = useTheme()

const GENDER = ['Male', 'Female']
const EMPLOYMENT_STATUS = ['Employed', 'Medical Leave', 'Retired', 'Disabled', 'Unemployed']
const MARITAL_STATUS = ['Married', 'Divorced', 'Single']
const RESIDENCE = ["Owner Occupier", "Public Housing", "Private Renting", "Living with parents/guardian", "Sheltered"]
const EDUCATION = ["High School or Below", "Bachelor", "College", "Master", "Doctor"]

const datosUser = ref({
    INCOME: '',
    YRS_AT_CURRENT_ADDRESS: '',
    YRS_WITH_CURRENT_EMPLOYER: '',
    NUMBER_OF_CARDS: '',
    CREDITCARD_DEBT: '',
    LOAN_AMOUNT: '',
    CREDIT_SCORE: '',
    PROPERTY_VALUE: '',
    AREA_AVG_PRICE: '',
    LOANS: '',
    GENDER: '',
    EDUCATION: '',
    EMPLOYMENT_STATUS: '',
    MARITAL_STATUS: '',
    APPLIEDONLINE: 'YES',
    RESIDENCE: '',
    COMMERCIAL_CLIENT: 'TRUE',
    COMM_FRAUD_INV: 'FALSE'
})

const validar = () => {
    console.log(datosUser.value)

    const response = fetch('http://localhost:3030/api/evaluate', {
        method: 'POST',
        headers: {
            'Content-Type': 'application/json'
        },
        body:  JSON.stringify(datosUser.value) 
    })

    console.log(response)
}


const toggleTheme = () => theme.global.name.value = theme.global.current.value.dark ? 'light' : 'dark'

</script>