<template>
  <omegaup-popup
    v-bind:reviewer-nomination="true"
    v-bind:possible-tags="PROBLEM_CATEGORIES"
    v-on:submit="$emit('submit', tag, qualitySeal)"
  >
    <template slot="link-title">
      {{ T.reviewerNomination }}
    </template>
    <template slot="popup-content" slot-scope="slotProps">
      <div class="title-text">
        {{ T.reviewerNominationFormTitle }}
      </div>
      <div class="form-group">
        <label class="control-label">
          {{ T.reviewerNominationQuality }}
        </label>
        <br />
        <omegaup-radio-switch
          v-bind:value.sync="qualitySeal"
          v-bind:selected-value="qualitySeal"
        ></omegaup-radio-switch>
      </div>
      <div class="form-group">
        <label class="control-label">
          {{ T.reviewerNominationCategory }}
          <ul class="tag-select">
            <li
              class="tag-select"
              v-for="problemTopic in slotProps.sortedProblemTags"
              v-bind:key="problemTopic.value"
            >
              <label class="tag-select"
                ><input
                  type="radio"
                  v-bind:value="problemTopic.value"
                  v-model="tag"
                />
                {{ problemTopic.text }}</label
              >
            </li>
          </ul></label
        >
      </div>
      <div class="button-row text-right">
        <button
          class="col-md-4 mr-2 btn btn-primary"
          type="submit"
          v-bind:disabled="qualitySeal && !tag"
          v-on:click="slotProps.onSubmit"
        >
          {{ T.wordsSend }}
        </button>
        <button
          class="col-md-4 btn btn-secondary"
          type="button"
          v-on:click="slotProps.onHide(true)"
        >
          {{ T.wordsCancel }}
        </button>
      </div>
    </template>
  </omegaup-popup>
</template>

<script lang="ts">
import { Vue, Component, Prop, Watch } from 'vue-property-decorator';
import Popup from './Popup.vue';
import omegaup_RadioSwitch from '../RadioSwitch.vue';
import T from '../../lang';
import * as ui from '../../ui';

@Component({
  components: {
    'omegaup-popup': Popup,
    'omegaup-radio-switch': omegaup_RadioSwitch,
  },
})
export default class ReviewerPopup extends Vue {
  T = T;
  qualitySeal = true;
  tag = '';

  PROBLEM_CATEGORIES = [
    'problemLevelAdvancedCompetitiveProgramming',
    'problemLevelAdvancedSpecializedTopics',
    'problemLevelBasicIntroductionToProgramming',
    'problemLevelBasicKarel',
    'problemLevelIntermediateAnalysisAndDesignOfAlgorithms',
    'problemLevelIntermediateDataStructuresAndAlgorithms',
    'problemLevelIntermediateMathsInProgramming',
  ];
}
</script>
