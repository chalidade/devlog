# Storing User Videos in Their Own Google Drive

[fet](https://chalidade.github.io/fet/)'s learning room records camera and
screen video. Rather than keep everyone's video in my own storage, the files go to the learner's own Google Drive
instead, straight from the browser, with no server of mine in the path.

## The scope

`https://www.googleapis.com/auth/drive.file` lets the app see only files it
created itself. It can't list or read the rest of someone's Drive, so the
consent screen asks for something small and the request is easy to accept.

## Getting a token without a backend

Google Identity Services has a *token client* that returns a short-lived
access token in a popup. There's no redirect URI, no refresh token and no
client secret, only a client ID, and a client ID is public.

```ts
const client = google.accounts.oauth2.initTokenClient({
  client_id, scope: SCOPE,
  callback: (res) => { token = res.access_token },
})
client.requestAccessToken() // must run inside a click handler, or the popup is blocked
```

The token lives in memory with its expiry (minus a minute of margin). When it
runs out, the user clicks connect again.

## Uploading

- **Folders:** `fet-belajar/<stage>/`, found by a `files.list` query on name,
  parent and folder mime type, and created when missing. Names are escaped
  before they go into the query string.
- **Video:** a resumable upload. One POST with the metadata and
  `X-Upload-Content-Type`/`-Length` returns a `Location` URL, then one PUT sends
  the blob. Each recording becomes a new file.
- **Notes and code:** small text files go up as a multipart upload. If a file
  with that name already exists, a media PATCH overwrites it, so exporting twice
  doesn't create duplicates.
- **Sharing:** a recording stays private until the user picks it for a
  community post. Only then does the app add a `reader`/`anyone` permission.

## Gotchas

- While the consent screen is in Testing mode, only listed test users can
  connect. Everyone else gets an access-denied page that looks like a bug.
- The origin has to be listed exactly under *Authorized JavaScript origins*,
  `https://chalidade.github.io` for Pages and `http://localhost:5173` for dev.
  The path (`/fet/`) doesn't matter.

Source: [`docs/.vitepress/theme/lib/drive.ts`](https://github.com/chalidade/fet/blob/main/docs/.vitepress/theme/lib/drive.ts).
