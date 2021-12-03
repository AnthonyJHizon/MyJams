<template>
  <div>
    <Navbar />
    <div id="container">
      <div id="preferences-container">
        <ul id="preferences-list">
          <li v-for="preference in local_preferences" :key="preference.id">
            <div class="preference">
              <h2>{{ preference.name }}</h2>
              <img v-if="deletePreference" src="../static/xbutton.png" @click="handleDelete(preference.id)">
            </div>
          </li>
        </ul>
        <div id="preferences-buttons-container">
          <NuxtLink to="/questionnaire">
            <button class="preferences-buttons">
              Add
            </button>
          </NuxtLink>
          <button v-if="local_preferences.length !== 0" class="preferences-buttons" @click="deletePreference = !deletePreference">
            <p v-if="!deletePreference">
              Delete
            </p>
            <p v-else>
              Back
            </p>
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Navbar from '../components/Navbar'

export default {
  Navbar,
  props: {
    preferences: {
      type: Array,
      default () {
        return []
      }
    }
  },
  data () {
    return {
      deletePreference: false,
      local_preferences: this.preferences
    }
  },
  created () {
    this.local_preferences = [
      {
        id: '1',
        name: 'hello'
      },
      {
        id: '2',
        name: 'rock'
      },
      {
        id: '3',
        name: 'hiphop'
      }
    ]
  },
  methods: {
    handleDelete (id) {
      const index = this.local_preferences.findIndex(pref => pref.id === id)
      if (index > -1) {
        this.local_preferences.splice(index, 1)
      }
    }
  }
}
</script>

<style>
* {
  padding: 0px;
  margin: 0px;
}

.preference {
  display: flex;
  align-items: center;
  height: 128px;
  width: 512px;
  border-radius: 8px;
  overflow: hidden;
  background: white;
  box-shadow: rgba(60, 64, 67, 0.3) 0px 1px 2px 0px, rgba(60, 64, 67, 0.15) 0px 2px 6px 2px;
}

.preference h2 {
  display: inline-block;
  width: 380px;
  overflow: hidden;
  white-space: nowrap;
  text-overflow: ellipsis;
  color: black;
  padding: 0 32px;
}

.preference img {
  cursor: pointer;
}

.preferences-buttons {
  cursor: pointer;
  width: 200px;
  height: 50px;
  margin: 10px;
}

#container {
  display: flex;
  justify-content: center;
  width: 100%;
  height: 100vh;
  font-family: "Montserrat", sans-serif;
  background: rgb(255,255,255);
  background: -moz-radial-gradient(circle, rgba(255,255,255,1) 17%, rgba(246,246,246,1) 40%, rgba(235,235,235,1) 100%);
  background: -webkit-radial-gradient(circle, rgba(255,255,255,1) 17%, rgba(246,246,246,1) 40%, rgba(235,235,235,1) 100%);
  background: radial-gradient(circle, rgba(255,255,255,1) 17%, rgba(246,246,246,1) 40%, rgba(235,235,235,1) 100%);
  filter: progid:DXImageTransform.Microsoft.gradient(startColorstr="#ffffff",endColorstr="#ebebeb",GradientType=1);
}

#preferences-container {
  display: flex;
  flex-direction: column;
  align-items: center;
  width: 1000px;
  margin-top: 82px;
}

#preferences-list {
  list-style: none;
}

#preferences-list li {
  margin: 32px 52px;
}
</style>