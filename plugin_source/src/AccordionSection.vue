/* eslint-disable prettier/prettier */
<template>
    <div>
        <button class="accordion" id="{{ this.accordion_color }}"><strong>{{ this.monitored_object_id }}</strong>&nbsp;&nbsp;&nbsp;&nbsp;
            <span id="{{ accordion_text }}"></span>
        </button>
        <div class="panel">
            <div id="log-accordion-anonymous-identity-1669">
                <monitored-object 
                    data_source_type="url"
                    data_source_location="http://mycustombusinessapp.com/wp-content/plugins/MCBA-Wordpress/runQuery.php"
                    object_id="AnonymousIdentity_1669">
                </monitored-object>
            </div>
        </div>
    </div>
</template>

<script lang="ts">
import ServerLedData from "../src/typescript_source/concrete/ServerLedData";
import { defineComponent } from "vue";
export default defineComponent( {
    name: "accordion-section",    
    props: {
        monitored_object_id:  { type: String, default: "" },
        data_source_type:     { type: String, default: "" },
        data_source_location: { type: String, default: "" }},    
    data: () => ({ 
        monitor_led_data: new ServerLedData(),
        led_listen_event: "",  accordion_color: "", accordion_text: "", kebob_name: "", numeral_id: "", accordion_id: ""
    }),
    mounted() {
        let name_split = this.monitored_object_id.split( "_" );
        this.numeral_id = name_split[ 1 ];
        this.kebob_name = this.kebabize( name_split[ 0 ] );
        this.accordion_id = this.kebob_name + "-" + this.numeral_id;
        this.led_listen_event = "event-" + this.kebob_name + "-" + this.numeral_id;
        this.accordion_color = "accordion-color-" + this.kebob_name + "-" + this.numeral_id;
        this.accordion_text  = "accordion-text-"  + this.kebob_name + "-" + this.numeral_id;
        document.addEventListener( this.led_listen_event,  ( event ) => {
            let accordion_background_color = document.getElementById( this.accordion_color );
            if ( !accordion_background_color ) { throw( Error( "*** ERROR: element not defined! ***" )) }
            console.log( "*** accordion-section.vue: event received: " + this.led_listen_event );
            let accordion_text = document.getElementById( this.accordion_text);
            if ( !accordion_text ) { throw( Error( "*** ERROR: element not defined! ***" )) }
            console.log( accordion_text, event );
        });
    },
    methods: {
        start() { console.log( "*** accordion-section.vue: start() ***" ); },
 
        kebabize( str: string ) {
            return str.split('').map((letter, idx) => {
                return letter.toUpperCase() === letter
                ? `${idx !== 0 ? '-' : ''}${letter.toLowerCase()}`
                : letter;
        }).join(''); }
    }
});
</script>

<style scoped>
    :host {
        display: block;
        border: solid 1px gray;
        padding: 16px;
        max-width: 800px;
    }
    .accordion {
        background-color: #eee;
        color: #444;
        cursor: pointer;
        padding: 18px;
        width: 100%;
        border: none;
        text-align: left;
        outline: none;
        font-size: 15px;
        transition: 0.4s;
    }
    .active,
    .accordion:hover {
        background-color: #ccc;
    }
    .panel {
        padding: 0 18px;
        display: none;
        background-color: white;
        overflow: hidden;
    }
</style>
