<template>
  <div class="content-card-container">
    <div class="row-content">
      <div
        :class="
          positionSection === 'left'
            ? 'display-content-left'
            : 'display-content-right'
        "
      >
        <div class="title-content">
          <div class="name">{{ titleName }}</div>
        </div>

        <div class="image-content" :class="screenSize">
          <div class="image-box">
            <img :src="`/images/` + screenSize + '-' + image" />
          </div>
        </div>

        <div v-if="screenSize === 'mobile'" class="mobile-section-content">
          <v-carousel :show-arrows="false" height="auto">
            <v-carousel-item
              v-for="(sectionItem, index) in section"
              :key="`section-mb-` + index"
              class="carousel-item-custom"
            >
              <div
                class="title-section"
                :class="sectionItem.customNumber && 'custom-number'"
              >
                <div class="box-underline">
                  <span class="number-title">{{ getNumberTitle(index) }}</span>
                  <div class="underline"></div>
                </div>
                <div class="text-title ml-2">
                  {{ sectionItem.title }}
                </div>
              </div>
              <div class="detail-section">
                {{ sectionItem.detail }}
              </div>
            </v-carousel-item>
          </v-carousel>
        </div>

        <div v-else>
          <div
            class="section-content"
            v-for="(sectionItem, index) in section"
            :key="`section-` + index"
            :style="`background-color:${sectionItem.customBg};`"
          >
            <div
              class="container-content"
              :class="positionSection === 'left' ? 'left' : 'right'"
            >
              <div
                class="title-section"
                :class="sectionItem.customNumber && 'custom-number'"
              >
                <div class="mt-n3">
                  <span class="number-title">{{ getNumberTitle(index) }}</span>
                  <div
                    class="underline"
                    :style="`background-color: ${sectionItem.underLineColor}`"
                  ></div>
                </div>
                <div class="text-title ml-2">
                  {{ sectionItem.title }}
                </div>
              </div>
              <div
                class="detail-section"
                :style="
                  sectionItem.detailColor
                    ? `color: ${sectionItem.detailColor};`
                    : ''
                "
              >
                {{ sectionItem.detail }}
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "ContentCard",
  props: {
    titleName: { type: String, default: "" },
    image: { type: String, default: "" },
    section: { type: Array, default: [] },
    positionSection: { type: String, default: "left" },
  },
  data() {
    return {
      screenSize: "mobile",
    };
  },

  mounted() {
    this.onResize();
    window.addEventListener("resize", this.onResize);
  },

  destroyed() {
    window.removeEventListener("resize", this.onResize);
  },

  methods: {
    onResize() {
      if (window.innerWidth >= 1920) {
        this.screenSize = "desktop";
      } else if (window.innerWidth >= 768) {
        this.screenSize = "tablet";
      } else {
        this.screenSize = "mobile";
      }
    },

    getNumberTitle(index) {
      const formatNumber = ("0" + String(index + 1)).slice(-2);
      return formatNumber;
    },
  },
};
</script>

<style lang="scss" scoped>
.row-content {
  .title-content {
    padding: 0px 20px;
    font-size: 50px;
    color: #e7e7e7;
  }
  .image-content.mobile {
    display: flex;
    justify-content: center;
    .image-box {
      margin: 23px 0px;
      z-index: 2;
    }
  }
  .mobile-section-content {
    margin-top: -85px;
  }
  .carousel-item-custom {
    padding: 75px 20px 20px;
    background-color: #f5f4f9;
  }
  .title-section {
    font-size: 28px;
    line-height: 42.19px;
    letter-spacing: 1.5px;
    color: #c2c2c2;
    display: flex;
    margin-bottom: 18px;
    .box-underline {
      margin-top: -10px;
    }
    .number-title {
      font-size: 14px;
      line-height: 21.09px;
      letter-spacing: 1.5px;
      color: #000000;
    }
    .underline {
      width: 100%;
      height: 5px;
      background-color: #603ebe;
      border-radius: 5px;
      margin-top: -2px;
    }
    &.custom-number {
      .number-title {
        color: #8f6be8;
      }
    }
  }
  .detail-section {
    font-size: 15px;
    line-height: 28px;
    color: #000000;
  }
}
::v-deep .v-carousel__controls {
  background: transparent;
  margin-bottom: 20px;
  button {
    height: 10px !important;
    width: 10px !important;
    color: #d8d8d8 !important;
    &.v-btn--active {
      color: #5c3caf !important;
      &::before {
        opacity: 0 !important;
      }
    }
    .v-icon {
      opacity: 1 !important;
    }
  }
}
::v-deep .v-carousel__item {
  padding-bottom: 60px !important;
}

@media only screen and (min-width: $tablet-breakpoint) {
  .row-content {
    position: relative;
    .display-content-left {
      .title-content {
        padding: 20px 40px 0px;
        .name {
          max-width: 1500px;
          margin: auto;
          width: 100%;
          font-size: 90px;
          margin-top: 50px;
        }
      }
      .image-content {
        width: 100%;
        max-width: 1300px;
        margin: auto;
        position: relative;
        img {
          position: absolute;
          top: -125px;
          right: -240px;
        }
      }
    }
    .display-content-right {
      .title-content {
        .name {
          max-width: 1500px;
          margin-left: 38%;
          font-size: 90px;
          margin-top: 50px;
        }
      }
      .image-content {
        width: 100%;
        max-width: 1300px;
        margin: auto;
        position: relative;
        img {
          position: absolute;
          top: -100px;
          left: -150px;
        }
      }
    }
  }

  .section-content {
    padding: 40px;
    .container-content {
      &.left {
        max-width: 1500px;
        margin: auto;
      }
      &.right {
        max-width: 1500px;
        margin-left: 38%;
        .detail-section {
          max-width: 100%;
        }
      }
      .title-section {
        font-size: 36px;
        margin-bottom: 18px;
        .number-title {
          font-size: 18px;
        }
      }
      .detail-section {
        max-width: 75%;
        font-size: 18px;
      }
    }
  }
}

@media only screen and (min-width: $desktop-breakpoint) {
  .row-content {
    position: relative;
    .display-content-left {
      .title-content {
        padding: 100px 0px 0px;
        font-size: 90px;
        .name {
          max-width: 1500px;
          margin: auto;
          width: 100%;
          margin-top: 0px;
        }
      }
      .image-content {
        width: 100%;
        max-width: 2000px;
        margin: auto;
        position: relative;
        img {
          position: absolute;
          top: -235px;
          right: 0;
          padding-right: 100px;
          padding-top: 0px;
        }
      }
    }
    .display-content-right {
      .title-content {
        padding: 0px 0px;
        .name {
          max-width: 1500px;
          margin-left: 50%;
          margin-top: 0px;
        }
      }
      .image-content {
        width: 100%;
        max-width: 2000px;
        margin: auto;
        position: relative;
        img {
          position: absolute;
          top: -190px;
          left: 0;
          padding-left: 100px;
          padding-top: 60px;
        }
      }
    }

    .section-content {
      padding: 60px;
      .container-content {
        &.left {
          max-width: 1500px;
          margin: auto;
        }
        &.right {
          max-width: 1500px;
          margin-left: 50%;
        }
        .title-section {
          font-size: 36px;
          margin-bottom: 25px;
          .number-title {
            font-size: 18px;
          }
        }
        .detail-section {
          max-width: 75%;
          font-size: 20px;
        }
      }
    }
  }
}
</style>
