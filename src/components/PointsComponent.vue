<template>
    <div class="data">
        <div>
            <div class="badge user">User</div>
            <span>{{ playerPoints }}</span>
        </div>
        <div class="division" />
        <div>
            <div class="badge cpu">CPU</div>
            <span>{{ cpuPoints }}</span>
        </div>
    </div>
</template>

<style scoped>
.data {
    display: flex;
    gap: 5px;
    border: 1px solid gray;
    padding: 5px 10px;
    border-radius: 5px;
    justify-content: center;
}

.badge {
    padding: 2px 5px;
    border-radius: 5px;
}

.badge.user {
    background-color: blue;
}

.badge.cpu {
    background-color: red;
}

span {
    font-weight: bold;
    font-size: 1.5rem;

}

.division {
    border: 1px solid gray;
}
</style>

<script>
export default {
    props: {
        playerPoints: Number,
        cpuPoints: Number
    }
}
</script>