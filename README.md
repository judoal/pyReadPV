# pyReadPV
Python redo of PVMonitor project to read the output from an Outback Power Systems Photovoltaic system

The data source is an ascii stream from a server connected to an Outback Power Photovolotaic system. The raw data is a block of data sent once a seccond:

1,00,00,01,120,120,00,03,000,02,548,024,000,036 2,00,00,03,118,117,00,10,000,02,544,024,000,046 3,00,00,00,119,118,00,10,000,02,548,024,032,055 E,00,00,00,005,066,00,00,000,00,547,000,000,054 F,00,00,00,005,075,00,00,000,00,547,000,000,055 G,00,00,00,003,071,00,00,000,00,547,000,000,050 H,00,00,00,003,078,00,00,000,00,547,000,000,058

The 1st element in each line is the device ID. Numeric values are data from the inverter data and the alpha values are from the charge controller data.

Currently the data is only partially decoded. An example of one such block:

06172019131331 {'Op Mode': 'Sell Enabled', 'Sell Current': '03', 'Error Mode': 'OK', 'ACIn Volt': '124', 'Battery Volt': 52.4, 'Inverter Current': '07', 'Warn Mode': '128', 'Buy Current': '00', 'ID': '1', 'ACOut Volt': '123', 'Chgrger Current': '00', 'Misc': '024', 'AC Mode': '02'} {'Op Mode': 'Pass Thru', 'Sell Current': '00', 'Error Mode': 'OK', 'ACIn Volt': '120', 'Battery Volt': 52.0, 'Inverter Current': '00', 'Warn Mode': '000', 'Buy Current': '08', 'ID': '2', 'ACOut Volt': '119', 'Chgrger Current': '00', 'Misc': '152', 'AC Mode': '02'} {'Op Mode': 'Pass Thru', 'Sell Current': '00', 'Error Mode': 'OK', 'ACIn Volt': '120', 'Battery Volt': 52.4, 'Inverter Current': '00', 'Warn Mode': '000', 'Buy Current': '00', 'ID': '3', 'ACOut Volt': '120', 'Chgrger Current': '00', 'Misc': '024', 'AC Mode': '02'} {'Battery Volt': '523', 'charger Current': '05', 'Power (KWH)': '051', 'Aux Mode': '00', 'Error': '000', 'Charger Mode': '01', 'ID': 'E', 'PV Voltage': '064', 'PV Current': '04'} {'Battery Volt': '522', 'charger Current': '05', 'Power (KWH)': '046', 'Aux Mode': '00', 'Error': '000', 'Charger Mode': '01', 'ID': 'F', 'PV Voltage': '058', 'PV Current': '05'} {'Battery Volt': '522', 'charger Current': '06', 'Power (KWH)': '052', 'Aux Mode': '00', 'Error': '000', 'Charger Mode': '01', 'ID': 'G', 'PV Voltage': '081', 'PV Current': '04'} {'Battery Volt': '522', 'charger Current': '06', 'Power (KWH)': '059', 'Aux Mode': '00', 'Error': '000', 'Charger Mode': '02', 'ID': 'H', 'PV Voltage': '062', 'PV Current': '05'}

The 1st line is a time stamp (mmddyyhhmmss) that is created by the program when each block of data is read (neither the server nor the photovoltaic system provide a timestamp. Some of data such as "Op Mode" and "Error Mode" are decoded using the Outback Power documentation (found in the docs directory). Additional decoding of "... Mode" data for example still needs decoding.

Also under construction is a server simulator to send data directly from a raw data file over a socket for remote development and testing.

Python 2.7 is required since there is an incompatibility with python3

