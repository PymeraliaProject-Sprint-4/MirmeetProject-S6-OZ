<!-- Codi de la pagina -->
<template>
  <div style="width: 500px;" class="white-container">

    <div class="perfil-container">
      <img class="img-perfil" v-if="perfil.avatar" :src="'/storage/perfil/' + perfil.avatar" style="display: block; margin: 0 auto; max-width: 100%;" />
    <div class="perfil-text">
      <p id ="nameUser" v-if="perfil.length == perfil.length">{{ perfil.username}}</p>
      <p v-if="perfil.length == perfil.length">{{ perfil.bibliografy}}</p>
    </div>
  </div>
    <div style="width: 500px; display: flex; align-items: center;">

      <div v-if="this.me.username != this.perfil.username">

        <button class="botoFollow" @click="handleClick">
          {{ isClicked ? 'unFollow' : 'Follow' }}
        </button>
      </div>

      <div style="display: inline-block;">
        <div class="contador" style="display: inline-block; padding-right: 30px; padding-left: 50px;">
          <h2>Publicaciones</h2>
          <p v-if="userPublications.length > 0">{{ userPublications[0].publicationsammount }}</p>
        </div>
        <div class="contador" style="display: inline-block; padding-right: 30px;">
          <h2>Seguidores</h2>
          <p v-if="followers.length > 0">{{ followers[0].followersammount }}</p>
        </div>
        <div class="contador" style="display: inline-block;">
          <h2>Siguiendo</h2>
          <p v-if="following.length > 0">{{ following[0].followingammount }}</p>
        </div>
      </div>

    </div>
    <div v-if="this.me.id == this.perfil.id">
    <button class="botoConfiguracio" @click="modal(perfil)">
      Configuracion
    </button>
    </div>
    <div v-show="configuracioModal" class="modal ">
      <div class="modal-content">
        <div class="relative">
          <p class="ml-2 flex text-base font-semibold leading-6 text-gray-900">
            Editar Perfil
          </p>
          <form method="POST" v-on:submit.prevent="configPerfil()" enctype="multipart/form-data">

            <div hidden>
              @csrf
            </div>
            <div class="sm:items-start">
            <div class="mt-3 text-center sm:mt-0 sm:mx-1 sm:text-left">
            <div>
            <input type="hidden" v-model="id" id="id" name="id" required
              class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-600 dark:border-gray-500 dark:placeholder-gray-400 dark:text-white">
            </div>
            <div>
              <label for="name"
                class="block mb-2 text-sm font-medium text-gray-900 dark:text-white">Nombre</label>
              <input type="text" v-model="username" id="username" name="username" required
                class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-600 dark:border-gray-500 dark:placeholder-gray-400 dark:text-white">
            </div>
            <div>
              <label for="description"
                class="block mb-2 text-sm font-medium text-gray-900 dark:text-white">Biografia</label>
              <input type="text" v-model="bibliografy" id="bibliografy" name="bibliografy" required
                class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-600 dark:border-gray-500 dark:placeholder-gray-400 dark:text-white">
            </div>
            <div>
              <label for="image"
                class="block mb-2 text-sm font-medium text-gray-900 dark:text-white">Imagen Perfil</label>
              <input type="file" v-on:change="avatar" id="avatar" name="avatar" required
                class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-600 dark:border-gray-500 dark:placeholder-gray-400 dark:text-white">
            </div>
            </div>
            </div>

            <div class="flex items-center">
              <button class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded-lg" type="submit">
                Guardar cambios
              </button>
            </div>
          </form>
        </div>
      </div>

    </div>

  </div>
</template>


<!-- Estils per a esta vista -->
<style scoped>

.white-container {
  background-color: #fff;
  border-radius: 20px;
  padding: 20px;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.2);
}

#nameUser{
  font-weight: bold;
  font-size: 27px;
}
.perfil-container {
  display: flex;
  align-items: center;
  margin-right: 20px;
}
.perfil-text {
  margin-left: 20px;
}

.modal {
  position: fixed;
  z-index: 1;
  left: 0;
  top: 0;
  width: 100%;
  height: 100%;
  overflow: auto;
  background-color: rgba(0, 0, 0, 0.5);
  display: flex;
  align-items: center;
  justify-content: center;
}

.modal-content {
  background-color: white;
  padding: 20px;
  border-radius: 5px;
  box-shadow: 0px 5px 10px rgba(0, 0, 0, 0.5);
}

.relative {
  position: relative;
}

.img-perfil {
  width: 30%;
  border-radius: 50%;
}

.botoFollow {
  background-color: blue;
  color: white;
  border: none;
  padding: 10px 20px;
  border-radius: 5px;
  cursor: pointer;
}

.botoConfiguracio {
  background-color: blue;
  color: white;
  border: none;
  padding: 10px 20px;
  border-radius: 5px;
  cursor: pointer;
  width: 95%
}

.contador {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  margin-bottom: 10%;
  margin-top: 10%;
}

.contador h2 {
  margin: 0;
  font-size: 18px;
  font-weight: bold;
}

.contador p {
  margin: 0;
  font-size: 16px;
  font-weight: bold;
}
</style>

<!-- Scripts per a esta vista -->




<script>

// Importem la llibreria axios per a fer peticions HTTP
import axios from 'axios';

export default {
  data() {
    return {
      isClicked: false,
      confirm: null,
      idfollowing: 0,
      followers: 0,
      following: 0,
      userPublications: 0,
      perfil: {},
      me: {},
      configuracioModal: false,
      id: '',
      username:'',
      bibliografy:'',
      avatar:'',
    };
  },

  mounted() {
    this.getPublications();
    this.getFollowers();
    this.getFollowing();
    this.getPerfil();
    this.getMe();
  },

  methods: {
    getPerfil() {
      let user = window.location.pathname.split('/').pop()
      axios.get('/perfil/' + user + '/recuperar')
        .then(response => {
          this.perfil = response.data
          console.log(this.perfil);
        })
        .catch(error => {
          console.log(error)
        })
    },
    getMe() {
      let id = window.location.pathname.split('/').pop()
      axios.get('/me')
        .then(response => {
          this.me = response.data
        })
        .catch(error => {
          console.log(error)
        })
    },
    getFollowers() {
      let user = window.location.pathname.split('/').pop()
      axios.get('/perfil/' + user + '/get-followers')

        .then(response => {
          this.followers = response.data;
          this.getFollowers();
          console.log(this.followers);
        })
        .catch(error => {
          console.log(error);
        });
    },

    getFollowing() {
      let user = window.location.pathname.split('/').pop()
      axios.get('/perfil/' + user + '/get-following')

        .then(response => {
          this.following = response.data;
          this.getFollowing();
          console.log(this.following);
        })
        .catch(error => {
          console.log(error);
        });
    },


    getPublications() {
      let user = window.location.pathname.split('/').pop()
      axios.get('/perfil/' + user + '/get-publications')

        .then(response => {
          this.userPublications = response.data;
          console.log(this.this.userPublications);
        })
        .catch(error => {
          console.log(error);
        });
    },

    handleClick() {
      this.isClicked = !this.isClicked;

      // Si el botón está activado (isClicked == true), hacemos la petición POST
      if (this.isClicked) {
        axios.post('/follower', {
          idFollower: this.idfollower,
          idFollowing: this.perfil.id,
        })
          .then((response) => {
            console.log(idFollowing);
            this.confirm = response.data;
          })
          .catch((error) => {
            console.log(error);
          });
      }
      // Si el botón no está activado (isClicked == false), hacemos la petición PUT
      else {
        axios.put(`/following`, {
          idFollower: this.idfollower,
          idFollowing: this.perfil.id,
        })

          .then((response) => {
            console.log(response);
          })
          .catch((error) => {
            console.log(error);
          });
      }
    },
    modal(perfil) {
    this.configuracioModal = true;
    this.id = perfil.id
    this.username = perfil.username;
    this.bibliografy = perfil.bibliografy;
    this.avatar = perfil.avatar;
    },

    configPerfil() {

      const id = document.getElementById('id').value;
      const username = document.getElementById('username').value;
      const bibliografy = document.getElementById('bibliografy').value;
      const avatar = document.getElementById('avatar').files[0];
      console.log(id);

      const data = new FormData();
      data.append('id', id);
      data.append('username', username);
      data.append('bibliografy', bibliografy);
      data.append('avatar', avatar);

      axios.post('/perfil/configuracio', data)
        .then(response => {
          this.getPerfil();
          console.log(response.data)
        })
        .catch(error => {
          console.log(response.data)
        });
      },
  },

  }
</script>
