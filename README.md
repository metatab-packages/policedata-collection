#  Police Data Collection

This data collection collects datasets related to the operation of police departments, primarily those published the [Police Data Initiative](https://www.policedatainitiative.org/) website, and processes the datasets to make them easier to analyze. 

The datafiles related for this collection can be found on the [San Diego Regional Data Library data repository](https://data.sandiegodata.org/dataset/category/police_data_collection/)

## Related Projects: 

* [Police Data Accessibility Project](https://www.reddit.com/r/DataPolice/)
* [Police Data Initiative](https://www.policedatainitiative.org/)
* [Open Oversight](https://lucyparsonslabs.com/projects/openoversight/)
* [Fatal Encounters](https://fatalencounters.org/)
* [Mapping Police Violence](https://mappingpoliceviolence.org/)

## Managing the Collection

### Adding an Existing Data Package

Collections are composed of this top level directory and source packages that
are included a git submodules. So, to add a few packages:

  
    git submodule add https://github.com/metatab-packages/sandiegocounty.gov-covid19.git
    git submodule add https://github.com/metatab-packages/census.gov-boundaries-2018.git
    
Then, when checking out the collection, be sure to update all of the submodules too: 

    git clone --recurse-submodules <collection_url>
    
### Adding new data packages. 
    
To add a new package, cd to the staging directory, create the package, then check it in to github. Then use the instructions above to add it to the main directory as a submodule. 

    cd staging
    mp new -o exmaple.com -d datapackage
    cd exmaple.com-datapackage
    < Edit metadata; At least set description and title>
    mp github init
    cd ../
    git submodule add https://github.com/metatab-packages/exmaple.com-datapackage.git
    
The `mp github init` call will set up a new repo on Github for the package. It requires getting an pplication token from Github and adding it to the metatab configuration file. See ``mp github init``
    
    
### Building  packages. 

The top lvel directory defines `invoke` tasks. To use invoke you will need to `pip install invoke`. Then run `invoke -l` to like the available tasks. THe most important are: 

* `invoke build`: Run `mp build` in each package
* `invoke make`: Run `mp make` in each package, which will build the package, upload it to s3 and publish it to Wordpress, with the proper configuration. 
