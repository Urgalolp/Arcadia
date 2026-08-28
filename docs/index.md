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

  /*
   * Adds a centered line based on the current terminal width.
   * This keeps the visible text centered without changing
   * the actual terminal container.
   */
  async function writeCentered(text = "", min = 20, max = 50) {
    const width = 46
    const padding = Math.max(0, Math.floor((width - text.length) / 2))

    await writeLine(
      " ".repeat(padding) + text,
      min,
      max
    )
  }

  /*
   * User/password lines are intentionally left-aligned.
   */
  async function writeUserLine(text = "", min = 20, max = 50) {
    await writeLine(text, min, max)
  }

  async function boot() {

    // ================================================
    // HEADER
    // ================================================

    await writeLine(
      "█████████████████████████████████████████████"
    )

    await writeCentered("")
    await writeCentered("A R C A D I A")
    await writeCentered("INFORMATION INDEX")
    await writeCentered("")
    await writeCentered("SECURE TERMINAL v5.7.21")
    await writeCentered("")
    await writeCentered("----------------------------------------------")

    await sleep(800)


    // ================================================
    // USER IDENTIFICATION
    // ================================================

    await writeCentered("")
    await writeCentered("USER IDENTIFICATION")
    await writeCentered("")

    // User section intentionally left-aligned
    await writeUserLine("USERNAME")

    await sleep(250)

    await typeText("> ")

    await typeText(
      "F**************",
      40,
      90
    )

    output.textContent += "\n"

    await sleep(350)

    await writeUserLine("PASSWORD")

    await sleep(250)

    await typeText("> ")

    const correctPassword = "**************"

    // 5% chance of typing the password incorrectly
    const incorrectPassword = Math.random() < 0.05

    if (incorrectPassword) {

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

      await sleep(1000)

    } else {

      await typeText(
        correctPassword,
        40,
        100
      )

      output.textContent += "\n"
    }

    await sleep(500)

    await writeCentered(
      "----------------------------------------------"
    )


    // ================================================
    // VERIFYING CREDENTIALS
    // ================================================

    await sleep(500)

    await writeCentered("")

    await writeCentered(
      "VERIFYING CREDENTIALS..."
    )

    await sleep(500)

    const barLength = 32
    const barDuration = 3000
    const barInterval = barDuration / barLength

    const barStart = output.textContent.length

    output.textContent +=
      "[" + " ".repeat(barLength) + "]"

    for (let i = 1; i <= barLength; i++) {

      await sleep(barInterval)

      const bar =
        "█".repeat(i) +
        " ".repeat(barLength - i)

      output.textContent =
        output.textContent.slice(0, barStart) +
        `[${bar}]`
    }

    output.textContent += "\n"

    await writeCentered("")

    await writeCentered(
      "IDENTITY CONFIRMED"
    )

    await writeCentered("")

    await writeCentered(
      "ACCESS LEVEL: ███████"
    )

    await writeCentered("")

    await writeCentered(
      "----------------------------------------------"
    )

    await sleep(2000)


    // ================================================
    // CONNECTING TO INDEX
    // ================================================

    await writeCentered("")

    await writeCentered(
      "CONNECTING TO INDEX"
    )

    // One second per dot
    await sleep(1000)
    await typeText(".")

    await sleep(1000)
    await typeText(".")

    await sleep(1000)
    await typeText(".")

    /*
     * 3% chance of taking longer.
     */
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

      await sleep(1000)

      await writeCentered(
        `[ OK ] ${system}`
      )
    }


    // ================================================
    // ACCESS GRANTED
    // ================================================

    await writeCentered("")

    await writeCentered(
      "----------------------------------------------"
    )

    await writeCentered("")

    await sleep(500)

    await writeCentered(
      "ACCESS GRANTED."
    )

    await sleep(1500)


    // ================================================
    // WAIT FOR ENTER / CLICK
    // ================================================

    terminalInput.style.display = "block"

    function continueToHome() {
      window.location.href = "./DATABASE/"
    }

    function handleEnter(event) {
      if (event.key === "Enter") {
        window.removeEventListener("keydown", handleEnter)
        continueToHome()
      }
    }

    window.addEventListener(
      "keydown",
      handleEnter
    )

    terminalInput.addEventListener(
      "click",
      continueToHome
    )

    terminalInput.addEventListener(
      "pointerup",
      continueToHome
    )
  }

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

  /* Allow vertical scrolling when the terminal is taller than the screen */
  overflow-y: auto;
  overflow-x: hidden;
}

#terminal-output {
  width: 380px;
  max-width: calc(100vw - 2rem);

  margin: 0;

  white-space: pre-wrap;
  overflow-wrap: anywhere;

  font-family:
    "IBM Plex Mono",
    "Courier New",
    monospace;

  font-size: 14px;
  line-height: 1.45;

  box-sizing: border-box;
}

#terminal-input {
  display: none;

  width: 380px;
  max-width: calc(100vw - 2rem);

  margin-top: 2rem;

  font-family:
    "IBM Plex Mono",
    "Courier New",
    monospace;

  font-size: 14px;

  cursor: pointer;
  user-select: none;
  -webkit-tap-highlight-color: transparent;

  box-sizing: border-box;
}

#terminal-cursor {
  animation: cursor-blink 1s steps(1) infinite;
}

@keyframes cursor-blink {
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

    /*
     * Start at the top on phones so the full sequence
     * has vertical room to grow.
     */
    justify-content: flex-start;

    /*
     * Let the user scroll down to the final prompt.
     */
    overflow-y: auto;
    overflow-x: hidden;

    min-height: 100dvh;
  }

  #terminal-output {
    width: 100%;
    max-width: 100%;

    font-size: 11px;
    line-height: 1.35;

    white-space: pre-wrap;
    overflow-wrap: anywhere;
  }

  #terminal-input {
    width: 100%;
    max-width: 100%;

    margin-top: 1rem;

    padding: 0.75rem 0;

    font-size: 11px;

    /*
     * Make the tap target larger.
     */
    min-height: 2.5rem;
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