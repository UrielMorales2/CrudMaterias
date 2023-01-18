<template>
  
    <section>
        <h3>Añadir Profesor</h3>
        <div><label for="">Nombre: </label><input type="text" v-model="teacher.teacherName"></div>
        <div><label for="">Apellidos: </label><input type="text" v-model="teacher.apellidos"></div>
        <div><label for="">NIF: </label><input type="text" v-model="teacher.nip"></div>
        <div><label for="">Materias: </label><input type="text" v-model="subjet"> <button @click="agregarMaterias()">Agregar</button></div>
        <div>
            <ul>
                <li v-for="( elm, index) in teacher.subjects" :key="index">{{ elm }}</li>
            </ul></div>
        <div><input type="checkbox" v-model="teacher.doc">Documentacion entregada</div>
        <button @click="agregrarTeacher()">Agregar</button>
    </section>

    <section>
        <h3>Listado de profesores</h3>
        <table>
            <tr>
                <th>Nombres</th>
                <th>apellidos</th>
                <th>nip</th>
                <th>Materias</th>
                <th>doccumentacion entregada</th>
            </tr>
            <tr v-for="elm in teachers" :key="elm.nip" >
                <th>{{ elm.teacherName }}</th>
                <th>{{ elm.apellidos }}</th>
                <th>{{ elm.nip }}</th>
                <th>
                    <ul>
                        <li v-for="(item, index) in elm.subjects" :key="index" >{{item}}</li>
                    </ul>
                </th>
                <th v-if="elm.doc">Entregado</th>
                <th v-else >No Entregado</th>
            </tr>
        </table>

    </section>
</template>


<script lang="ts" setup>
    import { Ref, ref } from 'vue';


    // el interface sirve para tipar los datos
    interface Iteacher{
        teacherName : string,
        apellidos : string,
        nip : string,
        subjects : Array<string>,
        doc : boolean
    }
    
    let teacher:Ref<Iteacher> = ref({
        teacherName : '',
        apellidos : '',
        nip : '',
        subjects : [],
        doc : ''
    });


    let teachers:Ref<Array<Iteacher>> = ref([]);


    let subjet :Ref<string> = ref('')


    const agregarMaterias = () => {
        teacher.value.subjects.push(subjet.value);
        subjet.value = " ";
    }
    
    const agregrarTeacher = () =>{
        teachers.value.push({
            teacherName : teacher.value.teacherName,
            apellidos : teacher.value.apellidos,
            nip : teacher.value.nip,
            subjects : teacher.value.subjects,
            doc   : teacher.value.doc,
        });
        limpiar();
    }
    
    const limpiar = () =>{
        teacher.value.teacherName=  " ";
        teacher.value.apellidos=  " ";
        teacher.value.nip=  " ";
        teacher.value.subjects=  [];
        teacher.value.doc=  false;
    }
    
    const hola = () =>{
        console.log("buenos dias" + teacher.value.subjects);
        
    }


</script>


<style scoped>

</style>