---
title: Arcadia Terminal
---

<div id="arcadia-terminal">

<pre id="terminal-output"></pre>

<div id="terminal-input">
  <span id="terminal-prompt">[ PRESS ENTER OR CLICK TO CONTINUE ]</span>
  <span id="terminal-cursor">█</span>
</div>

</div>

<script>
(() => {
  const output = document.getElementById("terminal-output")
  const terminalInput = document.getElementById("terminal-input")

  if (!output || !terminalInput) return

  const sleep = ms =>
    new Promise(resolve => setTimeout(resolve, ms))

  async function typeText(text, min = 20, max = 50) {
    for (const char of text) {
      output.textContent += char

      const delay =
        min + Math.random() * (max - min)

      await sleep(delay)
    }
  }

  async function writeLine(text = "", min = 20, max = 50) {
    await typeText(text, min, max)
    output.textContent += "\n"
  }

  async function boot() {

    // ================================================
    // HEADER
    // ================================================

    await writeLine(
      "██████████████████████████████████████████████"
    )

    await writeLine("")

    await writeLine(
      "                 A R C A D I A"
    )

    await writeLine(
      "              INFORMATION INDEX"
    )

    await writeLine("")

    await writeLine(
      "          SECURE TERMINAL v5.7.21"
    )

    await writeLine("")

    await writeLine(
      "----------------------------------------------"
    )

    await sleep(800)


    // ================================================
    // USER IDENTIFICATION
    // ================================================

    await writeLine("")

    await writeLine("USER IDENTIFICATION")

    await writeLine("")

    // Username
    await writeLine("USERNAME")

    await sleep(250)

    await typeText("> ")

    await typeText(
      "F**************",
      40,
      90
    )

    output.textContent += "\n"

    await sleep(350)


    // Password
    await writeLine("PASSWORD")

    await sleep(250)

    await typeText("> ")

    const correctPassword = "**************"

    // 5% chance of typing the password incorrectly
    const incorrectPassword = Math.random() < 0.05

    if (incorrectPassword) {

      // Type incorrect password
      await typeText(
        "************",
        40,
        100
      )

      await sleep(300)

      // Erase incorrect password
      for (let i = 0; i < 12; i++) {

        output.textContent =
          output.textContent.slice(0, -1)

        await sleep(60)
      }

      await sleep(200)

      // Type correct password
      await typeText(
        correctPassword,
        40,
        100
      )

      output.textContent += "\n"

      // Pause after correcting password
      await sleep(1000)

    } else {

      // Type correct password
      await typeText(
        correctPassword,
        40,
        100
      )

      output.textContent += "\n"
    }

    await sleep(500)

    await writeLine(
      "----------------------------------------------"
    )


    // ================================================
    // VERIFYING CREDENTIALS
    // ================================================

    await sleep(500)

    await writeLine("")

    await writeLine(
      "VERIFYING CREDENTIALS..."
    )

    await sleep(500)

    const barLength = 32
    const barDuration = 3000
    const barInterval = barDuration / barLength

    // Create empty bar
    output.textContent +=
      "[" + " ".repeat(barLength) + "]"

    for (let i = 1; i <= barLength; i++) {

      await sleep(barInterval)

      const bar =
        "█".repeat(i) +
        " ".repeat(barLength - i)

      // Replace the existing bar
      output.textContent =
        output.textContent.replace(
          /\[[█ ]*\]$/,
          `[${bar}]`
        )
    }

    output.textContent += "\n"

    await writeLine("")

    await writeLine(
      "IDENTITY CONFIRMED"
    )

    await writeLine("")

    await writeLine(
      "ACCESS LEVEL: ███████"
    )

    await writeLine("")

    await writeLine(
      "----------------------------------------------"
    )

    // Pause before connecting
    await sleep(2000)


    // ================================================
    // CONNECTING TO INDEX
    // ================================================

    await writeLine("")

    await typeText(
      "CONNECTING TO INDEX"
    )

    // One second per dot
    await sleep(1000)
    await typeText(".")

    await sleep(1000)
    await typeText(".")

    await sleep(1000)
    await typeText(".")


    // 3% chance of taking longer to locate the index
    if (Math.random() < 0.03) {

      await sleep(1000)

      await typeText("...")

      await sleep(1000)

      await typeText("...")

      await sleep(1000)

      await typeText("...")
    }

    output.textContent += "\n\n"


    // ================================================
    // SYSTEM CHECKS
    // ================================================

    const systems = [
      "SYSTEM",
      "DATABASE",
      "CLASSIFIED",
      "HISTORICAL RECORDS",
      "LOGISTICS",
      "PERSONNEL"
    ]

    for (const system of systems) {

      // Two seconds per system
      await sleep(1000)

      await writeLine(
        `[ OK ] ${system}`
      )
    }


    // ================================================
    // ACCESS GRANTED
    // ================================================

    await writeLine("")

    await writeLine(
      "----------------------------------------------"
    )

    await writeLine("")

    await sleep(500)

    await writeLine(
      "          ACCESS GRANTED."
    )

    await sleep(1500)


    // ================================================
    // WAIT FOR ENTER
    // ================================================

    function continueToHome() {
      window.location.href = "./Home/home"
    }

    // Desktop: Enter key
    function handleEnter(event) {
      if (event.key === "Enter") {
        window.removeEventListener("keydown", handleEnter)
        continueToHome()
      }
    }

    window.addEventListener("keydown", handleEnter)

    // Mobile / mouse: tap or click the prompt
    terminalInput.addEventListener("click", continueToHome)

    // Mobile touch
    terminalInput.addEventListener("touchend", continueToHome)

  boot()
})()
</script>

<style>
#arcadia-terminal {
  position: fixed;
  inset: 0;
  z-index: 999999;

  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;

  background: #000;
  color: #fff;

  padding: 2rem;
  box-sizing: border-box;

  font-family:
    "IBM Plex Mono",
    "Courier New",
    monospace;

  overflow: hidden;
}

#terminal-output {
  width: min(900px, 100%);

  margin: 0;

  white-space: pre-wrap;
  overflow-wrap: anywhere;

  font-family:
    "IBM Plex Mono",
    "Courier New",
    monospace;

  font-size: 14px;
  line-height: 1.45;
}

#terminal-input {
  display: none;

  width: min(900px, 100%);

  margin-top: 2rem;

  font-family:
    "IBM Plex Mono",
    "Courier New",
    monospace;

  font-size: 14px;

  animation: blink 1s steps(1) infinite;

  cursor: pointer;
  user-select: none;
  -webkit-tap-highlight-color: transparent;
}

@keyframes blink {
  50% {
    opacity: 0;
  }
}


/* =========================================================
   MOBILE
   ========================================================= */

@media screen and (max-width: 600px) {

  #arcadia-terminal {
    padding: 1rem;
    justify-content: flex-start;
  }

  #terminal-output {
    width: 100%;

    font-size: 11px;
    line-height: 1.35;

    /*
     * Prevent long terminal lines from forcing
     * horizontal scrolling.
     */
    white-space: pre-wrap;
    overflow-wrap: anywhere;
  }

  #terminal-input {
    width: 100%;

    margin-top: 1rem;

    font-size: 11px;
  }
}


/* =========================================================
   VERY SMALL PHONES
   ========================================================= */

@media screen and (max-width: 380px) {

  #arcadia-terminal {
    padding: 0.75rem;
  }

  #terminal-output {
    font-size: 9px;
    line-height: 1.3;
  }

  #terminal-input {
    font-size: 9px;
  }
}
</style>