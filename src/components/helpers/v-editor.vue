<template>

    <div></div>

</template>

<script>

    export default {

        name: 'v-editor',

        props: ['value'],

        data: () => ({

            instance: null,
            timeout: null,

        }),

        mounted() {

            let self = this;

            if(self.instance == null || self.instance.destroyed) {

                self.timeout = setTimeout(function () {

                    window.tinyMCE.init({

                        target: self.$el

                    }).then(instance => {

                        self.instance = instance[0];

                        self.instance.setContent(self.value);

                        self.instance.on('Change keyup', () => {

                            self.$emit('input', self.instance.getContent());

                        });

                    });

                }, 500);

            }

        },

        beforeDestroy () {

            if(this.timeout != null) {

                clearTimeout(this.timeout);

            }

            if(this.instance != null) {

                this.instance.destroy();
                this.$el.innerHTML = '';

            }

        }

    }

</script>
