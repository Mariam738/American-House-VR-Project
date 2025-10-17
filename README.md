# American-House-VR Demo Videos Using XR Simulator 📹

## Scoring System 🏆

https://github.com/user-attachments/assets/e80e70a0-d2a0-414c-82e2-d3af791824db

https://github.com/user-attachments/assets/5f7480f6-9d1a-45eb-ab49-730f310d0be6

## Teleport 🚀📍
https://github.com/user-attachments/assets/26fdd75c-ce54-4c61-8e8d-7de517c49a55


## Ray and Direct Grab and Throw 🖐=͟͟͞͞🏀
https://github.com/user-attachments/assets/cc99bc0c-7192-4300-97ea-c0c1a416546e

https://github.com/user-attachments/assets/b5c2d7ca-b5cc-4854-84ad-c4043a2e5e52


# American-House-VR-Project-Checklist-
# **VR Project Assignment — American Home + Backyard Half-Court (Unity 6.2, OpenXR, XRI)**

**Submission Format:** Commit a `README.md` with this checklist **completed** (mark with `[x]`) and include your Unity project folder (or a build + project zip).
**Target Engine:** Unity **6.2** (URP) • **XR**: **OpenXR** + **XR Interaction Toolkit (Action-based)** • Testing: Meta/Oculus simulator or XRI Device Simulator.
**Rule #1:** **1 Unity unit = 1 meter** (physics uses SI: **−9.81 m/s²**).

---

## 0) Project Hygiene & Scale (do this first)

* [✅] `Assets/` folders exist: `Scenes`, `Prefabs`, `Art/Models`, `Art/Materials`, `Art/Textures`, `Scripts`, `Tools`
* [✅] Created **meter tools** in `Tools/`: `Ruler_1m` (1×0.05×0.05), `Door_2.05x0.9` (0.9×2.05×0.1), `Human_1.75m` (capsule scaled to **Y=0.875**)
* [✅] Physics **units respected**: all dimensions entered as meters (no arbitrary scaling)
* [✅] Layers added: `Environment`, `Interactable`, `Court`, `Teleport`, `UIWorld`
* [✅] Tag added: `Ball`

---

## 1) OpenXR + Packages (Unity 6.2)

* [✅] **OpenXR Plugin** installed (Package Manager)
* [✅] **XR Interaction Toolkit** installed (+ **Default Input Actions** sample imported)
* [✅] **XR Plug-in Management**: **OpenXR** enabled for **Standalone** and **Android**
* [✅] **OpenXR → Interaction Profiles**: **Oculus/Meta Touch Controller** enabled
* [✅] **Player → Active Input Handling** = **Input System (New)**

---

## 2) Scene & XR Rig

* [✅] Scene created: `Scenes/AmericanHome_Backyard`
* [✅] Used the one from started assets could not find the action-based Added **XR Origin (Action-based)** to scene
* [✅] Added **XR Interaction Manager**
* [✅] Added **Input Action Manager** with **XRI Default Input Actions** assigned
* [✅] **Teleportation Provider** present on XR Origin
* [✅] **XR Origin → Requested Tracking Origin** = **Floor**; **Camera Y Offset** = **0**
* [✅] Added **XR Device Simulator** (or Meta simulator) for playtesting

---

## 3) Ground (Single Plane) & Grass

* [✅] Created **Plane** `Ground_Main` at (0,0,0)
* [✅] **Scale** set to **X=2.5, Z=4.0** (Unity Plane 1=10 m → **25×40 m** lot)
* [✅] **Layer** = `Environment`
* [✅] **Teleportation Area** added; **Interaction Layer Mask = Teleport**
* [✅] Grass **URP/Lit** material applied (reasonable tiling; no excessive smoothness)

---

## 4) Fence (Perimeter)

* [✅] Built fence from **Cube** segments (each \~**X=2.0, Y=1.8, Z=0.1**)
* [✅] Placed perimeter at lot edges: **Z=±20**, **X=±12.5** (centered lot)
* [✅] All fence pieces **Layer = Environment** (BoxColliders intact)
* [🤷❓] Teleport ray **does not** pass through fence where ground is hidden

---

## 5) House Blockout (on same ground)

* [✅] House footprint approx **12 m × 9 m** (helper deleted after)
* [✅] Perimeter **walls**: height **2.7–3.0 m**, thickness \~**0.2 m**
* [✅] **Door opening**: **0.9 m × 2.05 m** (gap between wall segments)
* [✅] Interior dividers: Living (6×4 m), Kitchen (4×3.5 m), Bedroom (4×3 m), Hall (2×6 m)
* [✅] All walls **Layer = Environment** (colliders present)
* [✅ Locomotion Ouside House Only n Ground_Main] Optional thin floor visuals sit at **Y=0.01** (no Teleportation Area; teleport remains on `Ground_Main`)

---

## 6) Locomotion (Teleport + Optional Smooth Move/Turn)

* [✅] **XR Ray Interactor + Line Visual** on **Left/Right** hands (line length \~20, width 0.01)
* [✅] Teleport works on `Ground_Main` (reticle appears, landing succeeds)
* [✅ Snap Turn on Right✋ and Continouse move on Left ✋] (Optional) **Continuous Move/Turn Providers** added (snap turn 45°; speed \~1.5–2.0 m/s)

---

## 7) Grabbables (Minimum 3 props)

* [✅] Each prop has **Rigidbody** (Use Gravity, Interpolate), **non-trigger collider**
* [✅] Added **XR Grab Interactable** (Movement = **Velocity Tracking**, **Throw On Detach** enabled)
* [✅] Tuned **Drag** \~0.02–0.05, **Angular Drag** \~0.02–0.05
* [✅ Right ✋ is Direct Interactable Left ✋ is Ray Interactable and used radius is 0.1 to cover all hand ] Hands have **XR Direct Interactor** + **Sphere Collider (Is Trigger, Radius \~0.05)**

---

## 8) Basketball Half-Court (Backyard)

* [🌀✅ Used Full High School Court  Size of 15.24 * 25.6] Court size ≈ **9 m × 14 m** (half-court)
* [✅] **Backboard** \~**1.8 m × 1.05 m**; **Rim height = 3.05 m**
* [✅] **Rim inner diameter** \~**0.45 m** (18″)
* [✅] **Free-throw line** at **4.57 m** from backboard plane
* [✅ Used Textured Plane] Lines created (thin white cubes or a single textured plane)
* [✅] **NetTrigger** (IsTrigger) under rim for scoring detection (prep for Part: scoring)

---

## 9) Basketball (Sphere) — Physics & Grab

* [✅] **Sphere** `Ball_Sphere` created at \~**Y=1.2**
* [🌀✅Used Model from Asset Store with scale 1 but same size] **Scale** **(0.24, 0.24, 0.24)** (≈ 24 cm diameter)
* [✅] **Rigidbody**: **Mass=0.62**, **Drag=0.03**, **Angular Drag=0.03**, **Collision Detection=Continuous**, **Interpolation=Interpolate**
* [✅] **Physic Material** `PM_Basketball`: **Bounciness \~0.8**, Friction 0.6/0.7, **Bounce Combine=Maximum**
* [✅] **SphereCollider → Material = PM\_Basketball**
* [✅] **XR Grab Interactable**: **Velocity Tracking**, **Throw On Detach**, **Throw Velocity Scale \~1.05**
* [✅] **Tag = Ball** (for later scoring)

---

## 10) Lighting & Sky (Readable Daylight)

* [✅] One **Directional Light** (“Sun”) at \~30–45° elevation (soft, readable shadows)
* [✅] **Global Volume** (optional) for Skybox/HDRI (light post-FX only; no DoF/Motion Blur)
* [✅] URP **Shadow Distance** \~**25–35 m** (Quest-friendly)

---

## 11) Performance Pass (Quest-friendly)

* [✅] **URP Render Scale = 1.0**, **MSAA = 4×**
* [✅] Minimal post-FX; **no SSAO**, **no Motion Blur**, **no DoF**
* [✅] **Textures** mostly **1K** (hero at 2K); mobile compression ready
* [✅I guess this is done] Prefer **Box/Sphere/Capsule** colliders; avoid MeshCollider on large statics
* [🛠️ Had some problems with texture export from blender to unity working. Currently fixing them and trying to bake multiple textures in one map] Keep **unique materials ≤ \~50**
* [✅ I have no tiny probs to disble shadows on them] Disable shadows on tiny props; limit additional real-time lights

---

## 12) Verification (Play Mode)

* [✅] Camera height feels human-scaled near `Door_2.05x0.9` and `Human_1.75m`
* [✅] Teleport works outdoors and through the **door gap** into the house; walls/fence block where expected
* [✅] At least **3 grabbable props** work with **Direct** and **Ray** grab
* [✅] Ball **throws** naturally and **bounces** on ground/court
* [✅] Half-court **dimensions** match checklist (rim at **3.05 m**)

---

## 13) Build (Optional but recommended if you have a Quest)

* [✅] **File → Build Settings → Android**, **IL2CPP**, **ARM64**, Min API ≥ 29
* [✅] **OpenXR** active for Android; **Meta Quest Support** enabled in OpenXR features
* [✅ Tried to build on default devices but BUILD FAILED😞 but all compatible devices was SUCCESSFUL😀] First build as **Development Build** to validate input & performance on-device

---

## 14) Deliverables (what to submit)

* [✅] **Project zip** (or repo link) including `Assets/` and `ProjectSettings/`
* [✅] **Playable build** (PCVR or Android APK) if available
* [✅] `README.md` with this checklist **ticked** and **screenshots**:

  * [✅] Yard + fence overview
  * [✅ Door opening done in another project not here] Interior house blockout + door opening
  * [✅ In video] Ball grab and bounce
  * [✅] Court close-up with measured rim height
* [✅] Short clip (optional): teleport → grab → throw → score attempt

---

## Grading Rubric (100 pts)

* [ ] **Scale & Hygiene (15 pts):** correct units, folders, layers/tags, meter tools present
* [ ] **XR Rig & Locomotion (15 pts):** OpenXR/XRI configured; teleport (and optional smooth move/turn) working
* [ ] **Environment (15 pts):** one ground plane, correct lot size, fence blocks teleport, readable daylight
* [ ] **House Blockout (15 pts):** correct dimensions; door opening usable; colliders block rays
* [ ] **Grabbables (10 pts):** 3+ props with proper Rigidbody + XRI Grab (stable feel)
* [ ] **Basketball Court (15 pts):** half-court specs, rim 3.05 m, lines/trigger
* [ ] **Ball Physics (10 pts):** mass/drag/bounce correct; throws feel natural
* [ ] **Performance (5 pts):** sensible URP settings; low post-FX; simple colliders
* [ ] **Polish (5 pts):** materials tidy, consistent naming, scene organization

---

### Stretch Goals (extra credit)

* [ ] Score trigger increments UI counter + sound/haptics
* [ ] Reset button respawns ball at a point
* [ ] Comfort toggle (snap vs smooth turn) in a world-space menu
* [ ] Basic baked lights for interiors (low cost)

---

**Finished by Eng. Hatem Heshmat**
