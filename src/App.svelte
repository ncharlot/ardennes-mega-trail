<svelte:options
  customElement={{ tag: "ardennesmegatrail-faq", shadow: "none" }}
/>

<script lang="ts">
  import { onMount } from "svelte";
  import { getThemes } from "./lib/api/theme";
  import { getQuestions } from "./lib/api/question";
  import type { Theme } from "./lib/types/Theme";
  import type { Question } from "./lib/types/Question";
  import Accordion from "./lib/components/Accordion.svelte";

  export let locale = 'fr';

  let themes: Theme[] = [];
  let questions: Question[] = [];

  onMount(() => {
    getThemes().then((data) => {
      themes = data as Theme[];
    });

    getQuestions().then((data) => {
      questions = data as Question[];
    });
  });
</script>

<main>
  {#each themes as theme (theme.id)}
    <h3>
      {locale === "fr" ? theme.name_fr : theme.name_en}
    </h3>

    <div class="panel-group" id="faq-theme{theme.id}" role="tablist" aria-multiselectable="true">
      <Accordion {locale} questions={questions.filter((q) => q.theme_id === theme.id)}/>
    </div>
  {/each}
</main>
