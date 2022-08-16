<template>
    <v-container class="grey lighten-5 envelope-layout">
        <v-toolbar dark>
            <v-toolbar-title>Create Envelope</v-toolbar-title>
        </v-toolbar>
        <v-row>
            <v-col>
                <v-tabs vertical>
                    <v-tab>
                        <v-icon left>
                            mdi-account
                        </v-icon>
                        Template
                    </v-tab>
                    <v-tab>
                        <v-icon left>
                            mdi-lock
                        </v-icon>
                        Form
                    </v-tab>
                    <v-tab>
                        <v-icon left>
                            mdi-access-point
                        </v-icon>
                        Option 3
                    </v-tab>
                    <v-tab-item>
                        <v-card flat>
                            <v-card-text>
                                <v-file-input @change="selectFile" v-model="envelopeBgImage"
                                    accept="image/png, image/jpeg, image/bmp" placeholder="Upload Background Image"
                                    prepend-icon="mdi-camera" label="Upload Background Image">
                                </v-file-input>
                                <!-- <h3>Set Width & Height</h3>
                                <v-row>
                                    <v-col cols="12" sm="6" md="3">
                                        <v-text-field suffix="%" v-model="envelopeWidth" label="Width" solo>
                                        </v-text-field>
                                    </v-col>
                                    <v-col cols="12" sm="6" md="3">
                                        <v-text-field suffix="%" v-model="envelopeHeight" label="Height" solo>
                                        </v-text-field>
                                    </v-col>
                                </v-row> -->
                                <!-- <h3>Set Border</h3>
                                <v-col cols="12" sm="6" md="3">
                                    <v-text-field v-model="envelopeBorder" label="Border" solo>
                                    </v-text-field>
                                </v-col> -->
                                <h3>Choose Heading Color</h3>
                                <v-color-picker hide-inputs v-model="headingColor" dot-size="10"
                                    swatches-max-height="20">
                                </v-color-picker>
                                <v-slider label="Heading font size" v-model="headingFontSize" :min="1" :max="50">
                                </v-slider>
                                <h3>Choose Sub Heading Color</h3>
                                <v-color-picker hide-inputs v-model="subHeadingColor" dot-size="10"
                                    swatches-max-height="20">
                                </v-color-picker>
                                <v-slider label="Sub-Heading font size" v-model="subHeadingFontSize" :min="1" :max="50">
                                </v-slider>
                                <h3>Choose Address Color</h3>
                                <v-color-picker hide-inputs v-model="addressColor" dot-size="10"
                                    swatches-max-height="20">
                                </v-color-picker>
                                <v-slider label="Address font size" v-model="addressFontSize" :min="1" :max="50">
                                </v-slider>
                                <h3>Choose Mobile Number Color</h3>
                                <v-color-picker hide-inputs v-model="mobileColor" dot-size="10"
                                    swatches-max-height="20">
                                </v-color-picker>
                                <v-slider label="Mobile Number font size" v-model="mobileNumberFontSize" :min="1" :max="50">
                                </v-slider>
                                <h3>Choose Other1 Color</h3>
                                <v-color-picker hide-inputs v-model="other1Color" dot-size="10"
                                    swatches-max-height="20">
                                </v-color-picker>
                                <v-slider label="Other1 font size" v-model="other1FontSize" :min="1" :max="50">
                                </v-slider>
                                <h3>Choose Other2 Color</h3>
                                <v-color-picker hide-inputs v-model="other2Color" dot-size="10"
                                    swatches-max-height="20">
                                </v-color-picker>
                                <v-slider label="Other1 font size" v-model="other2FontSize" :min="1" :max="50">
                                </v-slider>
                            </v-card-text>
                        </v-card>
                    </v-tab-item>
                    <v-tab-item>
                        <v-card flat>
                            <v-card-text>
                                <div class="form-data">
                                    <v-text-field v-model="heading" label="Heading">
                                    </v-text-field>
                                    <v-text-field v-model="subHeading" label="Sub Heading">
                                    </v-text-field>
                                    <v-text-field v-model="address" label="Address"></v-text-field>

                                    <v-text-field v-model="mobile" label="Mobile Number">
                                    </v-text-field>
                                    <v-text-field v-model="other1" label="Other "></v-text-field>
                                    <v-text-field v-model="other2" label="Other">
                                    </v-text-field>
                                </div>
                            </v-card-text>
                        </v-card>
                    </v-tab-item>
                    <v-tab-item>
                        <v-card flat>
                            <v-card-text>
                                <v-btn>Add a heading</v-btn>
                            </v-card-text>
                        </v-card>
                    </v-tab-item>
                </v-tabs>
            </v-col>
            <v-col :style="{ margin: '25px' }">
                <v-card v-if="previewImage" id="imageToSave">
                    <img class="preview" :src="previewImage" alt=""
                        :style="{ width: `${envelopeWidth}%`, height: `${envelopeHeight}%`, borderRadius: `${envelopeBorder}px` }" />
                    <div class="InnerText">
                        <div style="height: 700px; width: 750px; position: relative;">
                            <vue-draggable-resizable class-name-resizable="my-resizable-class" :w="100" :h="50"
                                @dragging="onDrag" @resizing="onResize" :parent="true">
                                <div class="dragable-style"
                                    :style="{ color: `${headingColor}`, fontWeight: 'bold' }">
                                    <h1 :style="{ fontSize: headingFontSize + 'px', fontFamily: 'Tiro Devanagari Marathi' }">{{ heading }}</h1>
                                </div>
                            </vue-draggable-resizable>
                            <vue-draggable-resizable :w="100" :h="50" @dragging="onDrag" @resizing="onResize"
                                :parent="true">
                                <div class="dragable-style" :style="{ color: `${subHeadingColor}` }">
                                    <h1 :style="{ fontSize: subHeadingFontSize + 'px' }">{{ subHeading }}</h1>
                                </div>
                            </vue-draggable-resizable>
                            <vue-draggable-resizable :w="100" :h="50" @dragging="onDrag" @resizing="onResize"
                                :parent="true">
                                <div class="dragable-style" :style="{ color: `${addressColor}` }">
                                    <h1 :style="{ fontSize: addressFontSize + 'px' }">{{ address }}</h1>
                                </div>
                            </vue-draggable-resizable>
                            <vue-draggable-resizable :w="100" :h="50" @dragging="onDrag" @resizing="onResize"
                                :parent="true">
                                <div class="dragable-style" :style="{ color: `${mobileColor}` }">
                                    <h1 :style="{ fontSize: mobileNumberFontSize + 'px' }">{{ mobile }}</h1>
                                </div>
                            </vue-draggable-resizable>
                            <vue-draggable-resizable :w="100" :h="50" @dragging="onDrag" @resizing="onResize"
                                :parent="true">
                                <div class="dragable-style" :style="{ color: `${headingColor}` }">
                                    <h1 :style="{ fontSize: other1FontSize + 'px' }">{{ other1 }}</h1>
                                </div>
                            </vue-draggable-resizable>
                            <vue-draggable-resizable :w="100" :h="50" @dragging="onDrag" @resizing="onResize"
                                :parent="true">
                                <div class="dragable-style" :style="{ color: `${headingColor}` }">
                                    <h1 :style="{ fontSize: other2FontSize + 'px' }">{{ other2 }}</h1>
                                </div>
                            </vue-draggable-resizable>
                        </div>
                    </div>
                </v-card>
                <v-card v-if="!previewImage" height="750" width="500"></v-card>
                <div>
                    <v-btn class="ma-2" color="success" @click="saveImage">Download</v-btn>
                </div>
            </v-col>
        </v-row>
    </v-container>
</template>

<script>
import VueDraggableResizable from 'vue-draggable-resizable'
import { saveAsJpeg } from "save-html-as-image";

export default {
    name: 'EnvelopeDesign',
    components: {
        VueDraggableResizable
    },
    data: () => ({
        heading: '',
        subHeading: '',
        mobile: '',
        address: '',
        other1: '',
        other2: '',
        headingColor: 'black',
        subHeadingColor: 'black',
        addressColor: 'black',
        mobileColor: 'black',
        other1Color: 'black',
        other2Color: 'black',
        envelopeWidth: '100',
        envelopeHeight: '100',
        envelopeBorder: '0',
        envelopeNameColor: 'black',
        envelopeBgImage: [],
        previewImage: undefined,
        headingFontSize: 20,
        subHeadingFontSize: 15,
        addressFontSize: 12,
        mobileNumberFontSize: 10,
        other1FontSize: 10,
        other2FontSize: 10,
    }),

    methods: {
        selectFile(image) {
            this.envelopeBgImage = image;
            this.previewImage = URL.createObjectURL(this.envelopeBgImage);
        },
        onResize: function (x, y, width, height) {
            this.x = x
            this.y = y
            this.width = width
            this.height = height
        },
        onDrag: function (x, y) {
            this.x = x
            this.y = y
        },
        saveImage() {
            const node = document.getElementById("imageToSave");
            saveAsJpeg(node, { filename: 'rareprintEnvelope', printDate: false });
        }
    },
    created() {
        console.log(this.headingFontSize);
    }
}
</script>

<style>
.envelope-layout {
    padding: 25px;
    margin: 10px;
}

.form-data {
    border: 1px solid black;
    padding: 10px;
}

.box {
    border: 1px solid black;
    margin: 10px;
}

/* .v-slider {
    background-color: darkgray;
} */

h1 {
    text-align: center;
}

.InnerText {
    position: absolute;
    top: 0;

}

.dragable-style {
    height: 50px;
    width: 500px;
}

.dragable-style:hover {
    border: 1px solid black;
}
</style>
