<template>
  <div>
    <div class="row">
        <div class="col md-6">
          <h1>Formulario</h1>
          <form @submit.prevent>
            <div class="form-group">
              <label for="nombre">Nombre</label>
              <span v-if="!nombre"> Requerido*</span>
              <input type="text" id="nombre" class="form-control" v-model="nombre" @blur="validarName">
              <span class="text-danger" v-if="notAnumber"> Formato incorrecto</span>
            </div>
            <div class="form-group">
              <label for="telephone">Telephone</label>
              <span v-if="!telephone"> Requerido*</span>
              <span v-if="isAnumber"> Formato incorrecto</span>
              <input type="text" id="telephone" class="form-control" v-model="telephone" @blur="validarTel">
            </div>
            <div class="form-group">
              <label for="cp">CP</label>
              <span v-if="!cp"> Requerido*</span>
              <input type="text" id="cp" class="form-control" v-model="cp" @blur="validarCP">
              <span v-if="cpControl"> Formato incorrecto</span>
            </div>
            <div class="form-group">
              <label for="email">Email</label>
              <span v-if="!correo"> Requerido*</span>
              <span v-if="alto"> Formato incorrecto</span>
              <input type="email" id="email" class="form-control" v-model="correo" @blur="validarEmail">
            </div>
            <div class="form-group">
              <label for="contrasena">Contraseña</label>
              <span v-if="!contrasena"> Requerido*</span>
              <span v-if="pass"> Formato incorrecto</span>
              <input type="password" id="contrasena" class="form-control" v-model="contrasena" @blur="validarPassword">
            </div>
            <div class="form-group">
              <label for="contrasena2">Repetir Contraseña</label>
              <span v-if="!contrasena2"> Requerido*</span>
              <span v-if="pass2"> Formato incorrecto</span>
              <input type="password" id="contrasena2" class="form-control" v-model="contrasena2" @blur="validarPassword2">
            </div>
            <button type="submit" class="btn btn-primary btn-lg ml-2" onclick="registerValidate()">Enviar</button>
          </form>
        </div>
      </div>
  </div>
</template>

<script>
export default {
  name: 'Formulari',
  props: {
    msg: String
  },
  data() {
      return{
        nombre: "",
        telephone: "",
        cp: "",
        correo: "",
        contrasena: "",
        contrasena2: "",
        alto: "",
        notAnumber: "",
        isAnumber: "",
        cpControl: "",
        pass: "",
        pass2: ""
      }
    },
    methods: {
        validarEmail: function(){
            var texto = this.correo;
            var arroba = texto.indexOf("@");
            var punto = texto.indexOf(".");
            if (arroba == -1 || punto ==-1){
                this.alto = true;
            }else{
                this.alto = false;
            }
        },
        validarName: function(){
            if (this.nombre.match(/^[A-Za-z]{6,13}$/)) {
                this.notAnumber = false;
            }else if(this.nombre.match(/[^A-Za-z]/g)) {
                this.notAnumber = true;
            }else{
                this.notAnumber = true;
            }
        },
        validarTel: function(){
            if(this.telephone.match(/[^0-9]/g)){
                this.isAnumber = true;
            }else{
                this.isAnumber = false;
            }
        },
        validarCP: function () {  
            if(this.cp.match(/[^0-9]/g)){
                this.cpControl = false;
            }else if(this.cp.match(/^[0-9]{5,5}$/gm)){
                this.cpControl = false;
            }else{
                this.cpControl = true;
            }
        },
        validarPassword: function(){
            if(this.contrasena.match(/^(?=.*[a-z])(?=.*[A-Z])[A-Za-z\d$@ñ!%*?&+¿_]{6,13}$/)){
                this.pass = false;
            }else{
                this.pass = true;
            }
        },
        validarPassword2: function () { 
            if(this.contrasena == this.contrasena2){
                this.pass2 = false;
            }else{
                this.pass2 = true;
            }
            }
         }
    }

</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
