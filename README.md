# Container Shipping (DCSA)

How container shipping is booked, documented and tracked between shippers and ocean carriers -- bookings, shipping instructions and transport documents (the electronic bill of lading), vessel and port schedules, and track-and-trace events. The shape is owned by the Digital Container Shipping Association (DCSA) standards, so this context publishes DCSA's own objects and measures who implements them.

**A reference context.** The shape belongs to [dcsa-2025](https://dcsa.org/standards) (Apache-2.0). This repository does not restate or rename it: `schema/` holds the standard's own objects, each linked to the release it was read from, and `crosswalk/` measures, from each provider's harvested OpenAPI, which operations it implements and what share of the standard's request and response fields it carries.

Measured across 300 providers tagged Maritime, Shipping, Ocean Freight, Ports, Vessel Tracking, Logistics, Freight, Supply Chain, Supply Chain Visibility, Freight Forwarding, Container Shipping in [APIs.io](https://apis.io): **3 implement the standard**; 4 name it somewhere in a spec.

## The standard's APIs

| API | Release | Implementers | Operations |
| --- | --- | ---: | --- |
| track-and-trace | [2.2.0](https://app.swaggerhub.com/apis/dcsaorg/DCSA_TNT/2.2.0) | 1 | `GET /events`, `GET /events/{eventID}` |
| booking | [2.0.4](https://app.swaggerhub.com/apis/dcsaorg/DCSA_BKG/2.0.4) | 2 | `POST /bookings`, `GET /bookings/{bookingReference}` |
| ebl | [3.0.3](https://app.swaggerhub.com/apis/dcsaorg/DCSA_EBL/3.0.3) | 2 | `POST /shipping-instructions`, `GET /shipping-instructions/{documentReference}`, `GET /transport-documents/{transportDocumentReference}` |
| commercial-schedules | [1.0.3](https://app.swaggerhub.com/apis/dcsaorg/DCSA_CS/1.0.3) | 1 | `GET /point-to-point-routes`, `GET /port-schedules`, `GET /vessel-schedules` |
| operational-vessel-schedules | [3.0.2](https://app.swaggerhub.com/apis/dcsaorg/DCSA_OVS/3.0.2) | 1 | `GET /service-schedules` |

## Implementers

Coverage is the best-matching operation's share of the standard's fields, per API.

| Provider | APIs (field coverage) |
| --- | --- |
| [evergreen-marine](https://apis.io/providers/evergreen-marine/) | booking 89%, commercial-schedules 80%, ebl 98%, objects 98%, track-and-trace (1 operations) |
| [kuehne-nagel](https://apis.io/providers/kuehne-nagel/) | objects 62% |
| [maersk-line](https://apis.io/providers/maersk-line/) | booking 18%, ebl 17%, operational-vessel-schedules 75% |

## Findings

- Three carriers and forwarders implement DCSA in their own published OpenAPI, out of 300 maritime, freight and supply-chain providers measured. evergreen-marine implements booking, eBL, commercial schedules and track-and-trace, carrying 71-98% of each object's fields; maersk-line publishes DCSA booking, eBL and schedules under /dcsa/ paths; kuehne-nagel publishes a DCSA equipment event.
- The maritime and supply-chain census contexts found vessels, positions and tracked shipments agreeing on almost nothing. The carriers that agree do so by implementing DCSA, not by converging on their own.

## Decisions

- An operation is matched when its path or server names DCSA, or, matched on path alone, when it carries at least 30% of the standard object's fields: /bookings and /events are too common to count by path.
- Pinned to the latest final (non-beta) version of each DCSA API on SwaggerHub at measurement time, fetched resolved so the shared domain components are inlined.

## Licence

Measurements (profile, crosswalks, adopters) are CC BY-NC-SA 4.0; code is Apache 2.0. The standard's objects in `schema/` remain under the standard's own licence (Apache-2.0).
