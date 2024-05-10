<template>
    <div class="h-1">  
        <!-- Add this for control and eable to resize in this region -->
    </div>
    <div class="flex" style="-webkit-app-region: drag;">
        <div class="flex" style="-webkit-app-region: no-drag;">
            <button>
                <MenuSvg class="w-8 h-8"/>
            </button>
            <div class="ml-auto">
                <button>minize</button>
                <button>maximize</button>
                <button>close</button>
            </div>
        </div>
    </div>
</template>

<script>
import MenuSvg from '@/components/svg/MenuSvg.vue';

export default {
    name: 'AppBar',
    components: {
      MenuSvg
    },
    methods: {
    }
}
</script>