<template>
    <v-btn class="jbtn-file">
        {{ title }}<input type="file" @change="fileSelected" @click="nullifyEventTarget">
    </v-btn>
</template>

<script>
export default {
    name: 'UploadButton',
    props: {
        selectedCallback: {
            type: Function,
            default: function handleFile() {},
        },
        title: { type: String, default: 'Upload' },
    },
    methods: {
        nullifyEventTarget(e) {
            // So that the same file can be selected multiple times
            e.target.value = null;
        },
        fileSelected(e) {
            if (this.selectedCallback) {
                if (e.target.files[ 0 ]) {
                    this.selectedCallback(e.target.files[ 0 ]);
                } else {
                    this.selectedCallback(null);
                }
            }
        },
    },
};
</script>

<style scoped>
.jbtn-file {
    cursor: pointer;
    position: relative;
    overflow: hidden;
}

.jbtn-file input[type='file'] {
    position: absolute;
    top: 0;
    right: 0;
    min-width: 100%;
    min-height: 100%;
    font-size: 100px;
    text-align: right;
    filter: alpha(opacity=0);
    opacity: 0;
    outline: none;
    cursor: inherit;
    display: block;
}
</style>
