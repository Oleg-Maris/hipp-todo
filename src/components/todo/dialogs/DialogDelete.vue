<template>
  <v-dialog :value="true" persistent max-width="290">
    <v-card>
      <v-card-title class="text-h5"> Delete task? </v-card-title>

      <v-card-text
        >Are you sure you wanna delete this gosh darn motherflipping
        task?</v-card-text
      >
      <v-card-actions>
        <v-spacer></v-spacer>
        <v-btn @click="$emit('close')" text> No </v-btn>
        <v-btn
          @click="$store.dispatch('deleteTask', id)"
          color="red darken-1"
          text
        >
          Yes
        </v-btn>
      </v-card-actions>
    </v-card>
  </v-dialog>
</template>

<script>
export default {
  props: ["id"],
};
</script>
