<script setup>
import { computed } from 'vue'
const emit = defineEmits(['update:modelValue', 'createCardMessage', 'createCardFile', 'onPaste'])

const props = defineProps({
  modelValue: String
})

const computedValue = computed({
  get: () => props.modelValue,
  set: value => {
    emit('update:modelValue', value)
  }
})
</script>
<template>
  <div class="flex w-full">
    <div class="rounded-l-[10px] flex items-center justify-center bg-[#F4F5F7] pl-[15px]">
      <label for="file-input">
        <svg
          width="18"
          height="17"
          class="cursor-pointer"
          viewBox="0 0 18 17"
          fill="none"
          xmlns="http://www.w3.org/2000/svg"
        >
          <path
            d="M1.65832 15.0516C2.76387 16.1467 4.21322 16.6875 5.66256 16.6875C7.11191 16.6875 8.56126 16.14 9.66681 15.045L16.6169 8.16097C18.1944 6.59855 18.1944 4.05461 16.6169 2.49219C15.8552 1.73769 14.8373 1.31704 13.7587 1.31704C12.6801 1.31704 11.6622 1.73101 10.9004 2.49219L4.51657 8.81531C3.57281 9.75009 3.57281 11.2791 4.51657 12.2139C5.46033 13.1487 7.00405 13.1487 7.94781 12.2139L12.1475 8.05414C12.4644 7.74032 12.4644 7.23286 12.1475 6.91904C11.8307 6.60523 11.3184 6.60523 11.0016 6.91904L6.80856 11.0855C6.49172 11.3993 5.9794 11.3993 5.66256 11.0855C5.34573 10.7717 5.34573 10.2642 5.66256 9.9504L12.0397 3.63396C12.4981 3.17992 13.1048 2.93287 13.7587 2.93287C14.4058 2.93287 15.0193 3.17992 15.4777 3.63396C16.4214 4.56874 16.4214 6.09777 15.4777 7.03255L8.52081 13.9165C6.94338 15.479 4.375 15.479 2.79758 13.9165C2.03583 13.162 1.61788 12.1538 1.61788 11.0855C1.61788 10.0172 2.03583 9.00895 2.80432 8.25445L9.7477 1.37045C10.0645 1.05664 10.0645 0.549183 9.7477 0.235364C9.43087 -0.0784548 8.91854 -0.0784548 8.6017 0.235364L1.65832 7.11935C0.58648 8.17432 0 9.58317 0 11.0855C0 12.5811 0.58648 13.99 1.65832 15.0516Z"
            fill="black"
            fill-opacity="0.5"
          />
        </svg>
      </label>
      <input
        id="file-input"
        type="file"
        multiple="multiple"
        style="display: none;"
        name="file-input"
        @change="$emit('createCardFile', $event)"
      >
    </div>

    <textarea
      id="card-message-textarea"
      v-model="computedValue"
      class="bg-[#F4F5F7] py-[17px] pr-[15px] pl-[10px] text-[#656566] w-full text-[14px] border-none focus:ring-0"
      style="resize: none;"
      rows="1"
      type="text"
      placeholder="Напишите сообщение..."
      @paste="$emit('onPaste', $event)"
      @keydown.enter.exact.prevent="$emit('createCardMessage', computedValue.value)"
    />

    <div
      class="rounded-r-[10px] flex items-center justify-center bg-[#F4F5F7] pr-[12px]"
    >
      <div
        class="rounded-[8px] flex items-center justify-center min-w-[32px] min-h-[32px] bg-[#E0E1E3] hover:bg-white cursor-pointer"
        @click="$emit('createCardMessage', computedValue.value)"
      >
        <svg
          width="14"
          height="17"
          viewBox="0 0 14 17"
          fill="none"
          xmlns="http://www.w3.org/2000/svg"
        >
          <path
            d="M7 0L0 7L0.987 7.987L6.3 2.681V16.8H7.7V2.681L13.013 7.987L14 7L7 0Z"
            fill="#4C4C4D"
          />
        </svg>
      </div>
    </div>
  </div>
</template>
