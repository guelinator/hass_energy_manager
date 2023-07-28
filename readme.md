Energy Manager
----

Das Energiemanagement dient dazu Geräte bei vorhandenem PV Strom ein-, und bei wenig PV Strom aus-zuschalten.

Diese Werte werden mindestens für das Energiemanagement benötigt:
- sensor.energiemanagement_photovoltaik
- sensor.energiemanagement_verbrauch

Es empfiehlt sich einfach einen Template-Sensor zu erstellen, um die eigenen Werte auf die Werte des Energiemanagements zu spiegeln. z.B. so:

  - name: "Energiemanagement Photovoltaik"
    unique_id: "energiemanagement_photovoltaik"
    unit_of_measurement: "W"
    icon: mdi:arrow-decision-auto
    state: >
      {{ states("sensor.leistung_pv_gemittelt") }}


Geräte müssen einen "Leistungsbedarf" anmelden.
Folgende sensoren können dazu verwendet werden:
- sensor.leistungsbedarf_{name}
- input_number.leistungsbedarf_{name}

Diese Entitäten müssen sich in der Area "Energiemanagement" befinden, damit sie vom Energiemanagement gefunden werden.
{NAME} steht immer für ein Gerät. Dieser Name wird noch weitere male verwendet.

Um die Geräte schalten zu können, ist eine der folgenden Entitäten notwendig:
- switch.schalte_{name}_em
- input_boolean.schalte_{name}_em
- switch.schalte_{name}
- input_boolean.schalte_{name}

Das erste Gerät das gefunden wird, wird verwendet, falls mehrere vorhanden sind.

Pro Gerät kann eine Priorität festgelegt werden. Das Gerät mit der höchsten Priorität das einen Bedarf anmeldet wird als erstes eingeschaltet, und das Gerät mit der geringsten Priorität wird als erstes ausgeschaltet, wenn zu wenig PV Leistung vorhanden ist.

Die Priorität kann mit folgenden Entitäten festgelegt werden:
- input_number.prioritat_{name}
- sensor.prioritat_{name}


Pro Gerät kann auch eine Mindest-Dauer festgelegt werden, die das Gerät eingeschaltet bleiben muss.

Die Dauer kann mit folgenden Entitäten festgelegt werden:
- input_number.dauer_{name}
- sensor.dauer_{name}

