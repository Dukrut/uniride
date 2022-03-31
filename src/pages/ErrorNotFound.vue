<template>
  <div class="fullscreen uniride-bg text-white text-center q-pa-md flex flex-center">
    <div>
      <div>
        <h1 class="uniride-text">
          404
        </h1>
      </div>

      <div class="text-h2" style="opacity:.6">
        <span class="uniride-text">
          Ops! Acho que você se perdeu por ai!
        </span>
      </div>

      <q-btn
        class="q-mt-xl uniride-button"
        unelevated
        to="/"
        label="Ir para página inicial"
        no-caps
      />
    </div>
  </div>
</template>

<script>
import { defineComponent } from 'vue'

export default defineComponent({
  name: 'ErrorNotFound'
})
</script>
