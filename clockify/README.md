# Clockify Blueprints

## Notification example to use in `clockify-commute.yaml` blueprint
```yaml
service: notify.mobile_app_pixel_6
data:
  title: Fahrzeit
  data:
    notification_icon: mdi:train-car
    channel: fahrzeiten
    tag: fahrzeiten
    actions:
      - action: SUBMIT_FAHRZEIT
        title: >-
          Ankunft {{ as_timestamp(expand(end_time)[0].state) |
          timestamp_custom('%-H:%M', true) }}
      - action: SUBMIT_FAHRZEIT_NOW
        title: Aktuelle Uhrzeit
  message: |-
    Start: {{expand(start_time)[0].state }}
    Stop: {{expand(end_time)[0].state }}

```

## REST-Command example (required for `clockify-submit-fahrzeiten.yaml`)
```yaml
# configuration.yaml
...


rest_command:
  post_time_entry:
    url: "https://api.clockify.me/api/v1/workspaces/{{ workspaceId }}/time-entries"
    method: POST
    headers:
      x-api-key: !secret clockify_api_key
      Content-Type: "application/json"
    payload: '{"start": "{{ start }}", "end": "{{ end }}", "projectId": "{{ projectId }}", "tagIds": ["{{ tagId }}"], "description": "{{ description }}"}'
    content_type: "application/json; charset=utf-8"

...
```
