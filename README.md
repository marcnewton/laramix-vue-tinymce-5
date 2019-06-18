# laramix-vue-tinymce-5
Self hosted TinyMCE ^5.0.8 for Vue ^2.6.10 using Laravel Mix ^4.0.15

> Don't bother trying to use ES5/6 imports, it simply does not work, other solutions do not work in `modals` or `v-if` directives.

This setup method works when used with `modals` and `v-if` directive.

# Installation

```sh
yarn add --dev tinymce
```

In `webpack.mix.js` add:

```javascript
mix
    .copy('node_modules/tinymce/tinymce.min.js', 'public/js/tinymce.min.js')
    .copy('node_modules/tinymce/themes/silver/theme.min.js', 'public/js/themes/silver/theme.min.js')
    .copy('node_modules/tinymce/skins/content/default/content.min.css','public/js/skins/content/default/content.min.css')
    .copy('node_modules/tinymce/skins/ui/oxide/content.min.css','public/js/skins/ui/oxide/content.min.css')
```

Use blade script push or add `<script src="/js/tinymce.min.js"></script>` where TinyMCE is needed.

```blade
@push('scripts')
    <script src="/js/tinymce.min.js"></script>
@endpush
```

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

To use in your template:

```javascript
<v-editor v-model="description"></v-editor>
```

Done.
