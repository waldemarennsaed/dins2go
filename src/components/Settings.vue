<script setup lang="ts">
import { ref } from 'vue';

const token = `eyJhbGciOiJSUzI1NiIsInR5cCIgOiAiSldUIiwia2lkIiA6ICJLMjdRR3l1YlhId09Ia1ZZcXdja0dUZ0FvNWdiUFFUbGtSX0tvc2JJLVhjIn0.eyJleHAiOjE2NTYwMTgxMjAsImlhdCI6MTY1NjAxNzIyMCwiYXV0aF90aW1lIjoxNjU2MDE0ODk3LCJqdGkiOiI0OWI0ZGYxMy04ZDgwLTQ0ZWYtYWRjNy1iM2ZiZGZlZTAxMTAiLCJpc3MiOiJodHRwczovL2F1dGguZXZvZGV2LmFlZGlmaW9uLmV1L2F1dGgvcmVhbG1zL2FlZGlmaW9uIiwiYXVkIjpbImFsZXJ0YS1hcGkiLCJkaXNjb3Zlcnktc2VydmVyIiwibW9iaWxlLWFwcCIsImdyYWZhbmEtbW9uaXRvcmluZyIsImFkbWluLWZyb250ZW5kIiwiY29uZmFwcCIsImFjY291bnQiLCJidWlsZGluZy1jb25uZWN0Il0sInN1YiI6ImY6MGRmYWU0MDAtOGYzYi00NjdmLTg5YmMtMzk5MjMzOGEzY2I1OjIiLCJ0eXAiOiJCZWFyZXIiLCJhenAiOiJmcm9udGVuZCIsInNlc3Npb25fc3RhdGUiOiI2Mjk5ODQ3NS1kOTRiLTQwMzItYTQzZS1kNWRkY2NlOTVlNDQiLCJhY3IiOiIwIiwiYWxsb3dlZC1vcmlnaW5zIjpbImh0dHBzOi8vdml0ZWpzLXZpdGUtYXNleHBqLS0zMDAwLmxvY2FsLndlYmNvbnRhaW5lci5pbyIsImh0dHA6Ly9sb2NhbGhvc3Q6ODA4MCIsImh0dHBzOi8vd3d3LmV2b2Rldi5hZWRpZmlvbi5ldSIsImh0dHBzOi8vbmV3LmV2b2Rldi5hZWRpZmlvbi5ldSJdLCJyZWFsbV9hY2Nlc3MiOnsicm9sZXMiOlsib2ZmbGluZV9hY2Nlc3MiLCJ1bWFfYXV0aG9yaXphdGlvbiJdfSwicmVzb3VyY2VfYWNjZXNzIjp7ImRpc2NvdmVyeS1zZXJ2ZXIiOnsicm9sZXMiOlsidXNlciJdfSwibW9iaWxlLWFwcCI6eyJyb2xlcyI6WyJ1c2VyIl19LCJncmFmYW5hLW1vbml0b3JpbmciOnsicm9sZXMiOlsiQWRtaW4iXX0sImFkbWluLWZyb250ZW5kIjp7InJvbGVzIjpbImFkbWluaXN0cmF0b3IiXX0sImFsZXJ0YS1hcGkiOnsicm9sZXMiOlsiYWRtaW4iXX0sImNvbmZhcHAiOnsicm9sZXMiOlsiZ3JvdW5kdHJ1dGgiXX0sImFjY291bnQiOnsicm9sZXMiOlsibWFuYWdlLWFjY291bnQiLCJtYW5hZ2UtYWNjb3VudC1saW5rcyIsInZpZXctcHJvZmlsZSJdfSwiYnVpbGRpbmctY29ubmVjdCI6eyJyb2xlcyI6WyJ1c2VyIl19LCJmcm9udGVuZCI6eyJyb2xlcyI6WyJhbGVydGEtcmVhZGVyIiwidXNlciJdfX0sInNjb3BlIjoib3BlbmlkIGFwaSBlbWFpbCBwcm9maWxlIHJvbGVzIiwiZW1haWxfdmVyaWZpZWQiOmZhbHNlLCJuYW1lIjoiV2FsZGVtYXIgRW5ucyIsInByZWZlcnJlZF91c2VybmFtZSI6Indlbm5zQGFlZGlmaW9uLmNvbSIsImdpdmVuX25hbWUiOiJXYWxkZW1hciIsImZhbWlseV9uYW1lIjoiRW5ucyIsImFlZF9pZCI6MiwiZW1haWwiOiJ3ZW5uc0BhZWRpZmlvbi5jb20ifQ.lEK_paIsy4Z1nhOaBAesKKfIRrGKmBrYhQ-IH-MJvN3AqBN5w7KCHG3JkFB8jV8YhltPJZa7u9dhMGUH5uVT1fby4-7WGo2LKTn0l5dPBMpYuQ1tQfEZ4GkQDBT1wP7aleNdqY-V7uasAbrHm6XY2NU_obiKP_Pgcf0DCOHFIQ4xqiNc5J7CFrULrW9QzS7pi2jIr2pFtd0mOapMAAx-rDCkiSk6v0hZ04XzZf35di1DyaUAFgDcIC7Gm6FzJhW0jRT7N5taKtaU5tFxnJjm0NKQbrBPKF1l5xDAe9vrn_VBOX-iFPWcKSVrq-_-MTU3IbhmY10PGwKtgNec0QTcrA
`;

const interpolation = ref('previous');
const closedInterval = ref(false);
const short = ref(true);
const aggregation = ref('mean');
const start = ref(null);
const end = ref(new Date().toISOString().slice(0, 10));
const max = ref(null);
const samplerate = ref('auto');
const datapoints = ref('Dev101_Weather_Hum_ME_AI2');
const project = ref(15);

const emit = defineEmits<{
  (e: 'update:series', series: any[]): void;
}>();

function validateForm() {
  const form = document.querySelector('form');
  if (!form.checkValidity()) {
    document.querySelector('#submit').click();
    return false;
  } else {
    return true;
  }
}

function requestTimeseries() {
  const params = new URLSearchParams({
    dataPointIDs: datapoints.value,
    start: start.value ? start.value : '',
    end: end.value,
    max: max.value ? parseInt(max.value) : 1,
    closed_interval: closedInterval.value,
    interpolation: interpolation.value,
    short: short.value,
    aggregation: aggregation.value,
    samplerate: samplerate.value ?? null,
  });
  fetch(
    `https://api.evodev.aedifion.eu/v2/project/${project.value}/timeseries?${params}`,
    {
      headers: {
        Authorization: `Bearer ${token}`,
      },
    }
  )
    .then((data) => data.json())
    .then((response) => {
      const timeseriesResults = Object.keys(response);
      const seriesData = [];
      for (let timeseries of timeseriesResults) {
        const ser = {
          data: response[timeseries],
          marker: { enabled: false },
          name: timeseries,
          step: true,
          tooltip: {
            pointFormat: '{series.name}: <b>{point.y}</b>',
          },
        };
        seriesData.push(ser);
        emit('update:series', seriesData);
      }
    });
}

function validateAndFetchData() {
  if (validateForm()) {
    requestTimeseries();
  }
}
</script>

<template>
  <form>
    <div class="group">
      <div class="label-group">
        <label for="short">Short</label>
        <input type="checkbox" id="short" checked v-model="short" />
      </div>
    </div>

    <div class="group">
      <div class="label-group">
        <label for="previous">Previous</label>
        <input
          type="radio"
          name="interpolation"
          value="previous"
          v-model="interpolation"
          id="previous"
        />
      </div>

      <div class="label-group">
        <label for="linear">Linear</label>
        <input
          type="radio"
          name="interpolation"
          value="linear"
          id="linear"
          v-model="interpolation"
        />
      </div>

      <div class="label-group">
        <label for="null">Null</label>
        <input
          type="radio"
          name="interpolation"
          value="null"
          id="null"
          v-model="interpolation"
        />
      </div>

      <div class="label-group">
        <label for="none">None</label>
        <input
          type="radio"
          name="interpolation"
          value="none"
          id="none"
          v-model="interpolation"
        />
      </div>
    </div>

    <div class="group">
      <div class="label-group">
        <label for="closed_interval">Closed intervals</label>
        <input type="checkbox" id="closed_interval" v-model="closedInterval" />
      </div>
    </div>

    <div class="group">
      <div class="label-group">
        <label for="mean">Mean</label>
        <input
          type="radio"
          name="aggregation"
          value="mean"
          id="mean"
          checked
          v-model="aggregation"
        />
      </div>

      <div class="label-group">
        <label for="min">Min</label>
        <input
          type="radio"
          name="aggregation"
          value="min"
          id="min"
          v-model="aggregation"
        />
      </div>

      <div class="label-group">
        <label for="max">Max</label>
        <input
          type="radio"
          name="aggregation"
          value="max"
          id="max"
          v-model="aggregation"
        />
      </div>
    </div>

    <div class="group">
      <div class="label-group">
        <label for="start">Start</label>
        <input type="date" name="start" id="start" v-model="start" />
      </div>

      <div class="label-group">
        <label for="end">End</label>
        <input type="date" name="end" id="end" v-model="end" />
      </div>
    </div>

    <div class="group">
      <div class="label-group">
        <label for="max">Max</label>
        <input type="text" name="max" id="max" v-model="max" />
      </div>
    </div>

    <div class="group">
      <div class="label-group">
        <label for="samplerate">Samplerate</label>
        <input
          type="text"
          name="samplerate"
          id="samplerate"
          v-model="samplerate"
        />
      </div>
    </div>

    <div class="group">
      <div class="label-group">
        <label for="project">Project ID</label>
        <input
          type="number"
          name="project"
          id="project"
          v-model="project"
          required
        />
      </div>

      <div class="label-group">
        <label for="datapoints">Datapoint IDs</label>
        <textarea
          name="datapoints"
          id="datapoints"
          cols="30"
          rows="5"
          placeholder="DP1,DP2,DP3"
          v-model="datapoints"
          required
        ></textarea>
      </div>
    </div>

    <button type="button" @click="validateAndFetchData">
      Request timeseries data
    </button>
    <input type="submit" id="submit" style="display: none" />
  </form>
</template>

<style lang="sass">
form
  display: flex
  flrex-direction: row
  flex-wrap: wrap

.group
  border: 1px solid grey
  flex: 1
  min-width: 400px
  width: 400px
  max-width: 400px

.label-group
  display: flex
  flex-direction: row
  align-items: center
  justify-content: end
  margin: 2rem

  label
    margin-right: .5rem
</style>
