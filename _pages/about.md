---
layout: about
title: Home
permalink: /

profile:
  align: right
  image: headshot.jpg
  image_circular: false
  more_info: >
    <p>MS Robotics, Carnegie Mellon University</p>

selected_papers: true
social: true

announcements:
  enabled: false

latest_posts:
  enabled: false
---

<style>
  /* Match the larger CBS publication preview and author emphasis on the publications page. */
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

I am a recent M.S. Robotics graduate from [The Robotics Institute](https://www.ri.cmu.edu/), Carnegie Mellon University, where I was advised by [Maxim Likhachev](https://www.cs.cmu.edu/~maxim/) and [Howie Choset](https://www.ri.cmu.edu/ri-faculty/howie-choset/).

My research focused on reactive motion planning and control, allowing robots to quickly move through uncertain and dynamic environments. I am interested in combining ideas from machine learning, discrete search, and optimal control to deploy performant, yet safe algorithms with limited compute.

Previously, I earned a B.S. in Mechanical Engineering with a Computer Science concentration from UCLA.

## News

- **July 2026** — Successfully defended my Master's thesis, [*Exploiting Structure for Real-Time Robot Motion Planning and Control*](https://publications.ri.cmu.edu/exploiting-structure-for-real-time-robot-motion-planning-and-control).
- **January 2026** — Two papers accepted to ICRA 2026: [*Think Fast*](https://arxiv.org/abs/2512.01108) and [*CBS Protocol*](https://arxiv.org/abs/2510.00425).

<script>
  document.addEventListener("DOMContentLoaded", () => {
    const selectedPublications = document.querySelector('h2 a[href$="/publications/"]');
    if (selectedPublications) selectedPublications.textContent = "Selected Publications";
    document.querySelectorAll('.publications a[href="/cbf-safety-filters/"]').forEach((link) => {
      link.textContent = "Webpage";
      link.setAttribute("aria-label", "Webpage");
    });
  });
</script>
