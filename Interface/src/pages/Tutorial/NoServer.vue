<template>
  <div :class="{ mobile: isMobilePage }">
    <h1>{{ $t("tutorial.noserver.title") }}</h1>
    <slot></slot>
    <Card padded id="server-setup">
      <div v-if="activeIndex == 1" id="options">
        <h2>{{ $t("tutorial.noserver.needServer") }}</h2>
        <p id="option-info">{{ $t("tutorial.noserver.optionInfo") }}</p>
        <div id="self-setup">
          <div class="option">
            <a href="/docs/setup" target="_blank" rel="noopener noreferrer">
              <Button id="no" empty>
                {{
                $t("tutorial.noserver.selfSetup.goToDocs")
                }}
              </Button>
            </a>
            <ul class="option-infos">
              <li>{{ $t("tutorial.noserver.selfSetup.returnHere") }}</li>
            </ul>
          </div>
        </div>
      </div>
    </Card>
  </div>
</template>

<script>
import Button from "../../components/Button";
import Card from "../../components/Card";

export default {
  components: { Button, Card },
  data() {
    return {
      ip: [undefined, undefined, undefined, undefined],
      port: undefined
    };
  },
  computed: {
    activeIndex() {
      return this.$route.meta.activeIndex;
    },
    isMobilePage() {
      return this.$store.state.websiteBeingViewedOnMobileDevice;
    }
  }
};
</script>

<style lang="scss" scoped>
h1 {
  text-align: center;
}
#server-setup {
  margin-top: calc(#{$spacing-large} * 2);
  #options {
    & #option-info {
      margin-bottom: $spacing-large;
    }

    & .option {
      & .option-infos {
        margin-top: $spacing-medium;
        & li {
          list-style-type: disc;
          list-style-position: inside;

          &::marker {
            color: $secondary;
          }
        }
      }
    }
  }
}
</style>
