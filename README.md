# laramix-vue-tinymce-5
Self hosted TinyMCE ^5.0.8 for Vue ^2.6.10 using Laravel Mix ^4.0.15

This setup method works when used with `modals` and `v-if` directive.

# Installation

```sh
yarn add --dev tinymce
```

### Configure Webpack

> Don't bother trying to use ES5/6 imports, it simply does not work very well, you will get resource errors.

In `webpack.mix.js` add:

```javascript
mix
    .copy('node_modules/tinymce/tinymce.min.js', 'public/js/tinymce.min.js')
    .copy('node_modules/tinymce/themes/silver/theme.min.js', 'public/js/themes/silver/theme.min.js')
    .copy('node_modules/tinymce/skins/content/default/content.min.css','public/js/skins/content/default/content.min.css')
    .copy('node_modules/tinymce/skins/ui/oxide/content.min.css','public/js/skins/ui/oxide/content.min.css')
```

### Load TinyMCE

Use blade script push or add `<script src="/js/tinymce.min.js"></script>` where TinyMCE is needed.

```blade
@push('scripts')
    <script src="/js/tinymce.min.js"></script>
@endpush
```

### Add Vue Helper

Place copy `components/helpers/v-editor` from this repository into your project.

Register globally:

```javascript
import vEditor from "../components/helpers/v-editor"
Vue.component('v-editor', vEditor);
```

Or register in a component: 

```javascript
import vEditor from "../components/helpers/v-editor"
    export default {

        components: { vEditor },
       
        ...
    }
```

### How to use

To use in your template:

```javascript
<v-editor v-model="description"></v-editor>
```

Done.

### How to configure init options

When following the offcial [guide](https://www.tiny.cloud/docs/general-configuration-guide/basic-setup), the `tinymce.init({})` options object can be set as a property of `v-editor`.

```javascript
<v-editor v-model="input.description" :options="{ inline: true }"></v-editor>
```

Here is a full example in use inside a [VuetifyJS](https://vuetifyjs.com) `v-dialog`:

```javascript

<template>

    <v-dialog v-if="display" v-model="display" width="720" persistent>

        <v-card>

            <v-toolbar card dark color="primary">

                <v-toolbar-title>Example</v-toolbar-title>

                <v-spacer></v-spacer>

                <v-btn icon color="error" @click="close" title="Close">
                    <v-icon>mdi-close</v-icon>
                </v-btn>

            </v-toolbar>

            <v-container>

                <v-form>

                    <v-editor v-model="input.description" :options="editorOptions"></v-editor>

                </v-form>

            </v-container>

        </v-card>

    </v-dialog>

</template>

<script>

    import VEditor from "../../components/helpers/v-editor";

    export default {

        components: {VEditor},

        data: () => ({

            display: false,

            input: {
            
                description: '<p>Content of the editor.</p>'

            },

            editorOptions: {

                inline: true

            }

        }),

        methods: {
        
            close() {

                Object.assign(this.$data, this.$options.data());

            }

        }

    }

</script>

```
