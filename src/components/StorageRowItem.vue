<script lang="ts" setup>
import type {StorageItem} from "@/models/storage";
import ButtonsDownloadDelete from "@/components/ButtonsDownloadDelete.vue";
import {convertTime, convertSize} from '@/utils/displayFormats'

const props = defineProps<{
  item: StorageItem
  storageDataStore: any
}>()

function getUploadingItemText() {
  let percentage = (props.item.size_uploaded / props.item.size_total) * 100;
  return convertSize(props.item.size_uploaded) + " / " + convertSize(props.item.size_total) + " (" + Math.round(percentage) + "%)"
}

</script>

<template>
  <template v-if="item.time_edited == ''" > <!-- an uploading item -->
    <div class="flex-grow text-gray-700">{{item.name}}</div>
    <div class="upload-status-width text-right mr-2 text-gray-700">{{getUploadingItemText()}}</div>
  </template>
  <template v-else>  <!-- an stable item -->
    <div class="flex-grow">{{item.name}}</div>
    <div class="last-modified-width">{{convertTime(item.time_edited)}}</div>
    <div class="size-width">{{ convertSize(item.size_total) }}</div>
    <div class="actions-width"><buttons-download-delete :item="props.item" :storage-data-store="props.storageDataStore"/></div>
  </template>
</template>
