## Installation
NOT READY YET.
```
pip install exponea-client
```

## Usage
```python
import Exponea from exponea_client
exponea = Exponea("project_token", username="basic_auth_username", password="basic_auth_password")
```
You can now fully utilize all four API, which are Analyses, Catalog, Customer and Tracking API described bellow.

## Tests
To run tests, run the following command
```python
python -m pytest
```

## Official documenation
For official Exponea documenation of Data API please see <https://developers.exponea.com/v2/reference>

## Table of Contents
* [Customer API](#customer-api)
    * [get_customer](#get_customer)
    * [get_customer_consents](#get_customer_consents)
    * [get_customer_attributes](#get_customer_attributes)
    * [get_customers](#get_customers)
    * [get_events](#get_events)
    * [anonymize_customer](#anonymize_customer)
* [Analyses API](#analyses-api)
    * [get_report](#get_report)
    * [get_funnel](#get_funnel)
    * [get_segmentation](#get_segmentation)
* [Catalog API](#catalog-api)
    * [create_catalog](#create_catalog)
    * [get_catalog_name](#get_catalog_name)
    * [get_catalog_items](#get_catalog_items)
    * [update_catalog_item](#update_catalog_item)
    * [update_catalog_name](#update_catalog_name)
    * [create_catalog_item](#create_catalog_item)
    * [delete_catalog_item](#delete_catalog_item)
    * [delete_catalog_items](#delete_catalog_items)
    * [delete_catalog](#delete_catalog)
* [Tracking API](#tracking-api)
    * [get_system_time](#get_system_time)
    * [update_customer_properties](#update_customer_properties)
    * [add_event](#add_event)
    * [batch_commands](#batch_commands)

## Catalog API

## create_catalog
```python
exponea.Catalog.create_catalog("catalog_name", ["field_one", "field_two"])
```
| Parameter     | Type          | Required |
| ------------- | ------------- | -------- |
| catalog_name  | String        | Yes      |
| fields        | Array<String> | Yes      |

It returns ID of the catalog as a String.
```python
d2b69e7s987b0asa0137455f2
```

## get_catalog_name
```python
exponea.Catalog.get_catalog_name("catalog_id")
```
| Parameter     | Type          | Required |
| ------------- | ------------- | -------- |
| catalog_id    | String        | Yes      |

It returns name of the catalog as a String.
```python
test_catalog
```

## get_catalog_items
```python
exponea.Catalog.get_catalog_items("catalog_id", params={})
```
| Parameter     | Type          | Required |
| ------------- | ------------- | -------- |
| catalog_id    | String        | Yes      |
| params        | Dictionary    | No       |
_Note: params is a kwargs argument._
It returns items of the catalog that match the query and filters specified in params Dictionary. See [official documentation](https://developers.exponea.com/v2/reference#get-catalog-items) for what kind of options you can give to params Dictionary.
```python
{
    "matched": 2,
    "limit": 20,
    "skip": 0,
    "data": [{"item_id": "1", "properties": {"field_one": "foo", "field_two": "baz"}}], 
    "matched_limited": False,
    "total": 2
}
```

## update_catalog_item
```python
exponea.Catalog.update_catalog_item("catalog_id", "1", {"field_one": "new_value"})
```
| Parameter     | Type          | Required |
| ------------- | ------------- | -------- |
| catalog_id    | String        | Yes      |
| item_id       | String        | Yes      |
| properties    | String        | Yes      |
It returns Boolean of whether the operation was successful.
```python
True
```

## update_catalog_name
```python
exponea.Catalog.update_catalog_name("catalog_id", "new_name", ["fiel_one", "field_two", "field_three"])
```
| Parameter     | Type          | Required |
| ------------- | ------------- | -------- |
| catalog_id    | String        | Yes      |
| new_name      | String        | Yes      |
| fields        | Array<String> | Yes      |
_Note: fields must contain those fields that already exist._
It returns Boolean of whether the operation was successful.
```python
True
```

## create_catalog_item
```python
exponea.Catalog.create_catalog_item("catalog_id", "item_id", { "field_one": "value_one" })
```
| Parameter     | Type          | Required |
| ------------- | ------------- | -------- |
| catalog_id    | String        | Yes      |
| item_id       | String        | Yes      |
| properties    | Dictionary    | Yes      |
_Note: This operation replaces an already existing item if the IDs match._
It returns Boolean of whether the operation was successful.
```python
True
```

## update_catalog_item
```python
exponea.Catalog.update_catalog_item("catalog_id", "item_id", { "field_one": "value_one" })
```
| Parameter     | Type          | Required |
| ------------- | ------------- | -------- |
| catalog_id    | String        | Yes      |
| item_id       | String        | Yes      |
| properties    | Dictionary    | Yes      |
_Note: Updates only those fields that are specified in properties Dictionary._
It returns Boolean of whether the operation was successful.
```python
True
```


## delete_catalog_item
```python
exponea.Catalog.delete_catalog_item("catalog_id", "item_id")
```
| Parameter     | Type          | Required |
| ------------- | ------------- | -------- |
| catalog_id    | String        | Yes      |
| item_id       | String        | Yes      |
It returns Boolean of whether the operation was successful.
```python
True
```

## delete_catalog_items
```python
exponea.Catalog.delete_catalog_items("catalog_id")
```
| Parameter     | Type          | Required |
| ------------- | ------------- | -------- |
| catalog_id    | String        | Yes      |
It returns Boolean of whether the operation was successful.
```python
True
```

## delete_catalog
```python
exponea.Catalog.delete_catalog("catalog_id")
```
| Parameter     | Type          | Required |
| ------------- | ------------- | -------- |
| catalog_id    | String        | Yes      |
It returns Boolean of whether the operation was successful.
```python
True
```

## Tracking API

### get_system_time
```python
exponea.Tracking.get_system_time()
```
| Parameter     | Type          | Required |
| ------------- | ------------- | -------- |
It returns a Float.
```python
1533663283.8943756
```

### update_customer_properties
```python
exponea.Tracking.update_customer_properties({ "registered": "test" }, { "first_name": "Lukas" })
```
| Parameter     | Type          | Required |
| ------------- | ------------- | -------- |
| customer_ids  | Dictionary    | Yes      |
| properties    | Dictionary    | Yes      |
_Note: The Customer's properties will get updated with the values of the properties Dictionary._
It returns Boolean describing whether operation was successful or not.
```python
True
```

### add_event
```python
exponea.Tracking.add_event({ "registered": "test" }, "event_type", properties={ "property": "sample_property" }, timestamp=1533663283)
```
| Parameter     | Type          | Required |
| ------------- | ------------- | -------- |
| customer_ids  | Dictionary    | Yes      |
| event_type    | String        | Yes      |
| properties    | Dictionary    | No       |
| timestamp     | Float         | No       |
_Note: properties and timestamp are kwargs._
It returns Boolean describing whether operation was successful or not.
```python
True
```

### batch_commands
```python
exponea.Tracking.batch_commands([
    {
        "name": "system/time"
    }, {
        "name": "customers",
        "data": {
            "customer_ids": {
                "registered": "test"
            },
            "properties": {
                "first_name": "Lukas",
                "last_name": "Cerny"
            }
        }
    }
])
```
| Parameter     | Type          | Required |
| ------------- | ------------- | -------- |
| commands      | Array<Dictionary> | Yes      |
See [official documentation](https://developers.exponea.com/v2/reference#section-how-to-build-a-command-body) for the available formats of different types of commands.
It returns Boolean describing whether operation was successful or not.
```python
True
```

## Customer API

### get_customer
```python
exponea.Customer.get_customer({ "registered": "test", "cookie": "123" })
```
| Parameter     | Type          | Required |
| ------------- | ------------- | -------- |
| customer_ids  | Dictionary    | Yes      |
_Note: The keys of the Dictionary are the names of the ID type, and value is the value for a given customer._
It returns following Dictionary.
```python
{
    "events": [{
        "type": "test",
        "timestamp": 1533495544.343536,
        "properties": {}
    }], 
    "properties": {
        "first_name": "Lukas",
        "last_nam": "Cerny"
    },
    "ids": {
        "registered": "test",
        "cookie": "123"
    }
}
```

### get_customer_consents
```python
exponea.Customer.get_customer_consents({"registered": "test"}, [ "newsletter", "other" ])
```
| Parameter     | Type          | Required |
| ------------- | ------------- | -------- |
| customer_ids  | Dictionary    | Yes      |
| consent_types | Array<String> | Yes      |
It returns following Dictionary.
```python
{
    "newsletter": True,
    "other": False
}
```

### get_customer_attributes
```python
exponea.Customer.get_customer_attributes({"registered": "test"}, ids=["cookie", "ga"], properties=["first_name"], aggregations=["agg_id"], segmentations=["segm_id"], predictions=["pred_id"], expressions=["expr_id"])
```
| Parameter     | Type          | Required |
| ------------- | ------------- | -------- |
| customer_ids  | Dictionary    | Yes      |
| ids           | Array<String> | No       |
| properties    | Array<String> | No       |
| aggregations  | Array<String> | No       |
| expressions   | Array<String> | No       |
| segmentations | Array<String> | No       |
| predictions   | Array<String> | No       |
| expressions   | Array<String> | No       |
_Note: The paramateres are kwargs and specify the attributes you want to recieve._
It returns following Dictionary.
```python
{
    "ids": {
        "cookie": [],
        "ga": "sample_id"
    },
    "properties": {
        "first_name": "Lukas"
    },
    "aggregations": {
        "agg_id": "sample_aggregate"
    },
    "segmentations": {
        "segm_id": "sample_segment"
    },
    "predictions": {
        "pred_id": "sample_prediction"
    },
    "expressions": {
        "expr_id": "sample_expression"
    }
}
```
_Note: If you do not specify one of the attribute types, it will not have a key in the resulting Dictionary._

### get_customers
```python
exponea.Customer.get_customers()
```
| Parameter     | Type          | Required |
| ------------- | ------------- | -------- |

It returns following Dictionary.
```python
[
    {
        "ids": {
            "cookie": [], 
            "registered": "test"
        },
        "properties": {
            "first_name": "Lukas",
            "last_name": "Cerny"
        }
    }
]
```

### get_events
```python
exponea.Customer.get_events({ "registered": "test" }, [ "event_type" ])
```
| Parameter     | Type          | Required |
| ------------- | ------------- | -------- |
| customer_ids  | Dictionary    | Yes      |
| event_types   | Array<String> | Yes      |
_Note: Event type is the name of an Event._
It returns following Dictionary.
```python
[
    {
        "properties":{
            "foo": "baz"
        },
        "timestamp":1533495529.9268496,
        "type": "event_type"
    }
]
```

### anonymize_customer
```python
exponea.Customer.anonymize_customer({ "registered": "test" })
```
| Parameter     | Type          | Required |
| ------------- | ------------- | -------- |
| customer_ids  | Dictionary    | Yes      |
It returns a Boolean if operation was successful or not.
```python
True
```

## Analyses API

### get_report
```python
exponea.Analyses.get_report("report_id")
```
| Parameter     | Type          | Required |
| ------------- | ------------- | -------- |
| report_id     | String        | Yes      |

It returns following Dictionary. The elements in `data` represent individual rows.
```python
{
    "name": "report_name",
    "data": [
        {
            "column_name_1": "value_1",
            "column_name_2": 1
        }
    ]
}
```

### get_funnel
```python
exponea.Analyses.get_funnel("funnel_id")
```
| Parameter     | Type          | Required |
| ------------- | ------------- | -------- |
| funnel_id     | String        | Yes      |
It returns following Dictionary. The elements in `data` represent individual drill downs.
```python
{
    "name": "funnel_name",
    "data": [
        {
            "serie": "serie_name",
            "step 1 step_one_name count": 2,
            "step 2 step_two_name count": 1,
            "step 2 event_name duration from previous": 435764.1615576744
        }
    ]
}
```

### get_segmentation
```python
exponea.Analyses.get_segmentation("segmentation_id")
```
| Parameter     | Type          | Required |
| ------------- | ------------- | -------- |
| segmentation_id | String        | Yes      |
It returns following Dictionary. The elements in `data` represent individual segments.
```python
{
    "name": "segmentation_name",
    "data": [
        {
            "segment": "segment_name_1",
            "#": 0
        }
    ]
}
```