---
{
  "authentication": "", 
  "description": "Return a list of service hooks bound to a project.", 
  "example_request": "GET /api/0/projects/the-interstellar-jurisdiction/pump-station/hooks/ HTTP/1.1\nHost: sentry.io\nAuthorization: Bearer {base64-encoded-key-here}", 
  "example_response": "HTTP/1.1\nContent-Length: 89\nX-XSS-Protection: 1; mode=block\nContent-Language: en\nX-Content-Type-Options: nosniff\nVary: Accept-Language, Cookie\nAllow: GET, POST, HEAD, OPTIONS\nX-Frame-Options: deny\nContent-Type: application/json\n\n{\n  \"detail\": [\n    \"You do not have that feature enabled\"\n  ], \n  \"error_type\": \"unavailable_feature\"\n}", 
  "method": "GET", 
  "parameters": null, 
  "path_parameters": [
    {
      "description": "the slug of the organization the client keys belong to.", 
      "name": "organization_slug", 
      "type": "string"
    }, 
    {
      "description": "the slug of the project the client keys belong to.", 
      "name": "project_slug", 
      "type": "string"
    }
  ], 
  "query_parameters": null, 
  "sidebar_order": 7, 
  "title": "Projects"
}
---