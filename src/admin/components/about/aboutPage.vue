<template lang="pug">
  section.section.about
    .container.about__container
      .heading-row.about__heading-row
        h1.title.about__title Блок «Обо мне»
        button(
          type='button'
          @click="showAddingForm = true"
        ).btn.btn--add-skills-group Добавить группу
      .about__cards
        skill-cards(
          :showAddingForm="showAddingForm"
          @closeNewSkillCard="showAddingForm = false"
        )
          
</template>

<script>
import { mapState } from 'vuex';
export default {
  components: {
    skillCards: () => import("components/about/skillCards.vue")
  },
  data() {
    return {
      showAddingForm: false
    };
  }
};
</script>


<style lang="postcss" scoped>
@import "../../../styles/mixins.pcss";

.about {
  grid-area: content-area;
  background-image: linear-gradient(rgba(#fff, 0.9), rgba(#fff, 0.9)),
    url("~images/bg/mountain-baloon.jpg");
  background-position: center center, center center;
  background-repeat: repeat, no-repeat;
  background-size: cover, cover;
  /* min-height: 100vh; */
}

.about__container {
  @include phones {
    margin: 0;
    width: 100%;
  }
}

.about__heading-row {
  display: flex;
  align-items: center;

  @include phones {
    flex-direction: column;
    align-items: flex-start;
  }
}

.about__title {
  margin-right: 60px;

  @include phones {
    margin-right: 0;
    margin-bottom: 8%;
  }
}
</style>
