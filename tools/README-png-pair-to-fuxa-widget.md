# PNG Pair To FUXA Widget

Tool file:

- `png-pair-to-fuxa-widget.html`

## Usage

1. Open `png-pair-to-fuxa-widget.html` in a browser.
2. Choose the `OFF` PNG.
3. Choose the `ON` PNG.
4. Set the widget name and optional label.
5. Click `Generate SVG`.
6. Click `Download SVG`.

## After Generating The SVG

Place the generated SVG in a FUXA widget folder such as:

- `FUXA/widgets/smartfarm-examples/`

Then refresh the FUXA editor and open `Widgets Kiosk`.

## What The Widget Does

- supports 2 states: `OFF` and `ON`
- uses `_pb_state` for display state
- uses `_ps_label` for optional text
- can generate either boolean command widgets or Smartfarm raw JSON command widgets

## Smartfarm Raw Command Mode

When `Smartfarm raw command mode` is enabled:

- the generated widget posts through `_ps_cmd` instead of `_pb_cmd`
- the widget toggles visually on each click
- the outbound payload is a JSON string such as:

```json
{"action":"write_bit","type":"Y","addr":4,"value":true}
```

and then:

```json
{"action":"write_bit","type":"Y","addr":4,"value":false}
```

Main bindings in FUXA:

- `_ps_cmd` -> raw MQTT publish tag
- `_pb_state` -> optional feedback tag if the image must follow real device state

## Working Toggle Method For Lab/View

Use this pattern when the widget should alternate between `true` and `false`
on each click in real FUXA runtime:

1. Bind `_ps_cmd` to one raw MQTT publish tag such as `CMD_Y4`.
2. Leave `_pb_state` at default `false` during the first test, or bind it only
   to a real boolean or `0`/`1` feedback tag.
3. Keep `_ps_action`, `_ps_type`, and `_pn_addr` at the needed command values.
4. Do not add a shape `Events -> Set Value` row on the same widget when you
   want the SVG widget script itself to toggle.
5. Test in `Lab` or `View`.

Expected payloads:

- first click -> `{"action":"write_bit","type":"Y","addr":4,"value":true}`
- second click -> `{"action":"write_bit","type":"Y","addr":4,"value":false}`

## Important Reload Rule

- FUXA can keep the processed widget script inside the existing placed widget
  instance.
- If you edit the SVG file on disk and behavior does not change, remove the
  old widget from the view and drag the updated SVG in again.
- Custom publish widgets also need a declared placeholder function:

```js
function postValue(id, value) {
  console.error('Not defined!', id, value);
}
```

Without that placeholder, a standalone browser preview may still look correct
while the real FUXA Lab/View widget stays silent.

## Notes

- The widget embeds the PNG files as data URLs inside the SVG.
- Large source PNGs can make the final SVG large too.
- If needed, shrink or optimize PNGs before importing them.
