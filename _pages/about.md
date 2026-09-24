---
layout: about
title: home
permalink: /
subtitle: Robotics · Motion Planning · Learning

profile:
  align: right
  image: headshot.jpg
  image_circular: false
  more_info: >
    <p>Search-Based Planning Lab</p>
    <p>Carnegie Mellon University</p>

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

I work on robotics problems where decisions have to be both fast and informed by the structure of the task. My research combines search-based planning, dynamics, state estimation, and learning to help robots act in real time under uncertainty.

My thesis work explored two directions: belief-space planning for intercepting fast-moving objects, and learning adaptive control barrier functions that distill kinodynamic planners into reactive safety filters. The common thread is preserving useful model-based reasoning while meeting the demands of real-time execution.

I earned a B.S. in Mechanical Engineering with a Computer Science concentration from UCLA and an M.S. in Robotics from Carnegie Mellon University, where I worked with the Search-Based Planning Lab.

[Thesis presentation (PDF)](/assets/pdf/thesis-presentation.pdf) · [ICRA 2026 poster (PDF)](/assets/pdf/icra-2026-poster.pdf)
