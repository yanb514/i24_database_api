# i24-transform-module

I24's Transform module for downstream traffic visualization and analysis (post-post processing). 

The module is collection-agnostic, meaning it can transform both RAW and RECONCILED collections without explicit configuration. 

![transform_raw](https://user-images.githubusercontent.com/58854510/179090837-b10606c4-001d-4d8b-aaad-92dafc97dbff.png)
![transform_reconciled](https://user-images.githubusercontent.com/58854510/179090843-53eb1360-28b1-4b5d-afc4-13d31de09c7e.png)


## High level overview

The Transform module:

1. Subscribes to a post-processed collection via mongoDB's change stream (change_stream_reader.py)
2. Transforms trajectories into a timestamp-based document (transformation.py)
3. Writes and updates the documents into a transformed mongoDB collection (batch_update.py)
4. Parallelizes step 1-3 with multiprocessing (main.py)

## Initialize config

1. Clone the repository
2. Create a `config.json` file using `config.template.json`.
3. Enter the credentials for connecting to MongoDB and the collection info

    > `read_database_name` & `read_collection_name`: The name of the collection and its database to transform (must already exist in db)

    > `write_database_name` & `write_collection_name`: The name of the transformed collection and its database (to be generated by main.py)

    ```
    {
    	"host": "x.x.x.x",
    	"port": 27017,
    	"username": "username",
    	"password": "password",
    	"read_database_name": "db_name",
    	"read_collection_name": "collection_name"
    	"write_database_name": "database_name"
    	"write_collection_name": "collection_name"
    }
    ```

## How to transform an existing (static) collection using `static_collection_transformer.py`

1. Initialize config
2. Run `run_static_transformer.py`

## How to transform a dynamic collection using `run_dynamic_transformer.py`

1. Initialize config
2. Run `run_dynamic_transformer.py`
