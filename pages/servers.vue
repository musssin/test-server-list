<template>
  <div class="mx-auto max-w-full px-4 sm:px-6 lg:px-8">
    <div class="grid grid-cols-12 gap-6 ">
      <EditServer :server="selectedServer" class="col-span-12 md:col-span-4  md:order-2" @save="save" />
      <ServersList v-if="data" :servers="data" class="col-span-12 md:col-span-7 md:order-1" />
      <div v-else>Loading...</div>


    </div>
  </div>
</template>
<script setup lang="ts">
import type Server from '~/models/Server';

const URL = '/api/servers'

const { data, pending, error } = useFetch<Array<Server>>(URL, {
  method: 'get'
})

const { selectedServer } = useSelectServer()

const save = (server: Server) => {
  const edited = data.value?.find(s => s.id === server.id)
  if (edited) {
    edited.server_name = server.server_name
    edited.server_type = server.server_type
  }
}
</script>
