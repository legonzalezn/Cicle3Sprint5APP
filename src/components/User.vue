<template>
    <div id="User">
        <h2>
            <table>
                <tr>
                    <td>Numero de documento:</td>
                    <td>{{userData.per_numero}}</td>
                </tr>
                <tr>
                    <td>Primer nombre:</td>
                    <td>{{userData.per_nombre1}}</td>
                </tr>
                <tr>
                    <td>Segundo nombre:</td>
                    <td>{{userData.per_nombre2}}</td>
                </tr>
                <tr>
                    <td>Primer apellido:</td>
                    <td>{{userData.per_apellido1}}</td>
                </tr>
                <tr>
                    <td>Segundo apellido:</td>
                    <td>{{userData.per_apellido2}}</td>
                </tr>
                <tr>
                    <td>Numero de telefono:</td>
                    <td>{{userData.per_numero_contacto}}</td>
                </tr>
                <tr>
                    <td>Direccion de residencia:</td>
                    <td>{{userData.per_direccion}}</td>
                </tr>
                <tr>
                    <td>Fecha de nacimiento:</td>
                    <td>{{userData.per_fecha_nacimiento}}</td>
                </tr>
                <tr>
                    <td>Registrado desde:</td>
                    <td>{{userData.per_creado}}</td>
                </tr>
            </table>
        </h2>
    </div>
</template>



<script>

import axios from "axios";
    export default {
        name: "User",
        data:function(){
            return {
                username: "none",
                id: 0,
                userData: {}
            }
        },
        created: function () {
            console.log(this.$route.params)
            this.username = this.$route.params.userData.username
            this.id = this.$route.params.userData.id
            axios.get(`http://cicle3sprint4unal.herokuapp.com/user/${this.id}`)
                .then(info => {
                    console.log(info)
                    this.userData = info.data
                })
        }
    }
</script>

    


<style>
    #User{
        width: 100%;
        height: 100%;

        display: flex;
        justify-content: center;    
        align-items: center;
    }

    #User h2{
        font-size: 50px;
        color: #283747;
    }

    #User span{
        color: crimson;
        font-weight: bold;
    }
</style>