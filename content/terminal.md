<script>
const terminal = document.getElementById("terminal-text")
const prompt = document.getElementById("terminal-prompt")

function sleep(ms) {
  return new Promise(resolve => setTimeout(resolve, ms))
}

async function typeText(text, minDelay = 20, maxDelay = 45) {
  for (const char of text) {
    terminal.textContent += char

    const delay =
      minDelay + Math.random() * (maxDelay - minDelay)

    await sleep(delay)
  }
}

async function typeLine(text, minDelay = 20, maxDelay = 45) {
  await typeText(text, minDelay, maxDelay)
  await typeText("\n")
}

async function loadingBar(length = 32, duration = 3000) {
  const interval = duration / length

  for (let i = 0; i <= length; i++) {
    const bar = "█".repeat(i) + " ".repeat(length - i)

    // Remove previous bar if there is one
    terminal.textContent =
      terminal.textContent.replace(/\[[█ ]*\]$/, "")

    terminal.textContent += `[${bar}]`

    if (i < length) {
      await sleep(interval)
    }
  }

  await typeText("\n")
}

async function connectCheck(name) {
  await sleep(2000)
  await typeLine(`[ OK ] ${name}`)
}

async function runTerminal() {

  // -----------------------------------------------
  // HEADER
  // -----------------------------------------------

  await typeLine("██████████████████████████████████████████████")
  await typeLine("")
  await typeLine("                 A R C A D I A")
  await typeLine("              INFORMATION INDEX")
  await typeLine("")
  await typeLine("          SECURE TERMINAL v5.7.21")
  await typeLine("")
  await typeLine("-----------------------------------------------")
  await typeLine("")

  // -----------------------------------------------
  // USER IDENTIFICATION
  // -----------------------------------------------

  await typeLine("USER IDENTIFICATION")
  await typeLine("")
  await typeLine("USERNAME")
  await typeText("> ")

  await typeText("M**************", 35, 80)
  await typeText("\n")

  await typeLine("")
  await typeLine("PASSWORD")
  await typeText("> ")

  // 5% chance of mistyping the password
  const passwordMistake = Math.random() < 0.05

  if (passwordMistake) {

    await typeText("************", 35, 80)

    await sleep(500)

    // Erase password
    await typeText("\b".repeat(12))

    // Since backspaces don't visually erase textContent,
    // rebuild the terminal text without the wrong password.
    terminal.textContent = terminal.textContent.slice(0, -12)

    await typeText("**************", 35, 80)

    await typeText("\n")

    // Required one-second pause after correction
    await sleep(1000)

  } else {

    await typeText("**************", 35, 80)
    await typeText("\n")
  }

  await typeLine("")
  await typeLine("-----------------------------------------------")
  await typeLine("")

  // -----------------------------------------------
  // VERIFYING CREDENTIALS
  // -----------------------------------------------

  await typeLine("VERIFYING CREDENTIALS...")
  await typeText("[")

  // Three-second loading bar
  const barLength = 32
  const barTime = 3000
  const interval = barTime / barLength

  for (let i = 0; i < barLength; i++) {
    await sleep(interval)
    await typeText("█", 0, 0)
  }

  await typeLine("]")
  await typeLine("")

  await typeLine("IDENTITY CONFIRMED")
  await typeLine("")
  await typeLine("ACCESS LEVEL: ███████")
  await typeLine("")
  await typeLine("-----------------------------------------------")
  await typeLine("")

  // Two-second pause before connecting
  await sleep(2000)

  // -----------------------------------------------
  // CONNECTING
  // -----------------------------------------------

  await typeText("CONNECTING TO INDEX")

  // One second per dot
  await sleep(1000)
  await typeText(".")

  await sleep(1000)
  await typeText(".")

  await sleep(1000)
  await typeText(".")

  await typeText("\n\n")

  // 3% chance of "searching" longer
  if (Math.random() < 0.03) {
    await typeLine("[ SEARCHING... ]")
    await sleep(1000)

    await typeText("...")
    await sleep(1000)

    await typeText("...")
    await sleep(1000)

    await typeText("...\n\n")
  }

  // -----------------------------------------------
  // DATABASE CHECKS
  // -----------------------------------------------

  await connectCheck("DATABASE")
  await connectCheck("ARCHIVE")
  await connectCheck("CARTOGRAPHY")
  await connectCheck("PERSONNEL")
  await connectCheck("CLASSIFIED")
  await connectCheck("HISTORICAL RECORDS")

  await typeLine("")
  await typeLine("-----------------------------------------------")
  await typeLine("")

  await typeLine("          ACCESS GRANTED.")

  // -----------------------------------------------
  // WAIT FOR ENTER
  // -----------------------------------------------

  prompt.style.display = "block"

  document.addEventListener("keydown", function onEnter(event) {
    if (event.key === "Enter") {
      document.removeEventListener("keydown", onEnter)
      continueToHome()
    }
  })

  prompt.addEventListener("click", continueToHome, { once: true })
}

function continueToHome() {
  window.location.href =
    (document.body.dataset.basepath || "") + "/home"
}

runTerminal()
</script>