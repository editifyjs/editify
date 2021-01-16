<template>
  <div>
    <div class="mb-4" v-for="(item, i) in items" :key="i">
      <h2 v-html="item.content"></h2>
    </div>
  </div>
</template>

<script>
export default {
  data: () => ({
    items: [
      {
        type: "feature",
        content:
          "&#128640;&nbsp;&nbsp;&nbsp; The image main feature will be added.",
      },
      {
        type: "feature",
        content:
          "&#128640;&nbsp;&nbsp;&nbsp; The delimiter main feature will be added.",
      },
      {
        type: "bug",
        content:
          "&#128030;&nbsp;&nbsp;&nbsp; Text popup should only appear on editable fields.",
      },
      {
        type: "feature",
        content:
          "&#128640;&nbsp;&nbsp;&nbsp; Although the main feature of the video is not in the short term, it is thought to be added in the long term.",
      },
      {
        type: "bug",
        content:
          "&#128030;&nbsp;&nbsp;&nbsp; When using with 3rd party frameworks, some css features have slipped, they are being worked on!",
      },
      {
        type: "feature",
        content: "&#128640;&nbsp;&nbsp;&nbsp; Emoji plugin will be created.",
      },
    ],
  }),
};
</script>

<style scoped>
h2 {
  font-weight: 200;
  font-size: 18px;
}
</style>