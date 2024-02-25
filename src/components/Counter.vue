<template>
  <div
    class="w-1/3 p-10 text-2xl mx-auto rounded-xl shadow-lg text-center my-10"
  >
    <h3 class="font-bold mb-10">Enrollment Closes In:</h3>
    <div class="flex justify-between items-center">
      <div>
        <span class="text-5xl">{{ display_days }}</span>
        <p class="text-xs">days</p>
      </div>
      <span>:</span>
      <div>
        <span class="text-5xl">{{ display_hours }}</span>
        <p class="text-xs">hours</p>
      </div>
      <span>:</span>
      <div>
        <span class="text-5xl">{{ display_minutes }}</span>
        <p class="text-xs">minutes</p>
      </div>
      <span>:</span>
      <div>
        <span class="text-5xl">{{ display_seconds }}</span>
        <p class="text-xs">seconds</p>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: ['year', 'month', 'date', 'hour', 'minute', 'second', 'millisecond'],
  data: () => ({
    display_days: 0,
    display_hours: 0,
    display_minutes: 0,
    display_seconds: 0,
  }),
  computed: {
    _seconds() {
      return 1000
    },
    _minutes() {
      return this._seconds * 60
    },
    _hours() {
      return this._minutes * 60;
    },
    _days() {
      return this._hours * 24;
    },
    end() {
      return new Date(
        this.year,
        this.month,
        this.date,
        this.hour,
        this.minute,
        this.second,
        this.millisecond,
      )
    }
  },
  mounted() {
    this.showRemaining()
  },
  methods: {
    formatNum: num => (num < 10 ? '0' + num : num),
    showRemaining() {
      const timer = setInterval(() => {
        const now = new Date();
        // const end = new Date(2023, 9, 20, 10, 10, 10, 10);
        const distance = this.end.getTime() - now.getTime();

        if (distance < 0) {
          clearInterval(timer);
          return;
        }

        const days = Math.floor(distance / this._days);
        const hours = Math.floor((distance % this._days) / this._hours);
        const minutes = Math.floor((distance % this._hours) / this._minutes);
        const seconds = Math.floor((distance % this._minutes) / this._seconds);

        this.display_days = this.formatNum(days)
        this.display_hours = this.formatNum(hours)
        this.display_minutes = this.formatNum(minutes)
        this.display_seconds = this.formatNum(seconds)
      }, 1000);
    },
  },
  
};
</script>

<style scoped></style>
