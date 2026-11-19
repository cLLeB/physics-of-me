# Physics of Me

**Predict, measure on yourself with your phone's sensors, then see the formula with your own numbers.**

Physics of Me turns a phone into a pocket physics lab. Each activity asks a question ("How high can you jump?"), lets you guess, measures the real answer with the phone's own sensors, and then shows the formula filled in with your measurements. No rulers, no extra hardware: the phone measures distances itself (drop height, string length, spin radius, wall distance).

Built by **The Visionaries of Physics** for the **ISEN Innovation Contest 2026**.

- **Try it in the browser:** https://clleb.github.io/physics-of-me/
- **Android app:** [physics-of-me.apk](https://clleb.github.io/physics-of-me/physics-of-me.apk) (version 1.3, Android 8.0+)

## How an activity works

1. **Predict.** Make a guess with a slider.
2. **Measure.** Do it for real (jump, drop, swing, clap, walk upstairs) while the phone records.
3. **See the formula.** The law appears with your own numbers in it, and the app shows how close your guess was.
4. **Your turn.** Try again and change one thing.

## Activities

| Area | Activity | Question | Sensor | Formula |
|---|---|---|---|---|
| Mechanics | Slope | How fast does it slide? | Accelerometer | a = g · sin θ |
| Mechanics | Jump | How high can you jump, and with how much energy? | Accelerometer | h = g · t² / 8, E = m · g · h |
| Mechanics | Drop | Measure a height with a fall | Accelerometer | h = ½ · g · t² |
| Mechanics | Lift | Are you heavier in a lift? | Accelerometer | N = m · (g + a) |
| Mechanics | Pendulum | Measure gravity with a string | Gyroscope | T = 2π · √(L / g) |
| Mechanics | Light gate | Time swings without touching them | Proximity sensor | T = 2 × time between passes |
| Mechanics | Spin | What pushes you out in a turn? | Gyroscope + accelerometer | a = ω² · r |
| Mechanics | Reaction | The ruler-drop test, on screen | Touchscreen | d = ½ · g · t² |
| Mechanics | Run | Your speed from satellites | GPS | v = d / t |
| Magnetism | Magnet | See an invisible field | Magnetometer | B ∝ 1 / d³ |
| Waves and sound | Sound | What note is that? | Microphone | λ = v / f |
| Waves and sound | Beats | Two notes that wobble | Speaker | f_beat = \|f₁ − f₂\| |
| Waves and sound | Echo | Measure the speed of sound with a clap | Microphone + speaker | v = 2d / t |
| Light and EM waves | Light | How light fades with distance | Light sensor | I ∝ 1 / d² |
| Light and EM waves | Wi-Fi | An invisible wave you can measure | Wi-Fi signal strength | −6 dB per doubling of distance |
| Electricity | Charge | How many watts flow into your phone? | Battery voltage and current | P = V · I |
| Heat | Cool down | Why hot things cool fast, then slowly | Battery temperature | Newton's law of cooling |
| Fluids and pressure | Stairs | Weigh the air above you | Barometer | Δh = ΔP / (ρ · g) |

## Three ways to run it

- **Android app:** every activity, with direct access to all the sensors (gyroscope, magnetometer, light, barometer, proximity, battery, Wi-Fi, GPS). The app checks the website at launch and offers new versions.
- **Browser:** open the website on a phone; the activities the browser can reach (motion, sound, touch) work directly.
- **Demo data:** on a computer, or a phone without a given sensor, activities run on sample data so the lesson still works.

## Project layout

```
index.html                 the whole app: activities, charts and formulas (HTML, CSS, JavaScript)
version.json               latest version number, read by the app to offer updates
physics-of-me.apk          signed Android build
android/
  AndroidManifest.xml      permissions: microphone, Wi-Fi state, location (GPS), internet
  src/.../MainActivity.java  WebView wrapper with a JavaScript bridge to the native sensors
  res/                     icon and theme
  build.ps1                build script using the plain Android SDK tools (no Gradle)
```

## Build the Android app

Needs the Android SDK (build-tools 34.0.0, platform android-34), a JDK, and Python.

```powershell
powershell -NoProfile -ExecutionPolicy Bypass -File android\build.ps1
```

The script packages `index.html` into a WebView app, compiles the Java bridge, and writes a signed `physics-of-me.apk` at the repository root. The signing key is kept outside the repository (`%USERPROFILE%\.android\physicsofme.jks`) so new builds install over old ones.

## Safety

Some activities involve moving the phone: use a cushion for slides and drops, and keep a firm grip during spins.
