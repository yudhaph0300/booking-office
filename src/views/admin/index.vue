<template>
  <div class="container">
    <h1 class="text-center mb-10">Office List</h1>

    <!-- Start Dialog Add Data -->
    <div class="ml-10">
        <v-dialog
        v-model="dialogAdd"
        persistent
        max-width="800px"
        >
        <template v-slot:activator="{ on, attrs }">
            <v-btn
            color="primary"
            dark
            v-bind="attrs"
            v-on="on"
            >
            Add Office
            </v-btn>
        </template>
        <v-card>
            <v-card-title>
            <span class="text-h5">Add Data Office</span>
            </v-card-title>
            <v-card-text>
            <v-container>
                <v-row>
                <v-col cols="12">
                    <v-text-field
                    label="Name"
                    v-model="formAdd.name"
                    required
                    ></v-text-field>
                </v-col>

                <v-col cols="12">
                    <v-text-field
                    label="Location"
                    v-model="formAdd.location"
                    required
                    ></v-text-field>
                </v-col>

                <v-col cols="6">
                    <v-text-field
                    label="Capacity"
                    v-model="formAdd.capacity"
                    required
                    ></v-text-field>
                </v-col>

                <v-col cols="6">
                    <v-text-field
                    label="Price"
                    v-model="formAdd.price"
                    required
                    ></v-text-field>
                </v-col>

                <v-col cols="12">
                    <v-textarea
                    outlined
                    label="Description"
                    v-model="formAdd.description"
                    required
                    ></v-textarea>
                </v-col>
                
                </v-row>
                
            </v-container>
            </v-card-text>
            <v-card-actions>
            <v-spacer></v-spacer>
            <v-btn
                
                @click="dialogAdd = false"
            >
                Cancel
            </v-btn>
            <v-btn
                color="primary"
                @click="addOffice"
            >
                Add Data
            </v-btn>
            </v-card-actions>
        </v-card>
        </v-dialog>
    </div>
    <!-- End Dialog Add Data -->

    <!-- Start Dialog Edit Data -->
    <div class="">
        <v-dialog
        v-model="dialogEdit"
        persistent
        max-width="800px"
        >
        <v-card>
            <v-card-title>
            <span class="text-h5">Edit Data Office</span>
            </v-card-title>
            <v-card-text>
            <v-container>
                <v-row>
                <v-col cols="12">
                    <v-text-field
                    label="Name"
                    v-model="formEdit.name"
                    required
                    ></v-text-field>
                </v-col>

                <v-col cols="12">
                    <v-text-field
                    label="Location"
                    v-model="formEdit.location"
                    required
                    ></v-text-field>
                </v-col>

                <v-col cols="6">
                    <v-text-field
                    label="Capacity"
                    v-model="formEdit.capacity"
                    required
                    ></v-text-field>
                </v-col>

                <v-col cols="6">
                    <v-text-field
                    label="Price"
                    v-model="formEdit.price"
                    required
                    ></v-text-field>
                </v-col>

                <v-col cols="12">
                    <v-textarea
                    outlined
                    label="Description"
                    v-model="formEdit.description"
                    required
                    ></v-textarea>
                </v-col>
                
                </v-row>
                
            </v-container>
            </v-card-text>
            <v-card-actions>
            <v-spacer></v-spacer>
            <v-btn
                
                @click="dialogEdit = false"
            >
                Cancel
            </v-btn>
            <v-btn
                color="primary"
                @click="updateOffice()"
            >
                Edit Data
            </v-btn>
            </v-card-actions>
        </v-card>
        </v-dialog>
    </div>
    <!-- End Dialog Add Data -->
    

    
    <v-simple-table class="mx-10">
        <template v-slot:default>
        <thead>
            <tr>
            <th class="text-left">
                Id
            </th>
            <th class="text-left">
                Name
            </th>
            <th class="text-left">
                Location
            </th>
            <th class="text-left">
                Capacity
            </th>
            <th class="text-left">
                Price
            </th>
            <th class="text-left">
                Description
            </th>
            <th class="text-center">
                Action
            </th>
            </tr>
        </thead>
        <tbody>
            <tr
            v-for="office in offices"
            :key="office.id"
            >
                <td>{{ office.id }}</td>
                <td>{{ office.name }}</td>
                <td>{{ office.location }}</td>
                <td>{{ office.capacity }}</td>
                <td>{{ office.price }}</td>
                <td width="35%">{{ office.description }}</td>
                <td class="text-center mx-auto">
                    
                    <v-btn
                    width="40%"
                    class="mx-1"
                    dark
                    color="green"
                    @click="modeEdit(office.id)"
                    >
                        Edit
                    </v-btn>

                    <v-btn
                    width="40%"
                    class="mx-1"
                    dark
                    color="red lighen-4"
                    @click="deleteOffice(office.id)"
                    >
                        Delete
                    </v-btn>
                </td>
            </tr>
        </tbody>
        </template>
    </v-simple-table>
  </div>
</template>

<script>
import axios from 'axios'
export default {
    name: 'HomeAdmin',
    data() {
        return {
            offices: [],
            dialogAdd: false,
            dialogEdit: false,
            indexId: null,
            formAdd: {
                name: '',
                location: '',
                capacity: null,
                price: null,
                description: ''
            },
            formEdit: {
                name: '',
                location: '',
                capacity: null,
                price: null,
                description: ''
            }
        }
    },
    async mounted() {
        this.load()
    },
    methods: {
        async load() {
            const response = await axios.get(`http://localhost:3000/office`)
            this.offices = response.data
        },
        async addOffice() {
            try {
                await axios.post(`http://localhost:3000/office`, this.formAdd)
                this.load()
                this.formAdd.name = ''
                this.formAdd.location = ''
                this.formAdd.capacity = null
                this.formAdd.price = null
                this.formAdd.description = ''
                this.dialogAdd = false
            } catch (error) {
                console.log(error)
                this.dialogAdd = false
            }
        },
        async deleteOffice(id) {
            await axios.delete(`http://localhost:3000/office/`+id)
            this.load()
        },
        modeEdit(id){
            this.indexId = id
            this.dialogEdit = true
        },
        async updateOffice() {

            try {
                await axios.put(`http://localhost:3000/office/`+this.indexId, {
                name: this.formEdit.name,
                location: this.formEdit.location,
                capacity: this.formEdit.capacity,
                price: this.formEdit.price,
                description: this.formEdit.description })

                this.load()
                this.dialogEdit = false
                this.formEdit.name = ''
                this.formEdit.location = ''
                this.formEdit.capacity = null
                this.formEdit.price = null
                this.formEdit.description = ''    
            } catch (error) {
                console.log(error)    
            }


            
            
        }
    }

}
</script>

<style>

</style>