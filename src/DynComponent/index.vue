<script lang="tsx" setup>
import { ref, watch, onMounted, onUnmounted } from "vue";
import "./styles/index.scss";
import * as Echarts from "echarts";

const props = defineProps<{
  options?: Echarts.EChartsCoreOption;
}>();
let echartsOptions = ref<Echarts.EChartsCoreOption>(props.options || {});
let echartsInstance: Echarts.ECharts | null = null;
const rootRef = ref<HTMLElement>();

function getEchartsClass(): typeof Echarts {
  return Echarts;
}
function getEchartsInstance(): Echarts.ECharts | null {
  return echartsInstance;
}
function getEchartsOptions(): Echarts.EChartsCoreOption {
  return echartsOptions.value;
}
function setOptions(
  options: Echarts.EChartsCoreOption,
  notMerge?: boolean,
  lazyUpdate?: boolean
) {
  echartsOptions.value = options;
  echartsInstance?.setOption(echartsOptions.value, notMerge, lazyUpdate);
}

watch(
  () => props.options,
  (options: Echarts.EChartsCoreOption | undefined) => {
    if (options) {
      setOptions(options, true, true);
    }
  }
);

onMounted(() => {
  echartsInstance = Echarts.init(rootRef.value);
  setOptions(echartsOptions.value, true, true);

  const resize = () => {
    echartsInstance?.resize();
  };
  window.addEventListener("resize", resize);

  onUnmounted(() => {
    echartsInstance?.dispose();
    window.removeEventListener("resize", resize);
  });
});

defineExpose({
  getEchartsClass,
  getEchartsInstance,
  getEchartsOptions,
  setOptions,
});
</script>

<template>
  <main ref="rootRef" class="dyn-component--vue dyn-echarts"></main>
</template>

<style lang="scss" scoped></style>
