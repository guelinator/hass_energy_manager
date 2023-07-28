Energy Manager
----

Das Energiemanagement dient dazu Geräte bei vorhandenem PV Strom ein-, und bei wenig PV Strom aus-zuschalten.

Geräte müssen einen "Leistungsbedarf" anmelden.
Folgende sensoren können dazu verwendet werden:
- sensor.leistungsbedarf_{NAME}
- input_number.leistungsbedarf_{NAME}

Diese Entitäten müssen sich in der Area "Energiemanagement" befinden, damit sie vom Energiemanagement gefunden werden.
{NAME} steht immer für ein Gerät. Dieser Name wird noch weitere male verwendet.

