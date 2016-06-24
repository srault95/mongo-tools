Image Docker d'outils pour MongoDB
==================================

**Inclus:**

* `mtools`_ 
* `mongodb-tools`_     
* `mongotail`_
* `dex`_
* Commandes mongodb 3.2.7 (mongodump, mongoexport, ...)
* Python 2.7
* Client Mongo Python (pymongo)

**Exemples d'utilisation:**

::

    # requis: un serveur mongodb lancé dans un docker avec un name: "mongodb"

    $ docker run -it --rm --link mongodb:mongodb srault95/mongo-tools bash
    
    $ index-stats -H mongodb -d mydb 
    
    # Ou directement:
    
    $ docker run -it --rm --link mongodb:mongodb srault95/mongo-tools index-stats -H mongodb -d mydb
    

**mtools:**

:sources: https://github.com/rueckstiess/mtools

::

    # Extraction des logs de votre serveur mongodb
    mkdir data
    docker logs mongodb > data/mongod.log
    
    # Ouverture d'un shell bash 
    docker run -it --rm -v $PWD/data:/data srault95/mongo-tools bash

    # Analyse des logs
    mloginfo --queries /data/mongod.log
    mloginfo --restarts /data/mongod.log
    mloginfo --distinct /data/mongod.log
    mloginfo --connections /data/mongod.log

**mongodb-tools:**

:sources: https://github.com/jwilder/mongodb-tools

::

    # Ouverture d'un shell bash avec un lien vers votre serveur mongodb sous docker 
    $ docker run -it --rm ---link mongodb:mongodb srault95/mongo-tools bash

    $ index-stats -H mongodb -d mydb
    
    $ collection-stats -H mongodb -d mydb
    
    $ redundant-indexes -H mongodb -d mydb
    
**mongotail:**    

:sources: https://github.com/mrsarm/mongotail

::

    # Ouverture d'un shell bash avec un lien vers votre serveur mongodb sous docker 
    docker run -it --rm --link mongodb:mongodb srault95/mongo-tools bash
    
    # Active le profiling en level 1
    $ mongotail mongodb/widukind -l 1
    
    # Affiche les 100 derniers logs    
    $ mongotail mongodb/widukind -n 100
    2016-06-24 07:18:55.034 QUERY     [series] : {"filter": {"slug": "insee-ipch-2015-fr-coicop-001759971"}, "limit": 1, "find": "series", "singleBatch": true}
    2016-06-24 07:18:55.036 QUERY     [providers] : {"filter": {"enable": true, "name": "INSEE"}, "singleBatch": true, "limit": 1, "find": "providers", "projection": {"metadata": false}}
    2016-06-24 07:18:55.038 QUERY     [datasets] : {"filter": {"dataset_code": "IPCH-2015-FR-COICOP", "provider_name": "INSEE", "enable": true}, "singleBatch": true, "limit": 1, "find": "datasets", "projection": {"metadata": false}}
    
    # Affiche en temps réel les nouveaux logs
    $ mongotail mongodb/widukind -n 100 -f
        
**dex:**

:sources: https://github.com/mongolab/dex

*A terminer...* 

::
        
    dex -f mongod.log
    
    dex mongodb://mongodb/mydb -f mongod.log
    
    dex -p -n "*.series" mongodb://mongodb/mydb
     

.. _`mtools`: https://github.com/rueckstiess/mtools
.. _`mongodb-tools`: https://github.com/jwilder/mongodb-tools
.. _`mongotail`: https://github.com/mrsarm/mongotail
.. _`dex`: https://github.com/mongolab/dex