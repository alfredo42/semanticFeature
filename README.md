# Semantic Feature Mapping - Learning from Test Cases of Other Apps

This repository stores artifacts used for the evaluation of semantic feature mapping.

## Information

To avoid potential privacy/security leaks, we tried to anonymize the provided data as good as possible. After the review process is complete, you can also can get access to the **network profile data** and the **screenshots** (used for debugging purpose). The meta-data used in presented in the archive describes in our own words, what the overall functionality of the state was, but was not used for calculating matchings.

We spend our best effort to replace revealing descriptions in the data using the string `BLINDED`, without rendering the data useless by destroying the structure. You still might find *revealing* data if you spend serious effort.

## Legal Information

The provided data should be used for scientific research purposes only. No copyright infringement to the original owner is intended, nor should this be used to harm the original owner in any way.

## Short Documentation

### Repository Structure

#### Subjects

The `subjects folder` contains the DOM data extracted while running the original test suite. The data is structured for every domain, i.e. `Knowledge Bases`, `Search Engines (& Mail)`, and `eCommerce`.

In every tar-ball you will find the file `order.txt` which contains the order the states have shown up in the client identified by a UUID. Each `state-$UUID.json-file` is a JSON serialized version of our DOM data. The meta-data information contains information for human understanding only.

The `features` folder contains the manually identified features. Again the UUID in the file name expresses in which state these features occur.

#### Results

The `results` folder contains the detailed evaluation data going even beyond what could be expressed and discussed in the paper. For each application pair this data contains the calculated matching (without averaging the results). The `matching success` (RQ1) is evaluated per domain and overall in the subfolders `Knowledge Bases`, `Search Engines (& Mail)`, `eCommerce`, and `TOTAL`.

The files `prediction_total_eCommerce.csv`, `prediction_total_knowledge.csv`, `prediction_total_search.csv`, and `resultsprediction_total.csv` contain the analysis for RQ2.

### Data Structure (DOM data and states)

Stored in the `subjects` folder are the [DOM](https://de.wikipedia.org/wiki/Document_Object_Model) states of the application as shown in the browser interface. The DOM is a recursive tree structure and the JSON file captures this. I will not go into detail about what data this DOM contains, but refer to the available documentation.

## Reproducing the results

In order to reproduce the experimental setup with the data at hand you need to check the features folder, which contains a description of the features for each individual state. For the prediction the manually identified `label` has to be identical in the predicted `XPATH`.

In the state data the XPATH is build hierarchically, where the children of a DOM element are contained in the path `children`. Each element also contains attributes for

* relativeXPath: The position used for verifying the matching and used by the SELENIUM test case to interact with the application under test
* Position: `relX` (upper left corner), `relY`, `height`, and `width` used for grouping together labels and interactive element used by the test using visual alignment
* text: displayed text attributes (part of the analyzed NLP content)
* attributeMap: Based on the element type it can contain default texts, placeholder and the like.
* eventhandlers: self-explanatory. It contains the eventhandlers registered to this element.
