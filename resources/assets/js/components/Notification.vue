<template>
    <li class="dropdown" id="markasread">
        <a href="#" class="dropdown-toggle" data-toggle="dropdown" role="button" aria-expanded="false">
            Notifications <span class="badge">{{ unreadNotifications.length }}</span>
        </a>

        <ul class="dropdown-menu" role="menu">
            <li>
                <notification-item v-for="unread in unreadNotifications" :unread='unread' :key="unread.id"></notification-item>
            </li>
        </ul>
    </li>
</template>

<script>
    import NotificationItem from './NotificationItem.vue';
    export default {
        props:['unreads','userid'],
        components:{NotificationItem},
        data(){
            return {
                unreadNotifications: this.unreads
            }
        },
        mounted() {
            console.log('Component mounted.')
            Echo.private('App.User.' + this.userid)
                .notification((notification) => {
                    console.log(notification);
                    let newUnreadNotification = {data:{messageTime:notification.messageTime,user:notification.user}};
                    this.unreadNotifications.push(newUnreadNotification);
                });            
        }
    }
</script>
