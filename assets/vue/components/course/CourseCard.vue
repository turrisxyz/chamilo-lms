<template>
  <v-card
      v-if="course"
      elevation="4"
  >
    <div class="">
      <img class="object-cover w-full h-44" :src="course.illustrationUrl" />
    </div>
    <div class="p-4">
      <div class="h-10 flex flex-row justify-between">
        <div class="line-clamp-2 text-md w-5/6">
          <router-link :to="{ name: 'CourseHome', params: {id: course._id, course: course}, query: { sid: sessionId } }">
            <span v-if="session">
              {{ session.name }} -
            </span>
            {{ course.title }}
          </router-link>
        </div>
        <div>
          <v-icon icon="mdi-dots-vertical" />
        </div>
      </div>

      <div v-if="course.users" class="pt-6">
        <div class="flex flex-row" v-if="course.users.edges.length">
          <div class="flex flex-row pr-3" v-for="courseRelUser in course.users.edges">
            <div class="pr-2">
                <img class="inline-block h-8 w-8 rounded-full ring-2 ring-white"
                     :src="courseRelUser.node.user.illustrationUrl + '?w=80&h=80&fit=crop'"
                     alt=""
                />
            </div>
            <div v-if="course.users.edges.length < 3 " class="flex-col">
              <div>
              {{ courseRelUser.node.user.firstname }} {{ courseRelUser.node.user.lastname }}
              </div>
            </div>
          </div>
        </div>
      </div>
<!--    <q-card-actions>-->
<!--        <q-btn-->
<!--            type="a"-->
<!--            :to="{ name: 'CourseHome', params: {id: course.id, course: course}}"-->
<!--            text-color="white"-->
<!--            color="primary"-->
<!--            label="Go"-->
<!--        />-->
<!--      </q-card-actions>-->

    </div>
  </v-card>
</template>

<style scoped>
.my-card {
  width: 100%;
  max-width: 370px;
}
</style>
<script>

export default {
  name: 'CourseCard',
  props: {
    course: Object,
    session: Object,
    sessionId: {
      type: Number,
      required: false,
      default: 0
    }
  },
  data() {
    return {
    };
  },
  methods: {
  }
};
</script>
