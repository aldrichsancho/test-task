<template>
  <form @submit.prevent="submitForm">
    <div class="row" style="padding-bottom: 14px">
      <div class="col-12 col-sm-6" style="padding-bottom: 8px">
        <Vue3DraggableResizable
          :initW="computedWidth"
          :initH="computedHeight"
          v-model:x="x"
          v-model:y="y"
          v-model:w="w"
          v-model:h="h"
          v-model:active="active"
          :draggable="true"
          :resizable="true"
          @activated="print('activated')"
          @deactivated="print('deactivated')"
          @drag-start="print('drag-start')"
          @resize-start="print('resize-start')"
          @dragging="print('dragging')"
          @resizing="print('resizing')"
          @drag-end="print('drag-end')"
          @resize-end="print('resize-end')"
        >
          <FormKit
            style="width: 100%"
            type="text"
            label="Name"
            name="name"
            v-model="formData.name"
            validation="required"
          />
        </Vue3DraggableResizable>
      </div>
      <div class="col-12 col-sm-6" style="padding-bottom: 8px">
        <!-- Tambahkan style padding-bottom disini juga -->
        <Vue3DraggableResizable
          :initW="computedWidth"
          :initH="computedHeight"
          v-model:x="x1"
          v-model:y="y1"
          v-model:w="w"
          v-model:h="h"
          v-model:active="active1"
          :draggable="true"
          :resizable="true"
          @activated="print('activated')"
          @deactivated="print('deactivated')"
          @drag-start="print('drag-start')"
          @resize-start="print('resize-start')"
          @dragging="print('dragging')"
          @resizing="print('resizing')"
          @drag-end="print('drag-end')"
          @resize-end="print('resize-end')"
        >
          <FormKit
            style="width: 100%"
            type="email"
            label="Email"
            name="email"
            v-model="formData.email"
            validation="required|email"
          />
        </Vue3DraggableResizable>
      </div>
    </div>

    <Vue3DraggableResizable
      :initW="computedWidth"
      :initH="computedHeight"
      v-model:x="x2"
      v-model:y="y2"
      v-model:w="w"
      v-model:h="h"
      v-model:active="active1"
      :draggable="true"
      :resizable="true"
      @activated="print('activated')"
      @deactivated="print('deactivated')"
      @drag-start="print('drag-start')"
      @resize-start="print('resize-start')"
      @dragging="print('dragging')"
      @resizing="print('resizing')"
      @drag-end="print('drag-end')"
      @resize-end="print('resize-end')"
    >
      <button
        type="button"
        @click="submitForm"
        :disabled="!isFormValid"
        class="btn btn-primary col-12 col-md-6"
      >
        Save
      </button>
    </Vue3DraggableResizable>
    <div style="height: 100px"></div>
  </form>
</template>

<script>
import {
  ref,
  computed,
  defineComponent,
  onMounted,
  onBeforeUnmount,
} from 'vue';
import Vue3DraggableResizable from 'vue3-draggable-resizable';
import 'vue3-draggable-resizable/dist/Vue3DraggableResizable.css';

export default defineComponent({
  components: { Vue3DraggableResizable },
  setup() {
    const x = ref(14);
    const y = ref(-50);
    const h = ref(100);
    const w = ref(100);
    const x1 = ref(340);
    const y1 = ref(-50);
    const x2 = ref(14);
    const y2 = ref(50);
    const active = ref(false);
    const active1 = ref(false);

    const isMobile = () => window.innerWidth <= 768;

    const computedWidth = computed(() => (isMobile() ? 100 : w.value));
    const computedHeight = computed(() => (isMobile() ? 120 : h.value));

    const updateDimensions = () => {
      if (isMobile()) {
        w.value = 200;
        h.value = 200;
        x1.value = x.value;
        y1.value = y.value + 80;
        x2.value = x.value;
        y2.value = y1.value + 80;
      } else {
        w.value = 300;
        h.value = 200;
        x1.value = 340;
        y1.value = -50;
      }
    };

    onMounted(() => {
      window.addEventListener('resize', updateDimensions);
      updateDimensions(); // Set initial dimensions based on current size
    });

    onBeforeUnmount(() => {
      window.removeEventListener('resize', updateDimensions);
    });

    const formData = ref({
      name: '',
      email: '',
    });

    const isFormValid = computed(
      () => formData.value.name && formData.value.email
    );

    const submitForm = () => {
      if (!isFormValid.value) {
        console.log('Form is invalid');
        return;
      }

      const jsonOutput = JSON.stringify(formData.value);
      console.log('Data:', jsonOutput);
      // Call API for saving data
    };

    const print = (val) => {
      console.log(val);
    };

    return {
      x,
      y,
      h,
      w,
      x1,
      y1,
      x2,
      y2,
      computedWidth,
      computedHeight,
      active,
      active1,
      formData,
      isFormValid,
      submitForm,
      print,
    };
  },
});
</script>

<style>
.parent {
  width: 200px;
  height: 200px;
  position: absolute;
  top: 100px;
  left: 100px;
  border: 1px solid #000;
  user-select: none;
}
</style>
