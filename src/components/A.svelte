<script>
    export let href;
</script>

<a {href} 
    class="flex items-center justify-center text-black hover:text-white bg-gray-200 border-0 px-8 focus:outline-none hover:bg-gray-600 rounded ">
        <slot />
</a>