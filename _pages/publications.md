---
layout: page
permalink: /publications/
title: Publications
nav: true
nav_order: 2
---

<style>
  /* Give the CBS Protocol GIF room, and make the matching self-author easy to spot. */
  .publications .author > em {
    border-bottom: 0 !important;
    font-style: normal;
    font-weight: 700;
    text-decoration: underline 2px solid currentColor;
    text-underline-offset: 0.15em;
  }

  @media (min-width: 576px) {
    .publications .row:has(#veerapaneni2025cbs_protocol, #olin2025thinkfastrealtimekinodynamic, #olin2026adaptivecbf) > .abbr {
      flex: 0 0 30%;
      max-width: 30%;
    }

    .publications .row:has(#veerapaneni2025cbs_protocol) > #veerapaneni2025cbs_protocol,
    .publications .row:has(#olin2025thinkfastrealtimekinodynamic) > #olin2025thinkfastrealtimekinodynamic,
    .publications .row:has(#olin2026adaptivecbf) > #olin2026adaptivecbf {
      flex: 0 0 66%;
      max-width: 66%;
    }

    .publications .row:has(#veerapaneni2025cbs_protocol, #olin2025thinkfastrealtimekinodynamic, #olin2026adaptivecbf) .preview {
      width: 100%;
      max-width: 100%;
      height: auto;
    }
  }

  .publications .row:has(#veerapaneni2025cbs_protocol, #olin2025thinkfastrealtimekinodynamic, #olin2026adaptivecbf) {
    margin-bottom: 2.5rem;
  }
</style>

<!-- _pages/publications.md -->

<!-- Bibsearch Feature -->

{% include bib_search.liquid %}

<div class="publications">

{% bibliography %}

</div>

<script>
  document.addEventListener("DOMContentLoaded", () => {
    document.querySelectorAll('.publications a[href="http://localhost:8080/cbf-safety-filters/"]').forEach((link) => {
      link.textContent = "Webpage";
      link.setAttribute("aria-label", "Webpage");
    });
  });
</script>
