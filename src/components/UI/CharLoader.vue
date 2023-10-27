<template>
    <div class="lds-ellipsis-container">
        <div class="lds-ellipsis">
            <div></div>
            <div></div>
            <div></div>
            <div></div>
        </div>
    </div>
</template>

<script>
export default {

}
</script>

<style scoped>
.lds-ellipsis-container {
    position: relative;
    width: 100%; /* Ширина 100% для центрирования по горизонтали */
    height: 100vh; /* Высота 100vh для центрирования по вертикали */
}

.lds-ellipsis {
    position: absolute;
    top: 50%; /* Положение по вертикали в середине */
    left: 50%; /* Положение по горизонтали в середине */
    transform: translate(-50%, -50%); /* Центрирование */
    width: 80px;
    height: 80px;
}

.lds-ellipsis div {
    position: absolute;
    top: 33px;
    width: 18px;
    height: 18px;
    border-radius: 50%;
    background: #99F538AD;
    animation-timing-function: cubic-bezier(0, 1, 1, 0);
}

.lds-ellipsis div:nth-child(1) {
    left: 8px;
    animation: lds-ellipsis1 0.6s infinite;
}

.lds-ellipsis div:nth-child(2) {
    left: 8px;
    animation: lds-ellipsis2 0.6s infinite;
}

.lds-ellipsis div:nth-child(3) {
    left: 32px;
    animation: lds-ellipsis2 0.6s infinite;
}

.lds-ellipsis div:nth-child(4) {
    left: 56px;
    animation: lds-ellipsis3 0.6s infinite;
}

@keyframes lds-ellipsis1 {
    0% {
        transform: scale(0);
    }

    100% {
        transform: scale(1);
    }
}

@keyframes lds-ellipsis3 {
    0% {
        transform: scale(1);
    }

    100% {
        transform: scale(0);
    }
}

@keyframes lds-ellipsis2 {
    0% {
        transform: translate(0, 0);
    }

    100% {
        transform: translate(24px, 0);
    }
}

</style>