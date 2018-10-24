<template>
  <div id="app">
    <div class="container">
      <ar-input placeholder="Search Name"></ar-input>
      <Search :profiles='profiles' />
    </div>
  </div>
</template>

<script>
import Search from './components/Search.vue'
import { of } from 'rxjs';
import { debounceTime, distinctUntilChanged } from 'rxjs/operators';

const profiles = [
  {
    "id": "1",
    "name": "Arjay Elbore",
    "profession": "Framework Developer",
    "motto": "I never wanted to be famous, I wanted to be great."
  },
  {
    "id": "2",
    "name": "Aivan Monceller",
    "profession": "Developer",
    "motto": "When in doubt, iterate faster!"
  },
  {
    "id": "2",
    "name": "Christopher Lloyd",
    "profession": "UX Developer",
    "motto": "Genius is the ability to reduce the complicated to the simple."
  },
  {
    "id": "3",
    "name": "Martin Llaneza",
    "profession": "UI Developer",
    "motto": "The key to performance is elegance, not battalions of special cases."
  },
  {
    "id": "4",
    "name": "Melvin Vivas",
    "profession": "Manager - Solutions Engineering",
    "motto": "When in Doubt, Iterate Faster."
  },
  {
    "id": "5",
    "name": "Murali Pusuluri",
    "profession": "UI Developer",
    "motto": "To iterate is human, to recurse is divine."
  },
  {
    "id": "6",
    "name": "Nox Mendina",
    "profession": "Sr. Manager - Solutions Engineering",
    "motto": "When in doubt, iterate faster!"
  }
];

// const getProfiles = (username) => {
//   return fetch(`https://api.github.com/users/${username}/repos`)
//     .then(res => res.json());
// }

export default {
  name: 'app',
  async created() {
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
      loading: false,
      profiles: []
    }
  },
  components: {
    Search
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: left;
  color: #2c3e50;
  margin-top: 10px;
}
</style>
