Freestyle Libre 2
**********************

The Freestyle Libre 2 system can automatically report dangerous blood glucose levels. The Libre2 Sensor sends the current blood sugar values to a receiver (reader or smartphone) every minute. The receiver triggers an alarm if necessary. With a self-modified LibreLink App, you can continuously receive your blood sugar values on your smartphone. Καθώς τα στέλνουν απευθείας μέσω του bluetooth στο τηλέφωνό σας, δεν θα χρειαστεί να αγοράσετε έναν προσαρμογέα bluetooth όπως το MiaoMiao. 

Βήμα 1: Φτιάξτε το δικό σας patched Librelink-App
==============

For legal reasons, the so-called patching has to be done by yourself according to one of two instructions:

https://github.com/user987654321resu/Libre2-patched-App

https://github.com/TinoKossmann/LibreLink-xDrip-Patch

The patched app has to be installed instead of the original app. The next sensor started with it will wireless transmit its values to the smartphone.

Important: First install and uninstall the original app on an NFC capable smartphone. NFC has to be enabled. This costs no extra power. Then install the patched app. This can de checked by the foreground authorization notification. 

.. image:: ../images/fsl2pic1.jpg
  :alt: LibreLink Foreground Service

It significantly improves the connection stability compared to the original app. Now set the permissions memory and location, enable automatic time and timezone and set the alarms in the LibreLink app. Now start the Libre2 sensor with the patched app by simply scanning the sensor. Follow the instructions. The sensor remembers the device it was started with. Only this device can receive alarms in the future.

.. image:: ../images/fsl2pic2.jpg
  :alt: LibreLink permissions memory & location
  
.. image:: ../images/fsl2pic3.jpg
  :alt: Android settings location
  
.. image:: ../images/fsl2pic4.jpg
  :alt: LibreLink settings alarm
  
You can use a second NFC capable smartphone with the original LibreLink app for scanning via NFC. The Reader can NOT be used any more, it cannot be connected in parallel! The second phone can upload the blood sugar values into the Abbott Cloud (LibreView). LibreView can generate reports for the DiaDoc. There are many parents who absolutely need this. The patched app does not have any connection to the Internet.

The first connection setup to the sensor is critical. The LibreLink app tries to establish a wireless connection to the sensor every 30 seconds. All settings must be correct: 

* NFC enabled
* memory permission enabled 
* location enabled
* automatic time and timezone 
* at least one alarm setting in the LibreLink app. 

As long as you see a red exclamation mark ("!") on the upper left corner of the LibreLinks start screen there is no connection. Only when the exclamation mark is gone, the connection is established and blood sugar values are sent to the smartphone. This should happen after a maximum of 5 minutes.

.. image:: ../images/fsl2pic5.jpg
  :alt: LibreLink no connection
  
If the exclamation mark remain, this can have several reasons:

- the Android location service is not granted - please enable it in the system settings
- automatic time and time zone is not set - please change the settings accordingly
- activate alarms - at least one of the three alarms must be activated in LibreLink
- Bluetooth is switched off - please switch on

Restarting the phone can help, you may have to do it several times. As soon as the connection is established, the red exclamation mark disappears and the most important step is taken. Sensor and phone are now connected, every minute a blood sugar value is transmitted.

.. image:: ../images/fsl2pic6.jpg
  :alt: LibreLink connection established
  
Now the smartphone settings can be changed again if necessary, e.g. if you want to save power. Location service can be switched off, volume can be set to zero or alarms can be switched off again. The values are transferred anyway.

When starting the next sensor, however, all settings must be set again!

Βήμα 2: Εγκατάσταση και ρύθμιση παραμέτρων xDrip+ app
==============

The blood sugar values are received on the smartphone by the xDrip+ App. 

* Εάν δεν έχετε ήδη εγκαταστήσει, κάντε λήψη της εφαρμογής xdrip και εγκαταστήστε ένα από τα τελευταία nightly builts από εδώ <https://github.com/NightscoutFoundation/xDrip/releases>.
* In xDrip+ select "Libre2 (patched App)" as data source. If necessary, enter "BgReading:d,xdrip libre_receiver:v" under Less Common Settings->Extra Logging Settings->Extra tags for logging. This will log additional error messages fo trouble shooting.
* Στο xdrip, μεταβείτε στις Ρυθμίσεις> Συμβατότητα Interapp> Δυνατότητα τοπικής μετάδοσης δεδομένων και επιλέξτε ΕΝΕΡΓΟΠΟΊΗΣΗ.
* Στο xdrip πηγαίνετε στο Ρυθμίσεις> Συμβατότητα Interapp> Αποδοχή θεραπειών και επιλέξτε OFF.
* Εάν θέλετε να μπορείτε να χρησιμοποιήσετε το AndroidAPS για τη βαθμονόμηση, στη συνέχεια στο xdrip μεταβείτε στις Ρυθμίσεις> Συμβατότητα Interapp> Αποδοχή βαθμονομίσεων και επιλέξτε ΕΝΕΡΓΟΠΟΊΗΣΗ.  Ενδέχεται επίσης να θέλετε να ελέγξετε τις επιλογές στις Ρυθμίσεις> Λιγότερες κοινές ρυθμίσεις> Ρυθμίσεις βελτιωμένης βαθμονόμησης.

.. image:: ../images/fsl2pic7.jpg
  :alt: xDrip+ LibreLink logging
  
.. image:: ../images/fsl2pic7a.jpg
  :alt: xDrip+ log
  #
Step 3: Start sensor
===============

In xDrip+ start the sensor with "Start Sensor" and "not today". 

In fact this will not start any Libre2 sensor or interact with them in any case. This is simply to indicate xDrip+ that a new sensor is delivering blood sugar values. If available, enter two bloody measured values for the initial calibration. Now the blood glucose values should be displayed in xDrip+ every 5 minutes. Skipped values, e.g. because you were too far away from your phone, will not be backfilled.

Step 4: Configure AndroidAPS
==============
* Στο AndroidAPS πηγαίνετε στο Config Builder > BG Πηγή και έλεγχος " xDrip+' 
Αν το AndroidAPS δεν λαμβάνει τιμές BG όταν το τηλέφωνο βρίσκεται σε κατάσταση λειτουργίας αεροπλάνου, χρησιμοποιήστε Προσδιορισμός δέκτη όπως περιγράφεται στη[ σελίδα ρυθμίσεων xDrip](../Configuration/xdrip.html).

Μέχρι τώρα, χρησιμοποιώντας το Libre 2 ως πηγή BG, δεν μπορείτε να ενεργοποιήσετε το "πάντα ενεργοποιημένο SMB" και το "ενεργοποιημένο SMB μετά τους υδατάνθρακες" μέσα στον αλγόριθμο SMB. Οι τιμές BG του Libre 2 δεν είναι αρκετά ομαλές ώστε να το χρησιμοποιείτε με ασφάλεια. Δείτε " Εξομάλυνση δεδομένων της γλυκόζης του αίματος <../Χρήση/Smoothing-Blood-Glucose-Data-in-xDrip.md>`_ για περισσότερες λεπτομέρειες.

Experiences and Troubleshooting
===================

The connectivity is extraordinary good. With the exception of Huawei mobile phones, all current smartphones seems to work well. The reconnect in case of connection loss is phenomenal. The connection can break off if the mobile phone is in the pocket opposite the sensor or if you are outdoors. When I am gardening, I use to wear my phone on the sensor side of my body. In rooms, where Bluettooth spreads over refections, no problems should occur. If you have connectivity problems please test another phone.

Technically, the current blood sugar value is transmitted to xDrip+ every minute. A weighted average filter calculates a smoothed value over the last 25 minutes. This is mandatory for looping. The curves look smooth and the loop results are great. The raw values on which the alarms are based jitter a little more, but correspond to the values that the reader also displays. In addition, the raw values can be displayed in the xDrip+ graph in order to be able to react in time to rapid changes. Please switch on Less Common Settings->Advanced Settings for Libre2->show Raw values. Then the raw values are additionally displayed as small white dots.

.. image:: ../images/fsl2pic8.jpg
  :alt: xDrip+ advanced settings Libre 2
  
.. image:: ../images/fsl2pic9.jpg
  :alt: xDrip+ homescreen with raw data
  
The sensor runtime is fixed to 14 days. The 12 extra hours of Libre1 no longer exist. xDrip+ shows additional sensor information after enabling Avanced settings for Libre2->show Sensor Infos in the System page like the starting time. No infomration about the remaining lifetime of the L2 sensor is displayed. The remaining time can only be seen in the patched LibreLink app. Either in the main screen as remaining days display or as start time in the three-point menu->Help->Event log under "New sensor found".

.. image:: ../images/fsl2pic10.jpg
  :alt: Libre 2 start time
  
Altogether it is one of the smallest CGM systems on the market. Small, no transmitter necessary and mostly very accurate values without fluctuations. After approx. 12 hours running-in phase with deviations of up to 30 mg/dL the deviations are typical smaller than 10 md/dL. Best results at the rear orbital arm, other setting points with caution! No need to set a new sensor one day ahead for soacking. That would disturbe the internal leveling mechanism.

There seem to be bad sensors from time to time, which are far away from the blood values. It stays that way. These should be immediately replaced.

Moved sensors can result in bad results. The filament which sits in the tissue is a little bit moved and will measure different results. Mostly you will see jumping values in xDrip+. Or the difference to the bloody values change. Please replace the sensor immediately! The results are inaccurate now.

A sensor exchange takes place on-the-fly: Set new sensor shortly before activation. As soon as xDrip+ receives no more data from the old sensor, start the new sensor with the patched app. After one hour new values should appear automatically in xDrip+. If not, please check the phone settings and proceed as with the first start. In xDrip+ please select "Sensor Stop" and "Delete calibration only" to help xDrip adjust the calibration. No need to start the Sensor in xDrip+ later on.

.. image:: ../images/fsl2pic11.jpg
  :alt: xDrip+ missing data when changing Libre 2 sensor
  
You can calibrate the Libre2 with an offset of plus/minus 20 mg/dL (intercept), but no slope. To be on the safe side, calibrate every 24 - 48 hours. The values are accurate up to the end of the sensor and do not jitter as with the Libre1. However, if the sensor is completely off, this will not change. The sensor should then be replaced immediately.

The Libre2 sensors contain plausibility checks to detect bad sensor values. As soon as the sensor moves on the arm or is lifted slightly, the values may start to fluctuate. The Libre2 sensor will then shut down for safety reasons. Unfortunately, when scanning with the App, additional checks are made. The app can deactivate the sensor even though the sensor is OK. Currently the internal test are too strict. I have completely stopped scanning and haven't had a failure since then.

In other `time zones <../Usage/Timezone-traveling.html>`_ there are two strategies for looping: Either 

1. leave the smartphone time unchanged and shift the basal profile (smartphone in flight mode) or 
2. delete the pump history and change the smartphone time to local time. 

Method 1. is great as long as you don't have to set a new Libre2 sensor on-site. If in doubt, choose method 2., especially if the trip takes longer. If you set a new sensor, the automatic time zone must be set, so method 1. would be disturbed. Please check before, if you are somewhere else, you can run otherwise fast into problems.

Besides the patched app the new Droplet transmitter or (soon available) the new OOP algorithm of xDrip+ can be used to receive blood sugar values. MM2 and blucon do NOT work so far.
