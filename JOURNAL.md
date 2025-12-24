# 24 Dec - Official Start
Spent time: (notas, deletar depois: tempo do cronometro + 2 horas)

Hello! Atsom here again with another project that has potential to get abandoned/unfinished!! Decided to speedrun a project in the last week of Blueprint (i ended up procrastinating too long)

Anyways, onto the actual project. Before today's official start, i was stuck laid down on the couch, looking through online stores to check for prices of speedcubing timers:

> "This one is $50, $55, $53.99... holy shit, this one's $100"

And i just decided that buying a physical timer isn't worth dropping big bucks on, after all, most of us are bored teenagers with lots of wishes and not lots of money. So i thought, why not design one, and finally start that Blueprint project i've been procrastinating for so long! So then i started a few days ago. Sat in my chair spinning around, brainstorming for good way to make a timer start mechanism, since actual flagship timers aren't pushbutton/switch based, people just touch them, and they work!

> "Should i just do it differently and add pushbutton- no, they're just too small"

Then it hit me. Capacitive switches. The things that revolutionized your pocket screens, AKA phones. They do not need any strong pressing forces to activate, just a simple light touch! No small switches, no hassle!
But then another issue hit me. There were no consumer-grade capacitive switches big enough to cover the whole palm's surface. I searched, searched, searched. 

Closest thing i found was this: https://imgur.com/a/p0qPnuM

I was lost again. If not capacitive switches, easy to use, easy to configure, what else would i use??? Plus, even if i had found a good capacitive switch -- the PCB would end up getting too big, bumping up the PCB prices quite a bit.
Turns out, i had the wrong thinking process. Why just buy premade PCB switches? I could just easily make my own switches using only the IC in a capacitive switch + conductive material!!

Plus, i decided to think how the companies that make the timers think. So i decided to watch a [QUALITY teardown video](https://www.youtube.com/watch?v=oFdWaF1P40I) to take a look at the internals.
What i could make out from the components, were the (i assume) proprietary capacitive switches embedded inside the plastic, then connected to the bottom corners of the PCB, then obviously, the main PCB. https://imgur.com/a/Lb7D4VR

Notice the timer doesn't have a big PCB, with the switches on it. It's a small board with the sensors connected externally.
So now i have an idea of what to work with.

I searched again, but this time, for the ICs of the capacitive sensors. And i found a good one!

In this case, i've decided to use a single AT42QT1010 for each side.

The AT42QT1010 is a digital burst mode charge-transfer sensor by Microchip that is capable of detecting near proximity or touch, making it ideal for implementing touch controls. ( Source: [Datasheet](https://ww1.microchip.com/downloads/aemDocuments/documents/OTH/ProductDocuments/DataSheets/40001946A.pdf) )

It's perfect. Small. Cheap. Only a few pins, that makes it perfect to just throw it around anywhere and route easily. I could cram all this into a super small PCB and cut costs even more if i had more skill. But it's gonna be an average size. So based on this knowledge, i started working. At night. 21h (or 9pm) to be specific.

> What? Sleep? There's no good designer without their sleep deprivation!!!

So now, my basic idea of components for now.

- An ESP32 of any series 
- Capacitive sensors
- USB port (obviously)
- Battery and battery charging circuit to make it portable
- 3.5mm jack to transfer data
- And a good, colorful display so you can get faster times with rainbow puke RGB

This is the proof of concept schematic i've arrived at now. https://imgur.com/a/sionhMd

For the MCU, i chose the ESP32-S3 because of its builtin USB HID and serial USB controller, less components on the board; As i mentioned before, i will be working with the AT42QT1010 capacitive sensor; Plus regular USB-C port for charging and data transfer, being it either firmware updates, or sending data up to your favorite timer app; Audio jack; I still haven't decided on battery size / capacity since i have no expectation of current draw, so i can't really estimate a battery size, but i will be using a famous battery charging IC, the [BQ24074](https://www.ti.com/product/BQ24074). That's gonna be my "beta" of the project. Like any project, changes are to be expected, being such changes big or small, either i discover one of these components are NRND, not available at LCSC, or i just wake up the next day with an urge to revamp EVERYTHING.



