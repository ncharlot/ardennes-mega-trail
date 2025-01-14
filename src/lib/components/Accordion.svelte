<script lang="ts">
  import type { Question } from "../types/Question";

  export let locale = 'fr';
  export let questions: Question[] = [];
</script>

{#each questions as question (question.id)}
  <div class="panel panel-default">
    <div class="panel-heading" role="tab" id="faq-question{question.id}">
      <h4 class="panel-title">
        <a role="button" data-toggle="collapse" data-parent="#faq-theme{question.theme_id}" href="#faq-answer{question.id}" aria-expanded="true" aria-controls="faq-answer{question.id}">
          {locale === "fr" ? question.question_fr : question.question_en}
        </a>
      </h4>
    </div>
    <div id="faq-answer{question.id}" class="panel-collapse collapse" role="tabpanel" aria-labelledby="faq-question{question.id}">
      <div class="panel-body">
        {@html locale === "fr" ? question.answer_fr : question.answer_en}
      </div>
    </div>
  </div>
{/each}
