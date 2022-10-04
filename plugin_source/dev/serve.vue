<script lang="ts">

import { defineComponent } from "vue";
import AccordionSection from "../src/AccordionSection.vue";

export default defineComponent({
  name: "ServeDev",
  components: { AccordionSection },
});
</script>

<template>
  <div id="app">
    <accordion-section 
        data_source_type="url"
        data_source_location="http://americansjewelry.com/libraries/local-php-api/index.php/"
        monitored_object_id="AnonymousIdentity_1669">
    </accordion-section>
  </div>
</template>
