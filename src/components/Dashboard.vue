<template>
 
</template>

<script>
import draggable from "vuedraggable";

export default {
  name: "Dashboard",
  components: {
    draggable
  },
  data: function() {
  return {
      dragActive: false,
      nextFilter: HTMLElement,
      abonnements: [
        {
          name: "Netflix",
          price: 10.0,
          interval: "monthly"
        },
        {
          name: "Spotify",
          price: 10.0,
          interval: "monthly"
        },
        {
          name: "VPN Express",
          price: 12.0,
          interval: "monthly"
        }
      ],
      tagFilter: [
        { tags: ["expense", "income", "sanitary", "party", "food"] },
        { tags: [] }
      ]
    };
  },
  mounted() {
      this.nextFilter = this.$el.querySelector(".noOpacity");
  },
  methods: {
    onStart: function() {
      this.dragActive = true;
      this.nextFilter.classList.remove("noOpacity");
      this.nextFilter.classList.add("lowOpacity");
    },
    onEnd: function() {
      this.dragActive = false;
      if (this.nextFilter.children.length > 0) {
        this.tagFilter.push({ tags: [] });
      } else {
        this.nextFilter.classList.remove("lowOpacity");
        this.nextFilter.classList.add("noOpacity");
      }
      this.tagFilter = this.tagFilter.filter((tf, i) => tf.tags.length > 0 || i == this.tagFilter.length - 1);
      setTimeout(() => {
        if (this.$el.querySelector(".noOpacity") != null) {
          this.nextFilter = this.$el.querySelector(".noOpacity");
        }
        console.log(this.tagFilter);
        console.log(this.nextFilter);
      })
    },

    onMove: function(event) {
      console.log(event);
      if (event.dragged.children[0].classList.contains("noOpacity")) {
        return false
      }
      
      if (!this.dragActive) {
        return
      }
      if (event.to == this.nextFilter) {
        this.nextFilter.classList.remove("lowOpacity");
      } else {
        this.nextFilter.classList.add("lowOpacity");
      }   
    }
  },
};
</script>

<style scoped>
.fCards {
  margin-bottom: 10px;
}

.tagContainer {
  min-width: 30px;
  min-height: 80px;
  background-color: bisque;
  opacity: 1;
}

.filterContainer {
width: 100%;
}

.flip-list-move {
  transition: transform 0.5s;
}

.ghost {
  opacity: 0.5;
  background: #c8ebfb;
}

.fade-enter-active,
.fade-leave-active {
  transition: all 0.2s;
}
.fade-enter,
.fade-leave-to {
  opacity: 0;
}
.fade-enter-active {
  transition-delay: 0.2s;
}
.lowOpacity {
  opacity: 0.5 !important;
}

.noOpacity {
  opacity: 0 !important;
}
</style>