<template>
    <div class="wrap">
            {{ unread.data.messageTime.date }}
    </div>
</template>

<script>

    export default {
        props:['unread']
    }
</script>
