<script setup lang="ts">
import { ref, onMounted } from 'vue'
import QRCode from 'qrcode'

const discordUrl = 'https://discord.gg/j9HCDdAe'
const qr = ref('')

onMounted(async () => {
  try {
    qr.value = await QRCode.toDataURL(discordUrl, { margin: 1, width: 256 })
  } catch (err) {
    console.error('Failed to render Discord QR code', err)
  }
})
</script>

<template>
  <div class="absolute bottom-0 left-0 right-0 z-10 flex items-end justify-end gap-3 p-3 pointer-events-none">
    <div class="px-4 py-2 rounded-lg bg-black/70 text-white text-sm">
      Software Meeting · <strong>Thursdays 9pm</strong> on Discord
    </div>
    <img v-if="qr" :src="qr" alt="QR code for the PROVES Discord" class="w-20 h-20 rounded bg-white">
  </div>
</template>
