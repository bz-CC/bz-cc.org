+++
title = "Rebuilding the Network at GoodGames Bern"
description  = "A new UniFi network for GoodGames Bern: segmented, remotely managed, and monitored externally."

date = 2026-10-26
+++

> [!NOTE]
> The website of GoodGames Bern: <span class="demo-icon" style="-webkit-mask-image:var(--icon-link); mask-image:var(--icon-link);"></span> [goodgames.gg](https://goodgames.gg/)

## Intro

When [GoodGames Bern](https://goodgames.gg/) moved to a new location, the network couldn't come along. At the old location, the venue ran on the network infrastructure of the [Erupt lounge](https://erupt.ch/en). With the move, GoodGames needed a network of its own, so our association designed and rolled one out from scratch. The goal was a setup that is reliable for staff, welcoming for guests, and easy to operate without being on site.

## Why UniFi

The choice of UniFi was made by the owner before we got involved, with simplicity as the main reason. It turned out to be a good fit. Gateway, switches, and access points are managed from a single controller, which gives one place for configuration, monitoring, and firmware updates.

## Structured cabling

The physical layer was installed in-house by the GoodGames team, with our guidance and support. The building is wired with Cat6A, which provides headroom for 10 Gbit/s over the full channel length and keeps the cabling viable well beyond the current hardware generation. Horizontal runs are terminated on a patch panel in the rack. A clean, documented patch field keeps the connection between the cabling and the switches easy to trace and maintain.

## A clean two-tier design

{{ <image url="network_zones.svg" position="right" alt="Diagram of the network zones" content_path={page.path} /> }}

The network follows a two-tier design: a core and an access layer. The edge gateway and the core switch sit together in the rack and form the core. Leaf switches spread throughout the building act as the access layer, connecting the access points and wired devices in each area. Each leaf uplinks directly to the core, giving a simple star topology.

The design is deliberately straightforward. It is easy to understand, easy to troubleshoot, and easy to extend: adding a new area later just means placing another switch and uplinking it to the core, with no redesign needed.

For a venue of this size, this is the right level of complexity. Redundant cores or a full spine-leaf fabric would add cost and moving parts without a real benefit here.

## Separate zones for staff and guests

Not everyone on the network should have the same access. The network is split into distinct zones:

- **Staff zone:** for internal devices and systems, kept isolated from anything guest-facing.
- **Guest zone:** internet access only, with no path into internal resources.

This segmentation protects day-to-day operations and keeps visitors' devices away from the systems the business relies on.

## Guest Wi-Fi with captive portal

Guests connect to a dedicated Wi-Fi network with a captive portal. On connecting, they land on a splash page where they accept the terms of use before getting online. It makes for a smooth first impression and keeps access controlled and documented.

## Remote management

GoodGames has no IT team of its own, so our association handles support and operation. That only works if the network can be managed without a trip to Bern.

Day-to-day management happens through the UniFi UI, remotely. As a second path, WireGuard provides secure remote access into the network. It serves as a backup if the UniFi UI is unavailable, and as a way to reach devices and services directly when needed.

## External monitoring

Monitoring runs on our own infrastructure, outside the venue's network. Syslog and metrics are collected centrally, and ping alerts notify us when something stops responding. Because monitoring lives outside the site, we are alerted even if the site itself goes down, and we can often start troubleshooting before anyone at the venue notices a problem.

## Public services with dynamic DNS

For services that need to be reachable from outside, dynamic DNS keeps stable hostnames pointing at the site's connection, even if the public IP changes. This avoids the need for a static IP while keeping external services reliably accessible.

## The result

The move turned into an opportunity to build a network that is cleanly structured, segmented by purpose, and fully managed and monitored by us. It is also built to grow: the layout leaves room to expand as GoodGames Bern evolves.
