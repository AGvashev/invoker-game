<template>
    <div class="settings">
        <h2>Setting</h2>
        <div class="setting">
            <div 
            v-for="key in settings" 
            :key="key.name"
            class="keys">
                {{ key.button }} - {{ key.name }}
            </div>
        </div>
        
    </div>
</template>

<script>

export default {
  name: 'Settings',
  props: {
      settings: Object,
  },
}
</script>

<style>

</style>
