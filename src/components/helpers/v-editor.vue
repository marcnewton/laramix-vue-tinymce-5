<template>

    <div></div>

</template>

<script>

    export default {

        name: 'v-editor',

        props: {

            value: {
                type: String,
                default: () => (''),
            },

            options: {
                type: Object,
                default: () => ({})
            }

        },

        data: () => ({

            instance: null

        }),

        mounted() {

            let self = this;

            if (self.instance == null) {

                const defaults = {
                    target: self.$el
                };

                window.tinyMCE
                    .init({...defaults, ...self.options})
                    .then(instance => {

                        self.instance = instance[0];

                        self.instance.setContent(self.value);

                        self.instance.on('Change keyup', () => {

                            self.$emit('input', self.instance.getContent());

                        });

                    });

            }

        },

        beforeDestroy() {

            if (this.instance != null) {

                this.instance.destroy();

            }

        }

    }

</script>
