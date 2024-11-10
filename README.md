# Campsite power setup

Motivation for building my own batteryback came originally during 2020 when being outdoors was sough after.
I first bought [the tent](./tent.md) for May Contain Hackers festival and already had a plan to extend the setup with modern commoties.
The tent sleeps 10 soldiers or 4 adults. 
It has a stove for heating and the pieces weight around 10kg each.
This weight become the design criteria for the battery also.

When the project started, there were no options available in Finland.
Today, one can buy a complete package with less from a local store.

## Build timeline

| Timespan    | Description                                                                         |
|-------------|-------------------------------------------------------------------------------------|
| 2021 winter | Planning, parts orders, first build                                                 |
| 2022 summer | Everything in SmartStore box, charging from the grid with DC power supply           |
| 2022 winter | Rugged case for the battery and the accesories                                      |
| 2023 summer | Testing the limits, still charging with DC power supply                             |
| 2023 winter | Planningn for solar extension                                                       |
| 2024 summer | Woods and fetivals with panels and MPPT controller and accesories in SmartStore box |
| Upcoming... | Rugged case for the MPPT controller and tent LED lights                             |
| Upcoming... | Custom VE.Bus driver for the battery with Rust in RPI Pico?                         |

## The Battery bank
The LFP cells were not the biggest expense on the BOM.
A lot of the side costs came from the fact that I didn't have the specialised tools and consumables needed to build the wiring and internals.
Still, on the spotlight is how the LFP cell stores and discharges energy.

![Discharge curve of a cell](./zg20-discharge-3c.jpg)

Cell discharge curve from GWL Power product specs. Note how flat and linear the "power" band is.
BMS needs to measure the voltage accurately as possible. 
Overkill solar measures the cells within 0,0002 volts which is adequate for the purpose.

After the voltage drops below 3 volts per cell, the battery is considered to be empty.
BMS protects individual cells and disconnects the pack when a single cell reaches this limit.
In the assembled pack, number 2 is the worst performing cell hitting the triggering the load disconnect conditions
first. 

![Loading the first cells](./kantosahko_cells_first_charge.png)

Initial charge is done individually with each cell. Proposed loading current is 0.5C and the target voltage for the 
first charge is 3,8V. Consecutive charges can be done with 1C and to 3,65V per cell.
Initial charge takes around 2h for each cell, so be prepared to do this all day.

![First phase done](./kantosahko_1st_phase.png)

Instagram done! Pack is ready for first trials in summer cottage. The results were good, but the portability was not 
there yet. The next phase is to build a strong case with fixed mounting for USB A and C chargers.

## Bill of materials

The prices are what I paid for the item.
As the cost is spread across the whole build this acts as a reminder on how much I have dropped money into this hobby.
For the relevant parts, there are links to store pages, but some are already defunct.
Remeber to store the spec sheets to your own archives!

| Cost item                                                                                                                        | Price             |
|----------------------------------------------------------------------------------------------------------------------------------|-------------------|
| RD6024W 60V 24A DC power supply unit (VAT 0%)                                                                                    | 84,34e            |
| RD6024W 60V 24A Step-down converter with case (VAT 0%)                                                                           | 164,47e           |
| RD6024W import taxes 24%                                                                                                         | 59,71e            |
| [GWL LiFePO4 20H 3,7V cell](https://shop.gwl.eu/LiFePO4-cells-3-2-V/LiFePO4-High-Power-Cell-3-2V-20Ah-Alu-case-CE.html?cur=1) x8 | 301,44e           |
| GWL Power terminals x7                                                                                                           | 34,86e            |
| GWL ADR shipping (FedEx/TNT sucks)                                                                                               | 61,31e            |
| [Overkill BMS](https://overkillsolar.com/product/8s-bms-100a-lifepo4-m6-threaded/)                                               | 161.53e (164,50$) |
| Misc low power connectors                                                                                                        | 23,49e            |
| Misc high power connectors and insulation tape                                                                                   | 47,70e            |
| Misc tools                                                                                                                       | 64,69e            |
| DC cabels                                                                                                                        | 20,40e            |
| Brightsolar 12V/24V USB-A charger and volts display                                                                              | 19,90e            |
| [Peli protector case](https://www.amazon.de/-/en/gp/product/B000M463F0/)                                                         | 144,42€           |
| Aluminium T-bar, 1m                                                                                                              | 7,45€             |
| Aluminium U-bar, 1m                                                                                                              | 6,25€             |
| Aluminium Sheet, 1,5mm                                                                                                           | 18,15€            |
| Rivet gun                                                                                                                        | 34,95€            |
| Rivets, assorted set                                                                                                             | 18,90€            |
| [USB-C PD charger, 24V](https://www.amazon.de/gp/product/B09YPZCN3V/)                                                            | 40€               |
| [Switches](https://www.amazon.de/gp/product/B07JNRH3NS/)                                                                         | 14€               |
| **Total**                                                                                                                        | **1308,88e**      |

## Solar extension

Conviniently, the solar panels also weights around 10kg each.
During the summer of 2024, I noticed that I really don't have to care about the shadows infront of the panels.
The panels are way oversized due to a rash purchase decidsion and available options.

It would have been convinient if I could use only one foldable panel case, but it didn't provide enough voltage for the MPPT controller.
Victron eats 5V from the top, and doesn't do boosting.
The panel voltage hense needs to be around 5V higher than the battery charging voltage to be able to transfer energy to the storage.

Connecting 2 foldable panels in series provides enough voltage even in the cloudy day.
The MPPT controller effectively transforms the excess voltage to more current which makes it possible to harnes energy even in sub-optimal conditions.
In addition, if the panels are set up in a sunny day to a unobstruccted field, the empty battery is charged under an hour.
The inconvinidence of second foldable panel case makes returns in being quite perfect for the all summery usecases: more permanent camp in the woods, or top of during a longer festival.

| Item                                                                                                                                              | Price      | Purpose             |
|---------------------------------------------------------------------------------------------------------------------------------------------------|------------|---------------------|
| [EVI 200 Fold *2](https://www.verkkokauppa.com/fi/product/864451/EVI-200-Fold-taitettava-aurinkopaneeli-200-W)                                    | 2* 175,00€ | Foldable 200W panel |
| [Victron SmartSolar MPPT 100V/20A](https://esconet.fi/shop/scc075010060r-victron-smartsolar-mppt-75v-10a-12-24-v-lataussaadin-bluetoothilla-7574) | 96,42€     | MPPT controller     |
| Misc kables and connectors                                                                                                                        | 6,57€      | Wood-joy            |

## Upcoming additions

All pieces are aiming towards a mobile radio shack/drone base.

| Item                                                                                                                        | Price   | Purpose                |
|-----------------------------------------------------------------------------------------------------------------------------|---------|------------------------|
| [iCharger X8](https://www.stefansliposhop.de/en/chargers-power-supplys/junsi/junsi-icharger-x8-charger-1100w-8s::2053.html) | 179,90€ | Low flying helicopters |

