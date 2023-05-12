<template>
  <div class="w-auto mt-1 d-flex justify-content-between flex-wrap">
    <div class="align-self-center d-none d-sm-block">
      <span class="badge rounded-pill bg-primary">{{ leftCount }}</span> Items
      left
    </div>
    <div class="btn-group btn-group-sm" role="group">
      <button
        type="button"
        :class="[viewState == 'all' ? 'btn btn-dark' : 'btn btn-outline-dark']"
        @click="setViewState('all')"
      >
        All
      </button>
      <button
        type="button"
        :class="[
          viewState == 'uncheck' ? 'btn btn-dark' : 'btn btn-outline-dark',
        ]"
        @click="setViewState('uncheck')"
      >
        Active
      </button>
      <button
        type="button"
        :class="[
          viewState == 'check' ? 'btn btn-dark' : 'btn btn-outline-dark',
        ]"
        @click="setViewState('check')"
      >
        Completed
      </button>
    </div>
    <div class="btn-group btn-group-sm" role="group">
      <button
        type="button"
        class="btn btn-outline-danger"
        @click="setViewState('clear')"
      >
        Clear Completed
      </button>
    </div>
  </div>
</template>

<script>
export default {
  props: ["viewState", "leftCount"],
  data() {
    return {
      viewStates: this.viewState,
    };
  },
  methods: {
    setViewState(viewState) {
      this.$emit("setViewState", viewState);
    },
  },
};
</script>

<style>
</style>
