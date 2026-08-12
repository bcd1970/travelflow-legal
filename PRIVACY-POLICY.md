# TravelFlow Privacy Policy

**Last updated: 2026-08-12.** If this policy changes, the new version will
be published at the same URL as this one.

This policy applies to the TravelFlow app and takes effect when the app is
published on Google Play — the app is not yet released.

## What TravelFlow is

TravelFlow is a tool you run on your own phone to track business trips
across EU countries and work out the per-diem you're owed. It is not a
service that watches you — it's software that runs when you tell it to,
records what it needs to do its job, and keeps that record on your device.

## What the app collects

While you have a trip running, TravelFlow records your location — including
while the screen is off and the app is in the background. This is how it
knows which country you're in, how long you stayed, and when you crossed a
border. From that it builds:

- Trip records (start/end times, route, countries visited, days spent)
- Per-diem calculations based on those trip records
- Registered cell-tower identifiers (a country code, cell ID, and whether
  the phone is registered to that cell) — used only as a quick cross-check
  for which country you're in, alongside GPS
- A local diagnostics log: technical events, roughly-per-minute device
  state snapshots (things like whether the screen is on, the phone's power
  standby state, and how many location fixes have landed recently), and
  session records tagged with the app's build number. This is
  troubleshooting data about how the app itself is behaving, not a record
  of your activity for its own sake — but some of these diagnostic events
  do include coordinates (see "Standing by" below).

All of this is stored in a database on your device. TravelFlow does not
have a cloud sync feature in this version of the app — nothing here is
routinely uploaded to a server we run.

## What leaves your device, and to whom

A few things in TravelFlow do send data off your phone. All of them go to
Google, through Android's own location and geocoding services — not to us,
and not to any third party we chose.

**Place names.** To show you a readable place name (a city, a street, an
address) instead of raw GPS coordinates, TravelFlow uses Android's
`Geocoder` service. On most Android phones — including this one — that
service is implemented by Google Play services, which means the
coordinates you're asking to be turned into a place name are sent from
your device to Google to do that lookup. This happens every time the app
resolves a place name — when you open the Home screen, when it labels a
trip's start/end/border points, and when you search an address — not
occasionally, not as an edge case. Once sent, that data is handled under
Google's own privacy policy, not this one.

**Network-based location fixes.** When TravelFlow isn't actively tracking a
trip at high accuracy, it asks Android's fused location provider for a
lower-power fix (`PRIORITY_LOW_POWER` / `PRIORITY_BALANCED_POWER_ACCURACY`).
On Android, those lower-power fixes are typically produced by Google Play
services from nearby Wi-Fi and cell-tower signals, which it sends to
Google's servers to work out a location — the same as network-location
does for any Android app. TravelFlow doesn't do this itself; it asks the
OS for a location and Google's infrastructure is what answers.

**The standing-by geofence.** Even when no trip is active, TravelFlow keeps
one OS-level geofence registered through Google Play services' geofencing
client, centered on the location where your last trip ended (or, before
any trip has ever ended, wherever the app first anchored itself). This
lets the OS notify the app when you leave or return to that area, so it
can offer to start or end a trip — without the app itself having to keep
checking your location constantly. This fence is re-registered every time
you open the app and after every device reboot, and stays in place at all
times you're not on an active trip. The anchor coordinates are stored on
your device; registering the fence itself is one more thing handled by
Google's location infrastructure, the same way the fixes above are.

**Exporting a report.** If you choose to export a trip (Trips screen →
export), TravelFlow writes a CSV and PDF file on your device and opens
Android's share sheet so you can send it wherever you choose — email, a
file app, cloud storage, anywhere. That's a file leaving your device
because you asked it to; TravelFlow doesn't pick a destination or send it
anywhere on its own.

## Standing by: what happens with no trip active

TravelFlow only tracks your route and builds trip records while a trip is
running, and trips are started manually — see "Why background location"
below. But two things happen even when no trip is active:

- The standing-by geofence described above stays registered, so the OS is
  watching one fixed location (your last trip's end point) at very low
  power, waiting for you to leave or return to it.
- Every time you open the Home screen, TravelFlow fetches your last known
  location and reverse-geocodes it (see "Place names" above) to show a
  current-location line on the Home screen — even if you haven't started a
  trip.

Neither of these builds a trip record or a location history — they're used
to show you where you are right now and to know when to offer to start or
end a trip.

## What the app does NOT do

- No user accounts. There is no login and nothing to sign up for.
- No advertising. There are no ad SDKs in the app.
- No third-party analytics or crash-reporting SDKs. Nothing from Google
  Analytics, Firebase, or similar services is built into the app, and
  nothing about how you use the app is sent to us or to any analytics
  company. (The on-device diagnostics log described above is a separate,
  first-party thing: it stays on your device and app code never transmits
  it anywhere.)
- No selling or sharing your data with third parties.
- No cloud upload of your GPS traces or trip history by us. The Geocoder,
  network-location, and geofencing traffic described above go to Google's
  own infrastructure as part of using Android's location services — not to
  a server we run.

The app does not declare Android's `INTERNET` permission for itself. The
network traffic described above is handled by Google Play services
directly, not by app code we wrote.

## Why background location

TravelFlow tracks a trip while you're travelling — driving, on a train, on
a flight — with your screen off, because that's when a business trip
actually happens. For that to work, the app needs permission to see your
location in the background while a trip is active.

Trips are started manually. TravelFlow does not start recording a trip on
its own — you tell it a trip has begun, and full route tracking runs only
for the duration of that trip. (The lower-power standing-by geofence
described above runs at other times too, but it does not build a trip
record.)

## Your control over your data

Everything TravelFlow collects lives in a database on your phone.
Settings → Delete All Data removes:

- Trip records, crossings, and per-diem calculations
- Cell-tower samples
- App settings (reset to defaults)

It does **not** remove:

- The on-device diagnostics log described above (event, heartbeat, and
  session records, including the coordinates in NIGHT_ANCHOR_FIX and
  GEOFENCE_ENTER/EXIT events) — this is a separate database from your trip
  data and today's Delete All Data feature doesn't clear it.
- Any report files you've already exported (`trip-<id>.csv`/`.pdf` on your
  device) — those are ordinary files once created, and deleting your trip
  data doesn't delete copies you've already made.

Uninstalling the app removes everything — the trip database, the
diagnostics log, and any exported report files, all of which live in the
app's own storage.

You can also delete a single trip from the trip list, rather than
everything at once.

## How long data is kept

Trip and per-diem data stays on your device until you delete it yourself —
either by deleting individual trips, using Delete All Data in Settings, or
uninstalling the app. The on-device diagnostics log and any exported report
files persist until you uninstall the app, as described above. TravelFlow
does not automatically expire or delete your data on its own.

## Legal basis for processing (GDPR Article 6)

TravelFlow only processes your location and trip data because you choose
to use the app for that purpose. Starting a trip is an active choice you
make each time, and that choice is your consent (Article 6(1)(a) GDPR) for
that trip's location processing. You can withdraw that consent at any time
by not starting a trip, by turning off location permission for the app, by
deleting your data, or by uninstalling the app.

## Your rights

Because everything TravelFlow collects is stored on your own device, you
already hold and control that data directly. You still have the rights
GDPR gives you over data processed about you, and here's what they mean in
this app today:

- **Access**: everything is visible in the app itself — the trip list, trip
  details, and per-diem figures.
- **Rectification**: TravelFlow doesn't currently have an in-app way to
  edit a recorded trip's details. If a trip record is wrong, the way to
  correct it today is to delete that trip and, if needed, contact us (see
  below).
- **Erasure**: delete an individual trip, use Delete All Data, or
  uninstall the app (see "Your control over your data" above for exactly
  what each removes).
- **Portability**: export a trip as CSV/PDF from the Trips screen — that
  file is yours to take anywhere.
- **Objection**: since processing only happens when you choose to start a
  trip, objecting means not starting one, revoking the location
  permission, or uninstalling the app.
- **Complaint**: if you believe your data has been mishandled, you can
  lodge a complaint with your national data protection supervisory
  authority (in the EU, this is the authority for the country you live
  in), in addition to contacting us directly.

## International data transfers (GDPR Article 13(1)(f))

As described above, place-name lookups, network-location fixes, and
geofence registration are all handled by Google Play services, which sends
the relevant coordinates to Google. Google is a global company and may
process that data outside the EU/EEA, under Google's own privacy policy
and its own data-transfer safeguards — we don't control where Google
processes it once it's sent. This is the one point at which your location
data leaves the protections of this policy.

## Children

TravelFlow is a business-travel tool, not directed at children. It is not
intended for use by anyone under 16 — the general baseline age GDPR sets
for a child to consent for themselves (some EU countries set it as low as
13, but 16 is the safe assumption here). We have no way to verify a user's
age. If we become aware that a child has used the app and it holds their
data, we'll ask that Delete All Data be used, or the app uninstalled, to
remove it — the same tools any user has.

## Data controller

Dumitru-Bogdan Cozmita

A postal address for the data controller will be added here before this
policy is used for a live Play Store submission.

## Contact

bogdan.appdev@gmail.com
