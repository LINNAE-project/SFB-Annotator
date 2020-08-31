# start server
git clone https://github.com/cantaloupe-project/cantaloupe.git
cd cantaloupe
mvn clean compile exec:java -Dcantaloupe.config=cantaloupe.properties

# request image info
http://localhost:8182/iiif/2/MMNAT01_AF_NNM001001033_001/info.json

# request PNG version of the image
http://localhost:8182/iiif/2/MMNAT01_AF_NNM001001033_001/full/max/0/default.png

