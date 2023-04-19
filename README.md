# Kellinghusen Modality Selection

`SOHKellinghusenBox` is a modality selection model together with a harmonized OpenData collection for the train station at Kellinghusenstraße, Hamburg `Env[9.9668195,53.5647226 : 10.0162642,53.6139396]`. Agents arrive at the station at intervals and face the decision of which available modalities to choose. Available modalities are `Car`, `CarSharing`, `Bicycle`, `BicycleRental`, `Walking`. The decision between these different modalities is based on availability, fixed travel cost towards the destination, and a probabilistic preference of the agent.

You might use the dataset and/or the model for education, research, or transfer purposes. Please let us know about questions and usage.

Contact: Dr. Ulfia A. Lenfers ulfia.lenfers@haw-hamburg.de (www.mars-group.org)


## Starting

You can download an executable version of the model under [Releases](https://github.com/MARS-Group-HAW/model-soh-kellinghusen/releases).

##### Windows

For Windows users, start the box by calling the following command:
```shell script
SOHKellinghusenBox.exe
```
    
##### Unix, Mac, Linux

To start the box on unix-based systems, execute the following command:

```shell script
./SOHKellinghusenBox
```

---

> **Warning**
> Apple Users: There may be problems with the verification of the box and additional files with the extension ``*.dylib`` and ``*.dll``. Please execute the following command in order to make them accessible in your terminal:

```shell script
xattr -d com.apple.quarantine ./SOHKellinghusenBox
xattr -d com.apple.quarantine *.dylib
xattr -d com.apple.quarantine *.dll
```
---

Make sure that you have required permission to execute a program (e.g., execute `chmod +x SOHKellinghusenBox` on unix systems) and the default scenario described in the `config.json`, is available in the current directory where you start the box.

> Please note the current default output configuration is `trips`, creating trajectories for each `HumanTraveler` agent and stored within a `HumanTraveler_trips.geojson` file.

Alternatively, the output can be set to another destination (e.g.: for CSV output `output:csv` in the agent configuration `HumanTraveler` or database like PostgreSQL as described [here](https://www.mars-group.org/docs/tutorial/configuration/sim_output_formats)).

The system creates an output in the database or within a file (`HumanTraveler.csv` for CSV) in which states of each `HumanTraveler` is persited for each simulation step, when the agent has finished a sub-route of the composite multimodal route.


## Configure

The traveling schedule can be configured according to train station timetables in the supplied `config.json`. The config allows to change various settings such as time periods, the frequency of the output, or used scheduling tables such as:

````json
{
    "name": "HumanTravelerSchedulerLayer", 
    "file": "resources/human_traveler.csv"
}
````

This snippet assigns the used scheduling tabel towards a layer called `HumanTravelerSchedulerLayer`, controlling the spawn of events within the simulation (here spawning of agents). To increase the arrival of agents at the station, it is enough to increase the `spawningAmount` in the `human_traveler.csv` (e.g., `30` in the example below):

|startTime|endTime|spawningIntervalInMinutes|spawningAmount|hasBike|hasCar|prefersBike|prefersCar|usesBikeAndsdRide|usesOwnBikeOutside|usesOwnCar|source|destination|discriminator|
|---------|-------|-------------------------|--------------|-------|------|-----------|----------|-----------------|------------------|----------|------|-----------|-------------|
|16:00|16:30|1|30|0.45|0.05|0.5|0.1|0.55|0.35|0.05|"MULTIPOINT(...)"|"MULTIPOLYGON(...)"|1|


You can find more information about this [here](https://www.mars-group.org/docs/tutorial/configuration/sim_config_options).

## Analyze

The output results can be directly analyzed and visualized with a preferred GIS tool. Alternatively, we recommend https://kepler.gl/, a powerful open-source geospatial analysis tool.
