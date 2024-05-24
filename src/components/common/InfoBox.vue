<template>
  <div>
    <!-- <div id="info">Posição do Cursor: <span>{{ mouseX }}, {{ mouseY }}</span></div> -->
    <div v-if="id && title" id="followSquare"><b>{{ id }}</b><br>{{ title }}</div>
    <div v-if="id && title" id="followTriangle"></div>
    <div v-if="id && title" id="followTriangleWhite"></div>
  </div>
</template>

<script>
import { ref, onMounted, toRefs } from 'vue';

export default {
  props: {
    id: String,
    title: String
  },
  setup(props) {
    const { id, title } = toRefs(props);
    const mouseX = ref(0);
    const mouseY = ref(0);

    const updateMousePosition = (event) => {
      mouseX.value = event.clientX;
      mouseY.value = event.clientY;
      if (id.value && title.value) {
        updateSquarePosition(event);
        updateTrianglePosition(event);
        updateTriangleWhitePosition(event);
      }
    };

    const updateSquarePosition = (event) => {
      let followSquare = document.getElementById('followSquare');
      if (followSquare) {
        followSquare.style.left = (event.clientX - (followSquare.offsetWidth / 2)) + 'px';
        followSquare.style.top = (event.clientY - (followSquare.offsetHeight + 15)) + 'px';
      }
    };

    const updateTrianglePosition = (event) => {
      let followTriangle = document.getElementById('followTriangle');
      if (followTriangle) {
        followTriangle.style.left = (event.clientX - (followTriangle.offsetWidth / 2)) + 'px';
        followTriangle.style.top = (event.clientY - (followTriangle.offsetHeight * 2)) + 'px';
      }
    };

    const updateTriangleWhitePosition = (event) => {
      let followTriangleWhite = document.getElementById('followTriangleWhite');
      if (followTriangleWhite) {
        followTriangleWhite.style.left = (event.clientX - (followTriangleWhite.offsetWidth / 2)) + 'px';
        followTriangleWhite.style.top = (event.clientY - (followTriangleWhite.offsetHeight * 3)) + 'px';
      }
    };

    onMounted(() => {
      document.addEventListener('mousemove', updateMousePosition);
    });

    return {
      mouseX,
      mouseY,
    };
  }
};
</script>

<style scoped>
#info {
  position: fixed;
  top: 10px;
  left: 10px;
  background-color: #fff;
  padding: 10px;
  border: 1px solid #ccc;
}

#followSquare {
  color: white;
  padding: 5px 30px;
  background-color: #111;
  border-radius: 3px;
  position: fixed;
  text-align: center;
}

#followTriangle {
  width: 0;
  height: 0;
  border-left: 8px solid transparent;
  border-right: 8px solid transparent;
  border-top: 8px solid #111;
  position: fixed;
}

#followTriangleWhite {
  width: 0;
  height: 0;
  border-left: 5px solid transparent;
  border-right: 5px solid transparent;
  border-top: 5px solid #fff;
  position: fixed;
}
</style>
