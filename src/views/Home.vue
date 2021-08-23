<template>
<div>
  <v-toolbar dense dark color="indigo" class="pa-0">
     <v-img class="shrink mr-2" contain src="https://graphiste.com/blog/wp-content/uploads/2016/12/logo-todolist-4.png"
        transition="scale-transition" width="65"/>
    <v-toolbar-title class="flex text-center"><h1>To Do List</h1></v-toolbar-title>
    <v-img class="shrink mr-2" contain src="https://graphiste.com/blog/wp-content/uploads/2016/12/logo-todolist-4.png"
          transition="scale-transition" width="65"/>
  </v-toolbar>
  <v-container>
    <v-row>
      <v-col col="12" >
        <v-text-field single-line solo placeholder="Ecrire ici pour ajouter une tâche." v-model="tache_ajout"></v-text-field>
        <v-btn dark color="indigo" v-on:click="add">Cliquer ici pour l'ajouter</v-btn>
      </v-col>
    </v-row>
    <v-row v-if="liste_tache.length!=0">
      <v-col col="12">
        <v-simple-table fixed-header dense>
          <thead>
            <tr>
              <th class="indigo--text text-center">DESCRIPTION</th>
              <th class="indigo--text text-center" >VALIDATION(cliquer sur l'élément souligné)</th>
              <th class="indigo--text text-center">MODIFICATION</th>
              <th class="indigo--text text-center">SUPPRESSION</th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="(item,key) in liste_tache" v-bind:key="item.descritpion">
              <td><b>{{ item.description }}</b></td>
              <td class="text-center text-decoration-underline"><b v-on:click="validate(key)" v-if="liste_tache[key].validation== valid" class="green--text">{{ item.validation }}</b><b v-on:click="validate(key)" class="red--text" v-else>Pas exécutée</b></td>
              <td class="text-center"><b><v-btn color="white white--text" v-on:click="update(key)">
                <v-img class="shrink mr-2" contain src="https://p.kindpng.com/picc/s/154-1541056_edit-edit-icon-svg-hd-png-download.png"
                  transition="scale-transition" width="25"/></v-btn></b></td>
              <td class="indigo--text text-center"><b><v-btn color="white white--text" v-on:click="remove(key)">
                <v-img class="shrink mr-2" contain src="https://media.istockphoto.com/vectors/trash-can-icon-logo-template-illustration-design-vector-eps-10-vector-id1223505692?k=6&m=1223505692&s=612x612&w=0&h=2VAEjHYfLRfeJG3wtPFRfW-bl990Y9CNtm6yhpyU9OU="
                  transition="scale-transition" width="35"/></v-btn></b></td>
            </tr>
          </tbody>
        </v-simple-table>
      </v-col>
    </v-row>
    <v-row v-else>
      <v-col col="12" >
        <h1 class="brown--text">La liste des tâches est vide.</h1>
        <center>
        <v-img class="shrink mr-2" contain src="https://png.pngtree.com/png-vector/20190622/ourlarge/pngtree-checklistcheckexpertiselistclipboard-flat-color-icon-vec-png-image_1490531.jpg" 
            transition="scale-transition"
            width="450"/>
        </center>
      </v-col>
    </v-row>
  </v-container>
</div>
</template>

<script>
export default {
  name: "Home",
  data(){ 
    return{
      liste_tache:[],
      tache_ajout:"",
      valid:"Exécutée"
    }
  },
  methods:{
    add: function () {
      var t={ description:"",validation: ""};
      var flag=0;

      for (var item in this.liste_tache){
        if(this.liste_tache[item].description==this.tache_ajout){
          flag=1;
        }
      }
      if(flag==1){
        window.alert("la tâche est déjà inscrite dans la liste !!");
      }else{
        if(this.tache_ajout.length > 0){
          t.description=this.tache_ajout;
          this.liste_tache.push(t);
        }else{
          window.alert("Vous n'avez rien écrit !!");
        }
      }
      this.tache_ajout="";
    },
    remove: function (index) {
      this.liste_tache.splice(index,1);
      this.validation.splice(index,1);
    },
    update: function (index) {
      var tache_up=prompt("Modifier la tâche","");
      var flag=0;

      for (var item in this.liste_tache){
        if(this.liste_tache[item].description==tache_up){
            flag=1;
        }
      }
      if(flag==1){
        window.alert("la tâche est déjà inscrite dans la liste !!");
      }else{
        if(tache_up.length>0){
          this.liste_tache[index].description=tache_up;
          this.liste_tache[index].validation="";
        }else{
          window.alert("Vous n'avez rien écrit !!");
        }
      }
    },
    validate: function(index){
      if(this.liste_tache[index].validation=="Exécutée"){
        this.liste_tache[index].validation="";
      }else{
        this.liste_tache[index].validation="Exécutée";
      }
    }
  }
}
</script>
