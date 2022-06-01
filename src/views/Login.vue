<template>
    <v-row>
        <v-col class="pr-0 pb-0">
            <v-img width="100%" src="../assets/img/background.png"/>
        </v-col>
        <v-col class="pl-0">
            <v-card class="ma-16" flat>
                <v-card-text class="text-center">
                    Masuk
                </v-card-text>

                <v-card-text class="pa-0">
                    Email
                </v-card-text>
                <v-text-field
                 outlined
                 placeholder="Masukan email anda"
                />

                <v-card-text class="pa-0">
                    Kata Sandi
                </v-card-text>
                <v-text-field
                 outlined
                 placeholder="Masukan kata sandi anda"
                />

                <v-row>
                    <v-col class="text-left py-0">
                        <v-checkbox
                        class="my-0 py-0"
                        color="green"
                        >
                            <template v-slot:label>
                                <div>
                                    Simpan Kata Sandi
                                </div>
                            </template>
                        </v-checkbox>
                    </v-col>
                    <v-col class="text-right py-0">
                        <a href="#">Lupa kata sandi ?</a>
                    </v-col>
                </v-row>

                <v-row>
                    <v-col class="text-center">
                        <v-btn
                         color="#606FAA"
                         dark
                         class="px-10"
                        >
                            Masuk
                        </v-btn>
                    </v-col>
                </v-row>

                <v-card-text class="text-center">
                    atau
                </v-card-text>

                <v-card-text class="text-center">
                    Belum punya akun ? <a href="/register">Daftar</a>
                </v-card-text>
                
                
            </v-card>
        </v-col>
    </v-row>
</template>

<script>
export default {
    name: 'LoginPage'
}
</script>

<style>

</style>