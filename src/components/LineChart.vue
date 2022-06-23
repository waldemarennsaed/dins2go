<script setup lang="ts">
import { onBeforeMount, watch, ref, computed } from 'vue';
import { Chart as highcharts } from 'highcharts-vue';
import Highcharts from 'highcharts';
import merge from 'lodash.merge';
import nodata from 'highcharts/modules/no-data-to-display';

nodata(Highcharts);

onBeforeMount(() => {
  /**
   * https://github.com/highcharts/highcharts-vue/issues/71#issuecomment-485784315
   * The 'lang' object can not be updated to force a re-draw. Languages only change on rendering (create/destroy hooks)
   */
  Highcharts.setOptions({
    chart: {
      style: {
        fontFamily: 'Roboto, sans-serif',
      },
    },
    time: {
      timezoneOffset: new Date().getTimezoneOffset(),
    },
  });
});

export type ZoomParameters = {
  start: number;
  end: number;
};

interface Props {
  customChartOptions?: Highcharts.ChartOptions;
  loading?: boolean;
  series: any;
}

const props = withDefaults(defineProps<Props>(), {
  loading: false,
});

const chartRef = ref(null);

watch(props.loading, async (newValue, oldValue) => {
  if (newVal === true) {
    chartRef.chart.showLoading();
  } else {
    chartRef.chart.hideLoading();
  }
});

const emit = defineEmits<{
  (e: 'linechart:reset-zoom'): void;
  (e: 'linechart:zoom', zoomParameters: ZoomParameters): void;
}>();

const chartOptions = computed(() => {
  const result = {
    chart: {
      events: {
        selection: (event: any) => {
          const resetZoomButton: any = chartRef.chart.resetZoomButton;
          if (event.resetSelection) {
            if (resetZoomButton !== undefined) resetZoomButton.hide();
            emit('linechart:reset-zoom');
          } else {
            if (resetZoomButton !== undefined) resetZoomButton.show();
            const newStartTime: number = event.xAxis[0].min;
            const newEndTime: number = event.xAxis[0].max;
            emit('linechart:zoom', {
              end: newEndTime,
              start: newStartTime,
            } as ZoomParameters);
          }
        },
      },
      step: 'left',
      type: 'line',
      zoomType: 'x',
    },
    credits: {
      enabled: false,
    },
    legend: {
      enabled: false,
    },
    loading: {
      useHTML: true,
    },
    noData: {
      useHTML: true,
    },
    title: {
      text: '',
    },
    tooltip: {
      useHTML: true,
      valueDecimals: 2,
    },
    xAxis: {
      type: 'datetime',
    },
    yAxis: {
      allowDecimals: false,
      title: {
        style: {
          fontSize: 14,
        },
        text: 'Values',
      },
    },
    ...props.customChartOptions,
  };
  merge(result, props.customChartOptions);
  // This is done after creating the object to ensure that the series comes from the prop, not from customChartOptions
  Object.assign(result, {
    series: props.series,
  });
  return result;
});
</script>

<template>
  <highcharts
    ref="chartRef"
    :options="chartOptions"
    :update-args="[true, true, true]"
  />
</template>

<style lang="sass">
.unit-tag
  padding: 6px
  background-color: black
  color: whitej
  font-size: 12px
  border: none
  border-radius: 10px
</style>
