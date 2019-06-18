<template>

    <div></div>

</template>

<script>

    export default {

        name: 'v-editor',

        props: ['value'],

        data: () => ({

            instance: null

        }),

        mounted() {

            let self = this;

            if(self.instance == null) {

                window.tinyMCE.init({

                    target: self.$el

                }).then(instance => {

                    self.instance = instance[0];

                    self.instance.setContent(self.value);

                    self.instance.on('Change keyup', () => {

                        self.$emit('input', self.instance.getContent());

                    });

                });

            }

        },

        beforeDestroy () {

            if(this.instance != null) {

                this.instance.destroy();

            }

        }

    }

</script>
