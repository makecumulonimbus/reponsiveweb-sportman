<template>
  <div class="container-page">
    <div v-for="(contentItem, index) in contentData" :key="`content-` + index">
      <ContentCard
        :titleName="contentItem.TitleName"
        :image="contentItem.image"
        :positionSection="contentItem.positionSection"
        :section="contentItem.section"
      />
    </div>
  </div>
</template>

<script>
export default {
  name: "MainPage",
  data() {
    return {
      contentData: [
        {
          TitleName: "ATHLETS",
          image: "sportsperson-1.svg",
          positionSection: "right",
          section: [
            {
              title: "CONNECTION",
              detail:
                "Connect with coaches directly, you can ping coaches to view profile.",
              customBg: "#FFFFFF",
            },
            {
              title: "COLLABORATION",
              detail:
                "Work with other student athletes to increase visability. When you share and like other players videos it will increase your visability as a player. This is the team work aspect to Surface 1.",
              customBg: "#F5F4F9",
            },
            {
              title: "GROWTH",
              detail:
                "Resources and tools for you to get better as a student Athelte. Access to training classes, tutor sessions, etc",
              customBg: "#5E3DB3",
              detailColor: "#FFFFFF",
              underLineColor: "#FFFFFF",
            },
          ],
        },
        {
          TitleName: "PLAYERS",
          image: "sportsperson-2.svg",
          positionSection: "left",
          section: [
            {
              title: "CONNECTION",
              detail:
                "Connect with talented athlete directly, you can watch their skills through video showreels directly from Surface 1.",
              customBg: "#FFFFFF",
            },
            {
              title: "COLLABORATION",
              detail:
                "Work with recruiter to increase your chances of findingtalented athlete.",
              customBg: "#F5F4F9",
            },
            {
              title: "GROWTH",
              detail: "Save your time, recruit proper athlets for your team.",
              customBg: "#090C35",
              detailColor: "#FFFFFF",
              customNumber: true,
              underLineColor: "#FFFFFF",
            },
          ],
        },
      ],
    };
  },
};
</script>