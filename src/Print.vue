<template>
    <span ref="toPrint">
        <slot></slot>
    </span>
</template>
<script>
    import axios from 'axios';
    export default {
        install(Vue)
        {
            Vue.component('print',this);
        },
        props: {
            AutoClose: {
                required: false,
                type: Boolean,
                default: true,
            },
            UseManifest: {
                type: Boolean,
                default: true,
            },
            PrintCss: {
                type: String,
                required: false,
                default: '/css/print.css',
            }
        },
        methods: {
            print()
            {
                if(this.UseManifest)
                {
                    axios.get('/mix-manifest.json')
                        .then(manifest => {
                            this.preparePage(manifest.data[this.PrintCss]);
                        })
                        .catch(error => {
                            // couldn't retrieve manifest file. Time to fallback
                            this.preparePage(this.PrintCss);
                        });
                }
                else
                {
                    this.preparePage(this.PrintCss);
                }
            },
            preparePage(css)
            {
                let printCss = new String(`<link href="${css}" rel="stylesheet" type="text/css">`);
                let WinPrint = window.open('','','left=0,top=0,width=800,height=900,toolbar=0,scrollbars=0,status=0');
                WinPrint.document.write( printCss + '<span class="print">' + this.$refs.toPrint.innerHTML + '</span>');
                WinPrint.document.close();
                WinPrint.focus();
                let self = this;
                WinPrint.addEventListener('load', function(){
                    WinPrint.print();
                    
                    if(self.AutoClose === true)
                        WinPrint.close();
                    
                    self.$emit('printClosed');
                }, true);
            }
        }
    }
</script>
<style media="print">
    .print .print-hidden {
        display: none;
    }
</style>
