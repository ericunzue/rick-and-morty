<template>
  <section>
    <div class="characters">
      <div class="character__item" v-for="character in characters" :key="character.id">

       <CardCharacter :character="character" />
      </div>
    </div>
  </section>
</template>

<script>
import { computed, onMounted } from 'vue';
import {useStore} from 'vuex';
import CardCharacter from '@/components/CardCharacter';
export default {
  components:{
    CardCharacter
  },
  setup(){
    const store = useStore();
    const characters = computed(() => {
      return store.state.charactersFilter;
    })
    onMounted(() => {
      store.dispatch('getCharacters');
    })

    return{ 
      characters
    };
  }
  
}
</script>

<style>
.characters{
  display:grid;
  grid-template-columns: repeat(4, 1fr);
  gap:1.5rem;
  margin: 3rem 0;
}
</style>