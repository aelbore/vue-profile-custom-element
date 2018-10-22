<template>
  <div id="app">
    <div class="container">
      <ar-input placeholder="Search Name"></ar-input>

      <div class="container">
        <div class="col-md-3" v-for="(item, index) in profiles" v-bind:key="index">
            <Card :profile='item'  />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Card from './components/Card.vue'
import { of } from 'rxjs';
import { debounceTime, distinctUntilChanged } from 'rxjs/operators';

const profiles = [
  {
    "name": "Arjay Elbore",
    "profession": "Framework Developer",
    "motto": "I never wanted to be famous, I wanted to be great."
  },
  {
    "name": "Aivan Monceller",
    "profession": "Developer",
    "motto": "When in doubt, iterate faster!"
  },
  {
    "name": "Christopher Lloyd",
    "profession": "UX Developer",
    "motto": "Genius is the ability to reduce the complicated to the simple."
  },
  {
    "name": "Martin Llaneza",
    "profession": "UI Developer",
    "motto": "The key to performance is elegance, not battalions of special cases."
  },
  {
    "name": "Melvin Vivas",
    "profession": "Manager - Solutions Engineering",
    "motto": "When in Doubt, Iterate Faster."
  },
  {
    "name": "Murali Pusuluri",
    "profession": "UI Developer",
    "motto": "To iterate is human, to recurse is divine."
  },
  {
    "name": "Nox Mendina",
    "profession": "Sr. Manager - Solutions Engineering",
    "motto": "When in doubt, iterate faster!"
  }
];

export default {
  name: 'app',
  created: function() {
    const self = this;
    self.profiles = profiles

    document.body.addEventListener('ar.change', function(e) {
      of(e.detail.value)
        .pipe(
          debounceTime(700),
          distinctUntilChanged()
        )
        .subscribe(text => {
          self.profiles = profiles.filter(profile => profile.name.toLowerCase().includes(text.toLowerCase()));
        })
    })
  },
  data() {
    return {
      profiles: []
    }
  },
  components: {
    Card
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 10px;
}
</style>
