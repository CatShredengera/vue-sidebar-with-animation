<script>
import { computed } from 'vue';
import { RouterLink, useRoute } from 'vue-router';
import { collapsed } from './state';

export default {
    props: {
        to: { type: String, required: true },
        icon: { type: String, required: true }
    },
    setup(props) {
        const router = useRoute();
        const isActive = computed(() => router.path === props.to);
        return { isActive, collapsed };
    },
    components: { RouterLink }
}
</script>

<template>
    <RouterLink :to="to" class="link" :class="{ 'active': isActive }">
        <i class="icon" :class="icon" />
        <Transition name="fade">
            <span v-if="!collapsed">
                <slot />
            </span>
        </Transition>
    </RouterLink>
</template>

<style scoped>
.fade-enter-active,
.fade-leave-active {
    transition: opacity .1s;
}

.fade-enter,
.fade-leave-to {
    opacity: 0;
}

.link {
    display: flex;
    align-items: center;

    cursor: pointer;
    position: relative;
    font-weight: 400;
    user-select: none;

    margin: .1em 0;
    padding: .4em;
    border-radius: .25em;
    height: 1.5em;

    color: white;
    text-decoration: none;
}

.link:hover {
    background-color: var(--sidebar-item-hover);
}

.link.active {
    background-color: var(--sidebar-item-active);
}

.link .icon {
    flex-shrink: 0;
    width: 25px;
    margin-right: 10px;
}
</style>  