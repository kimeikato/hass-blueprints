# Clockify Blueprints

## REST-Command example
```yaml
rest_command:
  post_time_entry:
    url: "https://api.clockify.me/api/v1/workspaces/{{ workspaceId }}/time-entries"
    method: POST
    headers:
      x-api-key: !secret clockify_api_key
      Content-Type: "application/json"
    payload: '{"start": "{{ start }}", "end": "{{ end }}", "projectId": "{{ projectId }}", "tagIds": ["{{ tagId }}"], "description": "{{ description }}"}'
    content_type: "application/json; charset=utf-8"
```