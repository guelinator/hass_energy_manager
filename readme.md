Energy Manager
----

Das Energiemanagement dient dazu Geräte bei vorhandenem PV Strom ein-, und bei wenig PV Strom aus-zuschalten.

Diese Werte werden mindestens für das Energiemanagement benötigt:
- sensor.energiemanagement_photovoltaik
- sensor.energiemanagement_verbrauch

Für beide Werte empfiehlt es sich einen mean-filter-sensor zu verwenden, das nicht jedes Wölkchen die Geräte aus/einschaltet. Das Energiemenagement wird alle 5 Minuten ausgeführt, und deswegen sollten auch die mean-filter 5 min als zeitfenster haben.
      
      - platform: filter
        name: "Energiemanagement Photovoltaik"
        unique_id: "energiemanagement_photovoltaik"
        entity_id: sensor.leistung_pv_raw
        filters:
          - filter: time_simple_moving_average
            window_size: "00:05"
            precision: 0

Leistungsbedarf
---
Geräte müssen einen "Leistungsbedarf" anmelden.
Folgende sensoren können dazu verwendet werden:
- sensor.leistungsbedarf_{name}
- input_number.leistungsbedarf_{name}

Diese Entitäten müssen sich in der Area "Energiemanagement" befinden, damit sie vom Energiemanagement gefunden werden.
{name} steht immer für ein Gerät. Dieser Name wird noch weitere male verwendet. z.b. sensor.leistungsbedarf_pool


Schalter
---

Um die Geräte schalten zu können, ist eine der folgenden Entitäten notwendig:
- switch.schalte_{name}_em
- input_boolean.schalte_{name}_em
- switch.schalte_{name}
- input_boolean.schalte_{name}

Das erste Gerät das gefunden wird, wird verwendet, falls mehrere vorhanden sind.

Priorität
---

Pro Gerät kann eine Priorität festgelegt werden. Das Gerät mit der höchsten Priorität das einen Bedarf anmeldet wird als erstes eingeschaltet, und das Gerät mit der geringsten Priorität wird als erstes ausgeschaltet, wenn zu wenig PV Leistung vorhanden ist.

Die Priorität kann mit folgenden Entitäten festgelegt werden:
- input_number.prioritat_{name}
- sensor.prioritat_{name}
Die Werte sollen im Bereich -100 bis +100 sein.

Dauer
---

Pro Gerät kann auch eine Mindest-Dauer (in Stunden) festgelegt werden, die das Gerät eingeschaltet bleiben muss.

Die Dauer kann mit folgenden Entitäten festgelegt werden:
- input_number.dauer_{name}
- sensor.dauer_{name}

Energiemanagement-Card
---

Wenn man den Code von command: der datei energiemanagement_pv.yaml nimmt, die spaces davor löscht, und
    {% set debug = true -%}
einträgt, dann kann man den Content in eine Markdown-Card geben, und sieht somit was das Energiemanagement macht.

Beispiel
---

Beispiel 1:

| entität | wert | area |
|---------|------|------|
| sensor.leistungsbedarf_pool| 900 | Energiemanagement |
| input_boolean.schalte_pool_em | false | egal |
| input_number.prioritat_pool | 3 | egal |
| input_number.dauer_pool | 3.0 | egal |


Beispiel 2:

| entität | wert | area |
|---------|------|------|
| input_number.leistungsbedarf_pool| 900 | Energiemanagement |
| switch.schalte_pool | false | egal |
| sensor.prioritat_pool | 3 | egal |
| sensor.dauer_pool | 3.0 | egal |
