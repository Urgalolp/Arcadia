---
title: DATABASE
---

<div id="database-terminal">

  <div id="database-welcome">

    <div>ARCADIA INFORMATION INDEX</div>

    <div class="database-separator">-----------------------------------------------</div>

    <div>SYSTEM STATUS: <strong>ONLINE</strong></div>
    <div>ACCESS LEVEL: ███████</div>
    <div>SESSION: <strong>AUTHENTICATED</strong></div>

    <div class="database-separator">-----------------------------------------------</div>

    <div>WELCOME BACK, F█r█c█u█r█d█D█t█S█r█n█g !</div>

  </div>

</div>

<script>
(() => {
  const pageListing = document.querySelector(".page-listing")

  if (!pageListing) return

  // Hide the folder contents initially.
  pageListing.classList.add("database-list-hidden")

  // Reveal them after the welcome screen has appeared.
  setTimeout(() => {
    pageListing.classList.remove("database-list-hidden")
    pageListing.classList.add("database-list-visible")
  }, 1800)
})()
</script>