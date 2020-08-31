### Start Cantaloupe server

```
git clone https://github.com/cantaloupe-project/cantaloupe.git
cd cantaloupe
mvn clean compile exec:java -Dcantaloupe.config=cantaloupe.properties
```

### Summary of server requests

| Repository | Image info | Source image | Processed image |
|------------|------------|--------------|-----------------|
| [GitHub](https://github.com/LINNAE-project/SFB-Annotator/tree/master/data/jpg) | [link](http://localhost:8182/iiif/2/MMNAT01_AF_NNM001001033_001/info.json) | [JPG](https://raw.githubusercontent.com/LINNAE-project/SFB-Annotator/master/data/jpg/MMNAT01_AF_NNM001001033_001.jpg) | [PNG](http://localhost:8182/iiif/2/MMNAT01_AF_NNM001001033_001/full/max/0/default.png) |
| [DataverseNL](https://demo.dataverse.nl/dataset.xhtml?persistentId=doi:10.80227/test-JEQKJH) | [link](http://localhost:8182/iiif/2/1184/info.json) | [TIF](https://demo.dataverse.nl/api/access/datafile/1184) | [JPG](http://localhost:8182/iiif/2/1184/full/max/0/default.jpg) |
| [SURF Data Repository](https://trng-repository.surfsara.nl/deposit/900c341c1c10fff7) | [link](http://localhost:8182/iiif/2/900c341c1c10fff7%2Ffiles%2FMMNAT01_PM_NNM001001033_001/info.json) | [TIF](https://trng-repository.surfsara.nl/deposit/900c341c1c10fff7/files/MMNAT01_PM_NNM001001033_001.tif) | [JPG](http://localhost:8182/iiif/2/900c341c1c10fff7%2Ffiles%2FMMNAT01_PM_NNM001001033_001/full/max/0/default.jpg) |
