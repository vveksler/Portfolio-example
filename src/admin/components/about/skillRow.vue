<template lang="pug">
  tr.skill__row(
    :class="{ 'skill__row--edit': editMode }"
  )
    td.skill__col.skill__col--title
      input(type="text" placeholder="Новый навык" v-model="editedSkill.title").skill__input.skill__input--table.skill__input--title
    td.skill__col.skill__col--percent
      .skill__percent-block
        input(type="text" placeholder="100" v-model="editedSkill.percent").skill__input.skill__input--table.skill__input--percent
        span.skill__percent-prefix %
    td.skill__col.skill__col--btns
      .skill__btns-block
        .skill__edit-mode-btns
          button(
            type='button'
            @click="editCurrentSkill"
          ).btn.btn--save-skill
          button(
            type='button'
            @click="removeCurrentSkill"
          ).btn.btn--remove-skill
        .skill__read-mode-btns
          button(
            type='button'
            @click="editMode = true"
          ).btn.btn--edit-skill
          button(
            type='button'
            @click="removeCurrentSkill"
          ).btn.btn--trash-skill

</template>

<script>
import { mapActions, mapMutations } from "vuex";

export default {
  props: {
    skill: Object
  },
  data() {
    return {
      editMode: false,
      editedSkill: { ...this.skill }
    };
  },
  methods: {
    ...mapActions("skills", ["removeSkill", "editSkill"]),
    ...mapMutations("tooltip", ["SHOW_TOOLTIP"]),

    async removeCurrentSkill() {
      try {
        const {
          data: { message }
        } = await this.removeSkill(this.skill.id);
        this["SHOW_TOOLTIP"]({
          type: "success",
          text: message
        });
      } catch (error) {
        console.error(error.message);
        this["SHOW_TOOLTIP"]({
          type: "error",
          text: "Произошла ошибка при удалении навыка"
        });
      }
    },

    async editCurrentSkill() {
      try {
        const {
          data: { message }
        } = await this.editSkill(this.editedSkill);

        this["SHOW_TOOLTIP"]({
          type: "success",
          text: message
        });
        this.editMode = false;
      } catch (error) {
        console.error(error.message);
        this["SHOW_TOOLTIP"]({
          type: "error",
          text: 'Произошла ошибка'
        });
      }
    }
  }
};
</script>


<style lang="postcss" scoped>
@import "../../../styles/mixins.pcss";
@import "./styles/skill.pcss";

.skill__input {
  pointer-events: none;
}
</style>
