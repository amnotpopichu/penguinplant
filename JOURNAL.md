# June 1st: WAKE UP ITS THE FIRST OF THE MONTH
RAHH BATTERY WIRING WE LOVE STAYING UP ON ABSURD TIMES TO WORK ON KICAD CUS JETLAG RAHHHHHH
anywyas i spent a lot of time today reading through documentaiton (ewwwww) of the BQ24074RGTR i will be using to control my battery + lipo. i got stuck on a few things and will deal with en1 and ilim another time. otherwise hopefully it will work !! i need to add usb port for it next (i have NO clue how usb works so i bet im in for a treat)
https://lapse.hackclub.com/timelapse/Dbl2Vt9vdpjg
**Total time spent: 0.5 hours**

# June 29th: KICAD RAHHHHHH
GUESS WHO FINALLY GOT AROUND TO WIRING THINGS ME RAHHHHHHH. okay its like really late so lets go through what I did. The main things I did was do all of the mcu wiring (woah i didnt know i could do it). This took an really long time. why? cus im really dumb. took me a good few minutes to find the schematic, then took me time to reailze the example schematic and my schematic can differ.

Here are some key things i learned/did today:
1. was reminded that xtal32k isnt useful to me (i dont need exact precice timing)
2. was REALLY happy to learn i didn't have to wire LNA_in because im not doing wifi
3. figured out that all of the MT stuff is mainly for debugging (but because this will work first try i hopefully wont have to use for funny hardware debugging)
4. i learned what a decopuling capacitor is !! pretty much to my knowledge it just acts as a little backup, so things dont really go wrong (ie dropped voltage)
5. rx and tx are important for flashing data 
6. i have to use inductors. what is an inductor? i dont really know. something about filtering out noise 
7. crytsals somehow keep time. dont ask me how they just do. also there is a funny formula somewhere that the longer the traces are to the crystal teh change in capacitator needed!! 

Anyways I need to deal with battery management another time. quick thanks to [@JBlitzar](https://github.com/JBlitzar) bc i based my flashing mechanism off of his (did you know that gpio9 is now legacy or something and gpio0 is now boot for some c3 chips??)
![image name](journal_imgs/kicad_jun_29th.png)
**Total time spent: 1.5 hours**

# June 19th: uh kicad work i guess
i added more gpio pins. im struggling to find where my 3.3v will come out on the pinout of the esp but welp that seems like a later issue. also did some quick wiring while looking at documentation (ima cry). I think i will focus on wiring up sensors first, and next priority is figuring out where 3v3 comes from.
![image name](journal_imgs/kicad_jun_19th.png)
**Total time spent: 0.25 hours**

# June 14th: sensor work
i orginally thought i would need 90 degree joints and funny pcb design but i had the amazing realization that oh wait wires exist! so thats somekthing to remeber. another thing i should keep in mind is that my water should prob be in a different container than my electronics otherwise that could be kinda bad!

I will also be using stuff from JLC for pcba work:
- [esp32 s3](https://jlcpcb.com/partdetail/EspressifSystems-ESP32S3/C2913192)
- [AO3400A mosfet](https://jlcpcb.com/partdetail/Alpha_OmegaSemicon-AO3400A/C20917)
ill add flyback diodes later when i figure them out. guess who just learned global labels are different than regular after making a stupid amount of regular labels!

![image name](journal_imgs/kicad_jun_14.png)
**Total time spent: 0.5 hours**
# June 13th: understanding
cool! realizing the hole im digging myself into with qfn. anyways lets understand some parts today. (im procrastionating on reading data sheets).
1. sheets in kicad exist! press s to use them. apparently hierarical vs global labels vs power labels, but for my project i shall stick with global. 
2. things exist! heres some i will use while designing <br>a. [schematic checklist](https://docs.espressif.com/projects/esp-hardware-design-guidelines/en/latest/esp32s3/schematic-checklist.html)
<br> b. [datasheet](https://documentation.espressif.com/esp32-s3_datasheet_en.pdf) <br> c. [hardware design guidelines](https://docs.espressif.com/projects/esp-hardware-design-guidelines/en/latest/esp32s3/esp-hardware-design-guidelines-en-master-esp32s3.pdf)
3. crystal things exist! (i have only used xiao modudles and wroom dev modules so this is brand new to me). pretty much it needs to do funny timing stuff, so i need to make a "clock" with the xtal_p and xtal_n pins. the 32k ones are if i need precice timing during deep sleep (which i dont really). otherwise it turns out they can become gpio!
4. VDD is pretty much powering everything
5. PU chip is pull up. kinda important to keep EVERYTHING running. it apparently just makes the chip not turn on if its not pulled up. yikes!
5. strapping pins exist! its cool. it tells chippy what to do WHLIE booting. maybe avoid them! (and then also use them when i actaully need to)
6. there are a lot of vdds. also some do other things like rtc. idk why but hopefully i figure it out at some point
7. avoid gpio 19 and 20 cus they are part of usb pins
8. SPI pins importnat. idk what they do yet. it seems i will use them to flash stuff. i will look into this more later.
9. MT pins are debug dont really touch cus i dont need i can use as gpio ig uess
10. U0. maybe these are the real flashing pins. i dont know yet
11. gpio0 important i needd reset pin for flash (maybe)
12. adc 2 pins dont work with wifi (no clue why)
13. weak pulldown exists

![image name](journal_imgs/examplesch.png)


**Total time spent: 0.75 hours**


# June 10th: parts
okayyy so i decided ima do fully SMD PCBA with the xiao s3 chip itself, rather than the xiao xiao! i wanted to do this because i feel like it will be a much harder challenge, and will be more fun (aka work), and allow me to grow as a builder a lot more. TIL that lcsc's parts library is NOT the same as JLCPCB's part library even tho they source from LCSC. welp i guess they source form other places too. also i will be switching to an s3 for performance.
![image name](journal_imgs/jlcss.png)

**Total time spent: 0.5 hours**


# June 9th: Research & parts
goals:
Do parts research on what is needed

okay starting off with making an aliexpress acc to go buy parts (and look for them). genuienly bottom 5 site ive ever used. took me a while to get an acc (i deflated). anyways hope they r happy with my phone number. anyways for board type i think i will go with the xiao c3. i looked for a while on cheaper alternatives, but its minimal at best, and i think all in with the TP4056, and other work, it may just make more sense in general to go with the xiao c3. (also free shipping :D). genuienly looking for water pump took wAYY too long but lowk im a chud and couldnt find one. TIL what a mosfet is and i need to use one bc current draw exists. I also learned about a flyback diode, while I don't fully get it, it seems i may need one.

Parts List:\
[xiao c3](https://www.aliexpress.us/item/3256808605622611.html?spm=a2g0o.productlist.main.1.f86f1eaaJPPy2l&algo_pvid=88fe9a7b-8031-485e-a902-32c6e2d28adc&algo_exp_id=88fe9a7b-8031-485e-a902-32c6e2d28adc-0&pdp_ext_f=%7B%22order%22%3A%221094%22%2C%22eval%22%3A%221%22%2C%22fromPage%22%3A%22search%22%7D&pdp_npi=6%40dis%21USD%217.84%210.99%21%21%217.84%210.99%21%402140f54217810074411744749ec564%2112000052930246748%21sea%21US%210%21ABX%211%210%21n_tag%3A-29910%3Bd%3A5c316ac3%3Bm03_new_user%3A-29895%3BpisId%3A5000000207262921&curPageLogUid=44k5NjULlTpP&utparam-url=scene%3Asearch%7Cquery_from%3A%7Cx_object_id%3A1005008791937363%7C_p_origin_prod%3A)\
[lcd screen](https://www.aliexpress.us/item/3256804295713253.html?spm=a2g0o.productlist.main.1.57fa40e7AM37Lp&algo_pvid=efa5b5ae-d43f-4a1b-8b82-3127da3e38ec&algo_exp_id=efa5b5ae-d43f-4a1b-8b82-3127da3e38ec-0&pdp_ext_f=%7B%22order%22%3A%226344%22%2C%22eval%22%3A%221%22%2C%22fromPage%22%3A%22search%22%7D&pdp_npi=6%40dis%21USD%213.04%210.99%21%21%213.04%210.99%21%402101062a17810066121352022e98c4%2112000049978631702%21sea%21US%210%21ABX%211%210%21n_tag%3A-29910%3Bd%3A5c316ac3%3Bm03_new_user%3A-29895%3BpisId%3A5000000207262906&curPageLogUid=VFN6cp8YSAkv&utparam-url=scene%3Asearch%7Cquery_from%3A%7Cx_object_id%3A1005004482028005%7C_p_origin_prod%3A)\
[water pump](https://www.aliexpress.us/item/3256809367623169.html?spm=a2g0o.productlist.main.1.7171flCLflCLFQ&algo_pvid=b8daa97c-eb63-43e9-b0b3-c885851a2e4c&algo_exp_id=b8daa97c-eb63-43e9-b0b3-c885851a2e4c-0&pdp_ext_f=%7B%22order%22%3A%22670%22%2C%22eval%22%3A%221%22%2C%22fromPage%22%3A%22search%22%7D&pdp_npi=6%40dis%21USD%211.26%210.99%21%21%218.51%216.69%21%40212a70c117810079816934664e84a7%2112000049447316452%21sea%21US%210%21ABX%211%210%21n_tag%3A-29910%3Bd%3A5c316ac3%3Bm03_new_user%3A-29895%3BpisId%3A5000000207262936&curPageLogUid=4J8hwvhzadAv&utparam-url=scene%3Asearch%7Cquery_from%3A%7Cx_object_id%3A1005009553937921%7C_p_origin_prod%3A#nav-specification)\
[soil sensor](https://www.aliexpress.com/ssr/300000512/BundleDeals2?spm=a2g0o.productlist.main.3.3b1926c5PjpczG&productIds=1005008145000162%3A12000043981255787&pha_manifest=ssr&_immersiveMode=true&disableNav=YES&sourceName=SEARCHProduct&utparam-url=scene%3Asearch%7Cquery_from%3A%7Cx_object_id%3A1005008145000162%7C_p_origin_prod%3A1005007353966390&pvid=b94039c6-a6d0-402a-8512-eb841e5fab72&_gl=1*1s27d8z*_gcl_aw*R0NMLjE3ODEwMDYwMDEuRUFJYUlRb2JDaE1Jd3MzYW9vejZsQU1WTE5ZV0JSM0YzaHdWRUFBWUFTQUFFZ0pHel9EX0J3RQ..*_gcl_au*MTY0NzY3NDMyNC4xNzgxMDA2MDAw*_ga*OTU1ODEwOTY2MTM4MDk0LjE3ODEwMDU5Nzk0NzQ.*_ga_VED1YSGNC7*czE3ODEwMDYwMDAkbzEkZzEkdDE3ODEwMDgxNjAkajU1JGwwJGgw)\
[mosfet](https://www.aliexpress.us/item/3256810584186433.html?spm=a2g0o.productlist.main.8.67fb6c91kI6mpz&algo_pvid=5a4f3c1a-3229-45ac-887b-dc489313ddd2&algo_exp_id=5a4f3c1a-3229-45ac-887b-dc489313ddd2-20&pdp_ext_f=%7B%22order%22%3A%2214%22%2C%22eval%22%3A%221%22%2C%22fromPage%22%3A%22search%22%7D&pdp_npi=6%40dis%21USD%213.01%210.99%21%21%2120.31%216.71%21%40212e520f17810085948531669ee753%2112000053455106144%21sea%21US%210%21ABX%211%210%21n_tag%3A-29910%3Bd%3A5c316ac3%3Bm03_new_user%3A-29895%3BpisId%3A5000000207262936&curPageLogUid=YmupETK5ZUQj&utparam-url=scene%3Asearch%7Cquery_from%3A%7Cx_object_id%3A1005010770501185%7C_p_origin_prod%3A)\
[flyback diode](https://www.aliexpress.us/item/3256811738197733.html?spm=a2g0o.productlist.main.4.71c55bda2SP2el&aem_p4p_detail=202606090551042378211846771000000003063&algo_pvid=d5ca4f7c-56ad-4d61-b177-008e54dc4cc7&algo_exp_id=d5ca4f7c-56ad-4d61-b177-008e54dc4cc7-3&pdp_ext_f=%7B%22order%22%3A%2232%22%2C%22eval%22%3A%221%22%2C%22fromPage%22%3A%22search%22%7D&pdp_npi=6%40dis%21USD%211.97%210.99%21%21%2113.28%216.69%21%402140c1e917810094637746315e1637%2112000057033157395%21sea%21US%210%21ABX%211%210%21n_tag%3A-29910%3Bd%3A5c316ac3%3Bm03_new_user%3A-29895%3BpisId%3A5000000208023469&curPageLogUid=OemqhgArUy3t&utparam-url=scene%3Asearch%7Cquery_from%3A%7Cx_object_id%3A1005011924512485%7C_p_origin_prod%3A&search_p4p_id=202606090551042378211846771000000003063_1)\
[lipo](https://www.aliexpress.us/item/3256805052966980.html?spm=a2g0o.productlist.main.13.24106915kLa9Rz&algo_pvid=9ab030b7-6c68-49e5-b052-152487eaed1d&algo_exp_id=9ab030b7-6c68-49e5-b052-152487eaed1d-12&pdp_ext_f=%7B%22order%22%3A%2217%22%2C%22eval%22%3A%221%22%2C%22fromPage%22%3A%22search%22%7D&pdp_npi=6%40dis%21USD%2113.79%210.99%21%21%2113.79%210.99%21%4021015b7d17810096105385958e4a40%2112000037114559271%21sea%21US%210%21ABX%211%210%21n_tag%3A-29910%3Bd%3A5c316ac3%3Bm03_new_user%3A-29895%3BpisId%3A5000000208023469&curPageLogUid=yFJHec5QbFGz&utparam-url=scene%3Asearch%7Cquery_from%3A%7Cx_object_id%3A1005005239281732%7C_p_origin_prod%3A)

next steps:
pcb design!

![image name](journal_imgs/notes.png)

**Total time spent: 1 hours**