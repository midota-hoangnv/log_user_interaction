<template>
  <div>
    <button id="launch-widget-btn" @click="handleClick">
      Call With Us
    </button>
  </div>
</template>

<script>
import { datadogRum } from "@datadog/browser-rum";

export default {
  data() {
    return {};
  },
  mounted() {
    // initialize the streams api
    this.init();
  },
  methods: {
    handleClick() {
      console.log("click");
      datadogRum.setUser({
        id: "1234",
        name: "John Doe",
        email: "john@doe.com",
        plan: "premium",
      });
      datadogRum.addAction("search-category", {
        value: 1, // for example, 42.12
        items: [
          {
            id: 1,
            name: "Iphone 7 s",
            price: 10,
          },
        ], // for example, ['tomato', 'strawberries']
        includeTax: false,
        total: 2,
        userIds: [1, 2, 3],
      });
    },
    init() {
      datadogRum.init({
        applicationId: "22db8df2-5233-497a-a5af-aef581c4bece",
        clientToken: "puba8540ed275b102d2decf9d7dc43bb0a3",
        site: "ap1.datadoghq.com",
        service: "test-app",
        env: "development",
        // Specify a version number to identify the deployed version of your application in Datadog
        // version: '1.0.0',
        sessionSampleRate: 100,
        sessionReplaySampleRate: 20,
        trackUserInteractions: true,
        trackResources: false,
        trackLongTasks: false,
        defaultPrivacyLevel: "mask-user-input",
      });
    },
  },
};
</script>

<style>
#the-canvas {
  border: 1px solid black;
  direction: ltr;
}

.d-none {
  display: none;
}

.fakeRect {
  position: absolute;
  background: transparent;
  height: 100px;
  width: 100px;
  left: 359px;
  bottom: 150px;
  z-index: 1;
  content: "";
}

canvas {
  position: relative;
}
</style>
