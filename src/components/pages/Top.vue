<template>
    <v-content>
        <FileUploadBar class="file-upload-bar" />
        <Resultform />
        
    </v-content>
</template>

<style scoped>
.file-upload-bar {
    padding: 0 10%;
}
</style>

<script>
import FileUploadBar from '../organisms/FileUploadBar.vue';
import MatchingTable from '../organisms/MatchingTable.vue';
import Resultform from '../organisms/Result.vue';

export default {
    components: {
        FileUploadBar,
        MatchingTable,
        Resultform,
    },
};
</script>
  