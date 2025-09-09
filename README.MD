# Unreal Engine Modular Interaction System

[![Watch the video](https://img.shields.io/badge/▶️-Watch%20Demo-red?style=for-the-badge)](https://youtu.be/h8zYoLTyDkA)

## 1. About the Project

This project is a **modular interaction system** for Unreal Engine.
The system includes:

- **Doors**: Normal and locked, with modular events
- **Notes**: Modular note system configurable directly in the level
- **Item & Inventory**: Pickup system including unique items like flashlight
- **Chest System**: Place and reveal items in-game
- **Light Switch System**: Fully modular lights
- **Highlight & Custom Interaction Text**

**The system is fully modular and easy to extend.**
It is also open-source for anyone to use and improve.

---

## 2. Installation

You can either **download the project from GitHub** or use the **direct download link** provided below.

**Option 1 – GitHub:**

```
git clone https://github.com/Batin-dev/ue5-fps-interaction.git
```

**Option 2 – Direct Download:**
[Download the Project](https://drive.google.com/file/d/18cMzZ1FFytrQyjNg87V9quI8GCoBIQXK/view?usp=sharing)

After downloading or cloning, simply **open the `.uproject` file** in Unreal Engine 5 or later.
The project will **open immediately**.

**Note:** The project might be slightly large because it includes Unreal Engine Starter Content.

---

## 3. Usage & Examples

You can place blueprints directly into your level.
All **interactions are managed through base classes**, making it easy to customize child actors.

---

## 4. Blueprints & Class Structure


### **BP_Interactable_Base**

- **Description:** Parent class for all interactable objects.
  This class includes an interface with an `Interact` function that can be overridden in child blueprints.

- **Features:**

  - Interaction Text (fully customizable per child using `SetInteractionText`)
  - Outline / Highlight system

    - `ActivateOutline` and `DeactivateOutline` custom events are available.
    - No need to manually set up outlines; all meshes without the **NoOutline** tag automatically get highlighted.

  - `Interact` function (added by double-clicking the Interact interface in the Interfaces section and overridden in child blueprints for custom actions)

- **Usage:** Create child blueprints and:

  1. Override the `Interact()` function for custom behavior
  2. Use `SetInteractionText` to define child-specific interaction text

---

### **BP_Door_Base**

- **Description:** Modular system for normal and locked doors.

- **Customization Functions:**

  - `SetTLPlayRate` → Adjusts door opening/closing speed
  - `SetOpenAngle` → Sets the door's opening angle
  - `SetCloseSoundDelay` → Delay before the closing sound plays (experimental)
  - `SetOpenAndCloseSounds` → Sets custom open and close sounds

- **Events:**
- Open/Close Door Events → Handles door opening and closing; already present in BP_Door_Base and linked to the `Interact` function (BPI), can be overridden in child blueprints for custom behavior
- Child blueprints can leave the functions empty to use default values, or override them for custom behavior

_Open/Close Door Event Image:_
![openCloseDoorBP](https://res.cloudinary.com/dy5a7diii/image/upload/v1757360127/openCloseDoorBP_wpx1m4.png)
_Example custom settings usage in child class:_
![doorSettings](https://res.cloudinary.com/dy5a7diii/image/upload/v1757360126/DoorSettingBp_gqizgt.png)

---

### **BP_Door_Locked_Base**

- **Description:** Base class for locked doors, extending BP_Door_Base.

- **Events:**

  - `TryOpenDoor` → Attempts to open the door by checking for the correct key.

    - KeyID can be set directly in the level/map.
    - Child blueprints can override this event to customize mesh, sounds, or other behavior.
    - Leaving `TryOpenDoor` empty in child blueprints will use the default behavior.

- **Customization Functions:**

  - All customization functions from BP_Door_Base (`SetTLPlayRate`, `SetOpenAngle`, `SetCloseSoundDelay`, `SetOpenAndCloseSounds`) are also available here.

**Note**: In child blueprints, make sure to call the **TryOpenDoor** event inside the Interact function (BPI)

_Example usage in child class:_
![LockeddoorSettings](https://res.cloudinary.com/dy5a7diii/image/upload/v1757360301/LockedDoorSettings_n6qrpr.png)

---

### **BP_Note_Base**

- **Description:** Base class for notes. This class is simple and not heavily modular.

- **Usage / Customization:**

  - You can create child blueprints to use different meshes if desired.
  - The note's content can be changed by modifying the `Note Text` variable directly in the level/map.

- **Events:**

  - Optional: You can call custom events inside the `Interact` function (BPI) in child blueprints if additional interaction logic is needed.

---

### **BP_LightSwitch**

- **Description:** Simple light switch system.

- **Usage / Customization:**

  - Place the blueprint in your level and assign lights to the `Lights` array directly from the map.
  - You can set the initial state of each light using the `IsOpened` variable in the map (true = on, false = off).

- **Notes:**

  - Very lightweight and straightforward; minimal setup required.

_Example usage in level:_

![lightswitch](https://res.cloudinary.com/dy5a7diii/image/upload/v1757360380/lightswitch_mqvnry.png)

---

### **BP_Item_Base**

- **Description:** Base class for all pickable items.

- **Usage / Features:**

  - `AddToInventory` function → Adds the item to the inventory.

    - You can define whether the item is unique (only one can be picked) or stackable.

  - `DestroyActor (Safe)` → Removes the item from the world after pickup.
  - `PlaySound` event → Plays a pickup sound. If no sound is specified, default values are used.
  - The `Interact` function (BPI) in the base class is empty; child blueprints can call these functions when interacted with.

_Example usage in flashlight:_
![flashlightUsage](https://res.cloudinary.com/dy5a7diii/image/upload/v1757360612/exampleFlashlight_ow8r6n.png)

## 🤝 Contributing

This project is open-source! Contributions are welcome:

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m "Add some AmazingFeature"`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

## License

**Unlicense** – Use however you like, no restrictions!

## 💬 Support & Community

- For **bug reports**, **feature requests**, or questions, contact me on Discord: **batin.cpp**

---

Made with ❤️ for the Unreal Engine community.
⭐ If this project helped you, please consider giving it a star! ⭐
