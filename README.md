# Glow by Chlo — Netlify configuration

[build]
  publish = "."

[[headers]]
  for = "/*"
  [headers.values]
    X-Frame-Options = "SAMEORIGIN"
    X-Content-Type-Options = "nosniff"
    Referrer-Policy = "strict-origin-when-cross-origin"
    Permissions-Policy = "camera=(), microphone=(), geolocation=()"

[[headers]]
  for = "/css/*"
  [headers.values]
    Cache-Control = "public, max-age=604800"

[[headers]]
  for = "/js/config.js"
  [headers.values]
    Cache-Control = "no-cache"

[[redirects]]
  from = "/book"
  to = "/book.html"
  status = 301

[[redirects]]
  from = "/admin"
  to = "/admin/"
  status = 301
