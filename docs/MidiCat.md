# stoermelder MIDI-CAT and MEM-expander

MIDI-CAT is a module for MIDI-mapping and an evolution of [VCV's MIDI-MAP](https://vcvrack.com/manual/Core.html#midi-map) with several additional features:

- It can be configured for an MIDI output-port to send **controller feedback**, all your controls get initalized on patch-loading if your controller supports it!

- It has two different **pickup-modes** for controllers without input or automatic adjustment, so your parameters won't change until your controls reach their current positions.

- It allows mapping of **MIDI note messages**, providing momentary-mode, momentary-mode with velocity and toggle-mode.

- You can switch the module to "Locate and indicate" mode, which will help you to retrace your midi controls to the mapped module and parameter.

- CPU usage has been optimized.

Besides these new features the module brings the goodies known from stoermelder's other mapping modules like...

- ...text scrolling for long parameter names,

- ..."Locate and indicate" on slot's context menu for finding mapped parameters and

- ...unlocked parameters for changes by mouse or by preset loading or using a by preset-manager like stoermelder's [8FACE](./EightFace.md).

![MIDI-CAT intro](./MidiCat-intro.gif)

## Mapping parameters

A typical workflow for mapping your MIDI-controller will look like this:

- Connect your MIDI controller and select it on the top display of MIDI-CAT. If your controller can receive MIDI messages you can select the output port of the controller in the display in the middle.
- Activate the first mapping slot by clicking on it.
- Click on a parameter of any module in your patch. The slot will bind this parameter.
- Touch a control or key on your MIDI device. The slot will bind the MIDI CC or note message.
- Repeat this process until all the desired parameters have been mapped.

Since v1.7.0 a blinking mapping indicator will indicate the bound parameter the mapping-slot which is currently selected. 

![MIDI-CAT mapping](./MidiCat-map.gif)

If you like to know more on MIDI-mapping in VCV Rack please refer to one of the existing tutorials like [this one](https://www.youtube.com/watch?v=Dd0EESJhPZA) from [Omri Cohen](https://omricohencomposer.bandcamp.com/).

In v1.7.0 new mapping options have been added to MIDI-CAT to achieve even faster mappings without the need for touching every single parameter of a module:

- **Map module (left)**  
  Place MIDI-CAT directly on the left side of the module you like to map. Use the option _Map module (left)_ on the context menu to fill the mapping slots with all parameters of the module. Please note that there are two different variants available: _Clear first_ clears all mappings slots before the slots of MIDI-CAT are filled, _Keep MIDI assignments_ will not clear the assigned MIDI controls but all bindings to parameters. The latter option is useful if you want to reuse the controls of your MIDI device and re-map them onto a different module.  
  Mapping can be also enabled by Ctrl/Cmd+Shift+E (_Clear first_) or Shift+E (_Keep MIDI assignments_).

![MIDI-CAT module left](./MidiCat-map-left.gif)

- **Map module (select)**  
  This option changes your cursor into a crosshair which needs to be pointed onto any module within your patch by clicking on the panel. The variants _Clear first_ and _Keep MIDI assignments_ work the same way as for _Map module (left)_.  
  Mapping can be also enabled by Ctrl/Cmd+Shift+D (_Clear first_) or Shift+D (_Keep MIDI assignments_).

![MIDI-CAT module select](./MidiCat-map-select.gif)

## "Soft-takeover" or "Pickup" for CCs

MIDI-CAT supports a technique sometimes called "soft-takeover" or "pickup": If the control on your MIDI device has a position different to the mapped parameter's position all incoming MIDI messages are ignored until the parameter's position has been "picked up". This method must be enabled for each mapping-slot in the context menu: 

- **Direct**: Every received MIDI CC message is directly applied to the mapped parameter (default).

- **Pickup (snap)**: MIDI CC messages are ignored until the control reaches the current value of the parameter. After that the MIDI control is "snaped" unto the parameter and will only unsnap if the parameter is changed from within Rack, e.g. manually by mouse or preset-loading.

- **Pickup (jump)**: Same as snap-mode, but the control will loose the parameter when jumping to another value. This mode can be used if your MIDI controller supports switching templates and you don't want your parameters to change when loading a different template.

![MIDI-CAT module select](./MidiCat-map-cc.png)

## Note-mapping

MIDI-CAT supports mapping of MIDI note-messages instead of MIDI CC. There are different modes availbale as note-messages work differently to continuous controls:

- **Momentary**: Default setting, when a MIDI note is received the parameter will be set to its maximum value (an MIDI velocity of 127 is assumed).

- **Momentary + Velocity**: same as "Momentary", but the MIDI velocity of the note is mapped to the range of the parameter.

- **Toggle**: Every MIDI "note on" message toggles the parameter between its minimum and maximum value (usually 0 and 1 for switches).

Some controllers with push-buttons don't handle "note off" messages the way the message is intended, hence a mapping-slot can be switched with the option _Send "note on, velocity 0" on note off_ to send a "note on" message with "velocity 0" as MIDI feedback instead (since v1.7.0).

![MIDI-CAT module select](./MidiCat-map-note.png)

## MIDI-feedback

Any parameter change can be sent back to an MIDI output with the same CC or note. "Feedback" is useful for initialization of the controls on the MIDI device if it is supported, especially after loading a patch.

The option _Re-send MIDI feedback_ on MIDI-CAT's context menu allows you to manually send all values of mapped parameters back to your MIDI device (since v1.7.0). This can be useful if you switch your MIDI device while running Rack or the device behaves strangely and needs to be initalized again.

## Additional features

- The module allows you to import presets from VCV MIDI-MAP for a quick migration.

- The module can be switched to "Locate and indicate"-mode: Received MIDI messages have no effect to the mapped parameters, instead the module is centered on the screen and the parameter mapping indicator flashes for a short period of time. When finished verifying all MIDI controls switch back to "Operating"-mode for normal module operation of MIDI-CAT.

- The text shown in every mapping slot can be replaced by a custom text label in the context menu (since v1.4.0).

- If you find the yellow mapping indicators distracting you can disable them on MIDI-CAT's context menu (since v1.5.0).

- Accidental changes of the mapping slots can be prevented by the option _Lock mapping slots_ in the context menu which locks access to the widget of the mapping slots (since v1.5.0).

- Scrolling Rack's current view by mouse is interrupted by MIDI-CAT's list widget while hovered. As this behavior can be annoying all scrolling events are ignored if _Lock mapping slots_ is enabled (since v1.7.0).

- An active mapping process can be aborted by hitting the ESC-key while hovering the mouse over MIDI-CAT (since v1.7.0).

MIDI-CAT was added in v1.1.0 of PackOne. 

# MEM-expander

MEM is a companion module for MIDI-CAT: The expander allows you store an unlimited number of module-specific mappings which can be recalled for the same type of module without doing any mapping manually.  
A typical workflow will look like this:

- Place MEM on the right side of MIDI-CAT.
- Create a mapping using your MIDI device of any module in MIDI-CAT.
- You find a new option _Store mapping_ in the _MEM-expander_-section of MIDI-CAT's context menu. The submenu shows all module-types which are currently mapped in MIDI-CAT. If you mapped only one module in MIDI-CAT there will be only one item.
- The module-mapping is listed under _Available mappings_ in the context menu after storing. The number on the display of MEM will also increase by 1.
- If you like you can repeat this process: Clear the mapping-slots of MIDI-CAT and repeat for another module-type.

Stored module-mappings can be recalled by context menu option _Apply mapping_ or hotkey Shift+V while hovering MIDI-CAT or using the button on the panel of MEM. The cursor changes to a crosshair and the MIDI-mapping is loaded into MIDI-CAT after you click on a panel of module in your patch and MEM contains a mapping for this module-type.

![MEM workflow](./MidiCat-Mem.gif)

MEM should be considered as a sort of "memory-unit" for MIDI-CAT: The module-specific mappings are saved inside the MEM-module and can be exported using Rack's preset functionality on the context menu. This means you can reuse the same mappings in different instances of MIDI-CAT or multiple patches, independently of any current mapping of MIDI-CAT.

MEM is not designed to map and recall mappings for different types of modules the same time. If you desire to recall a specific mapping-setup into MIDI-CAT you can use stoermelder 8FACE which applies a complete setup by loading a preset of MIDI-CAT.

## Tips for MEM

- MEM can store only one mapping of any specific module-type. If you store a mapping for a module which has a mapping already it will be replaced.

- You can remove any mapping using the the context menu _Delete_.

- The push button on MEM can be mapped using any mapping module if like to activate _Apply mapping_ by MIDI or some other command.

MEM for MIDI-CAT was added in v1.7.0 of PackOne.