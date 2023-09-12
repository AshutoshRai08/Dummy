<script setup lang="ts">
import { useHead } from '@vueuse/head'
import { Ref,reactive } from 'vue'
import packageJson from '../../package.json'
import { useDarkmode } from '/@src/stores/darkmode'
import VButtonVue, { VButtonColor } from '../components/base/button/VButton.vue'
import { type } from 'os'
import { boolean } from 'zod'
// import {useTable} from "./usePage.ts"

// const {loadRows,rowList} = useTable();
import { Field, Form, ErrorMessage,useField } from 'vee-validate';
import * as yup from 'yup';

const schema = yup.object({
  email: yup.string().email().required(),
  name: yup.string().required(),
  // selection: yup.string().required(),
});

function onSubmit(values) {
  alert(JSON.stringify(values, null, 2));
}
function saveInStorage(){
            localStorage.setItem("empDatabase",JSON.stringify(rows))
            // insert into empDatabase 
        }
       function loadFromStoragex(){
            const dataFromLocal = localStorage.getItem("empDatabase");
            // this.tableData = dataFromLocal === null ? ref([]) : dataFromLocal
            // select * from empDatabase
        }

type TabId = 'elements' | 'components' | 'forms' | 'plugins'
const activeTab = ref<TabId>('elements')
const darkmode = useDarkmode()
const router = useRouter()
import { ref } from 'vue'
import Modal from '../../elements/modal.vue'
import { ButtonHTMLAttributes } from 'vue'
import Button from '../../elements/button.vue'
// import { useResetForm } from 'vee-validate'
const smallFormOpen = ref(false)

const Emp=ref('')
const email_input=ref('')

const valueSingle1 = ref([])
const valueSingle = ref([])
const optionsSingle = ['Batman', 'Robin', 'Joker']
const optionsSingle1 = ['Batman', 'Robin', 'Joker','Batman1']

        const newData=ref('')
        const newData2=ref('')
        const newData3=ref('')
        const newData4=ref('')
// const columns = [
//         // {
//         //   label:'Sr No.',
//         //   field:'numberin',
//         //   type:'Boolean (default: false)',
//         // },

//       ];
      // const fixed-header=Boolean(default:false);
      function resetForm(){
      // props.modelValue==''
      // props.valueSingle==''
      newData2.value=''
      newData.value=''
      newData3.value=''
      newData4.value=''
      }
      type ROWS={
        name:string, 
        email:string,
        department:string,
        role:string
        // action?:
        
      }
      const rows:ROWS[] =reactive([
   
      
      ]);
      function abc(){
        rows.push({
           name:newData.value, email:newData2.value, department:newData3.value,role: newData4.value 
        }
        )
        resetForm()
          saveInStorage(rows)
      }
      type COLUMN={
       
        [key: string]: any; 
  
      }
     const columns:COLUMN=reactive([
        {
          label: 'Name',
          field: 'name',
        },
        {
          label: 'Email ID',
          field: 'email',
          type: 'string',
        },
        {
          label: 'Department',
          field: 'department',
          type: 'string',
          // dateInputFormat: 'yyyy-MM-dd',
          // dateOutputFormat: 'MMM do yy',
        },
        {
          label: 'Role',
          field: 'role',
          type: 'string',
        },
        {
          label:'Actions',
          field:'action ',
          type:'buttons'
        }
      ]);

//  const props=defineProps<{
//   modelValue: string,
//   valueSingle : string,
//   COLUMN:{
//         // name: string;
//         field:string,
//         [key: string]: any; 
  
//       }
//   columns:{
  
//     value:[
//         {
//           label: 'Name',
//           field: 'name',
//         },
//         {
//           label: 'Email ID',
//           field: 'email',
//           type: 'string',
//         },
//         {
//           label: 'Department',
//           field: 'department',
//           type: 'string',
//           // dateInputFormat: 'yyyy-MM-dd',
//           // dateOutputFormat: 'MMM do yy',
//         },
//         {
//           label: 'Role',
//           field: 'role',
//           type: 'string',
//         },
//         {
//           label:'Actions',
//           field:'action ',
//           type:'buttons'
//         }
//       ]
//   };

// }
// >()
// newData= props.modelValue
const emit = defineEmits<{
    (event: 'update:modelValue', payload: string): void;
}>();

</script>


    





<template>

    
  <div class="table-data">

        <div class="filters filters-autoflow section-box">
        
  <VField v-slot="{ id }" grouped class="is-autocomplete-select" p-b-10>
    <VControl v-slot="{ id }" expanded>
      <Multiselect
        v-model="valueSingle"
        :attrs="{ id }"
        :options="optionsSingle"
        placeholder="Search heroes..."
        :searchable="false"
      />
    </VControl>

    <VControl  class="hidden-touch" v-slot="{ id }" is-right expanded>
      <Multiselect
        v-model="valueSingle1"
        :attrs="{ id }"
        :options="optionsSingle1"
        placeholder="Search heroes..."
        :searchable="true"
      />
    </VControl>

  <VButton bold @click="smallFormOpen = true" color="primary" class="filters-pull-right hidden-touch"> Add Contact </VButton>
  <VModal
    is="form"
    :open="smallFormOpen"
    title="Leave a Comment"
    size="large"
    actions="right"
    @submit.prevent="smallFormOpen = false"
    @close="smallFormOpen = false"
  >
    <template #content>
      <Form @submit="abc();smallFormOpen = false" :validation-schema="schema" >
      <div class="modal-form" >
        
        <div class="field">
          
          <label>Emplyee Name *</label>
          <div class="control">
            <Field name="name"  placeholder="Username"  type="text" v-model="newData" style="width: 100%;"
            @input="emit('update:modelValue', ($event.target as HTMLInputElement).value)" />
            <ErrorMessage name="name" style="color: blue;" />
          </div>
          {{newData2}}
        
        </div>
        <div class="field">
          <label>Email ID *</label>
          <div class="control">
           
            <Field name="email" type="email"  placeholder="Email ID" v-model="newData2" style="width: 100%;"
            @input="emit('update:modelValue', ($event.target as HTMLInputElement).value)" />
            <ErrorMessage name="email" style="color: red;" />
            
          </div>
        </div>
        <div>
          <label>Role *</label>
          <VField v-slot="{ id }" class="is-autocomplete-select">
            <VControl expanded>
              <Multiselect
                name="selection"
                v-model="newData4"
                :attrs="{ id }"
                :options="optionsSingle1"
                placeholder="Search heroes..."
                :searchable="true"
              />
              <ErrorMessage name="select" style="color: red;" />
            </VControl>
          </VField>
        </div>
        <div>
          <label>Department *</label>
          <VField v-slot="{ id }" class="is-autocomplete-select">
            <VControl expanded>
              <Multiselect
                v-model="newData3"
                :disabled="newData4=='Batman'"
                :attrs="{ id }"
                :options="optionsSingle"
                placeholder="Search heroes..."
                :searchable="true"
                @select="emit('update:modelValue', ($event.target as HTMLInputElement).value)"
              />
            </VControl>
          </VField>
        </div>
      </div>
      <!-- <button style="color:rgb(25, 67, 25);padding:5px;background-color:green">Submit</button> -->
      <!-- <button type="button" @click="validate;abc();smallFormOpen">saving</button> -->
      <VButton type="submit" color="primary" raised @click="validate();abc();smallFormOpen = false">Save</VButton>
     </Form>
    </template>
  </VModal>
  
  </VField>
  </div>
  <div id="vuero-Tab" class="section-title has-text-centered">
    <vue-good-table
      :columns="columns"
      :rows=rows
      :line-numbers="true"
      :pagination-options="{
        enabled: true,
        perPage: 5
      }"
    >   <div slot="table-actions-bottom">
      <button>My Edits</button>
      Right window
    </div>
    <template slot="table-row" slot-scope="props">
      <span v-if="columns.field== 'action'">
        <button @click="editRow(props.row.id)">Edit</button>
        <button @click="deleteRow(props.row.id)">Delete</button>
      </span>
      <span v-else>
        {{rows[columns.field]}}
      </span>
    </template>
    

  

    </vue-good-table>
  </div>
</div>

</template>
<style lang="scss">
.multiselect {
  @media (max-width: 1366px) {
    width: 100%;
  }
}
</style>