---
title: Retrieve availability when retrieving abstract products
description: Learn how to retrieve availability when retrieving abstract products using Glue API.
last_updated: Aug 22, 2022
template: glue-api-storefront-guide-template
---

This document describes how to retrieve availability when retrieving abstract products. To retrieve full information about abstract products, see [Retrieve abstract products](/docs/pbc/all/product-information-management/{{site.version}}/manage-using-glue-api/abstract-products/glue-api-retrieve-abstract-products.html).

## Installation

For detailed information on the modules that provide the API functionality and related installation instructions, see:
* [Glue API: Products Feature Integration](/docs/pbc/all/product-information-management/{{site.version}}/install-and-upgrade/install-glue-api/install-the-product-glue-api.html)
* [Install the Inventory Management Glue API](/docs/pbc/all/warehouse-management-system/{{site.version}}/install-and-upgrade/install-features/install-the-inventory-management-glue-api.html)

## Retrieve an abstract product

To retrieve general information about an abstract product, send the request:

---
`GET` **/abstract-products/*{% raw %}{{{% endraw %}abstract_product_sku{% raw %}}}{% endraw %}***

---


| PATH PARAMETER | DESCRIPTION |
| --- | --- |
| ***{% raw %}{{{% endraw %}abstract_product_sku{% raw %}}}{% endraw %}*** | SKU of an abstract product to get information for. |

### Request

| STRING PARAMETER | DESCRIPTION | EXEMPLARY VALUES |
| --- | --- | --- |
| include | Adds resource relationships to the request. | abstract-product-availabilities |

`GET https://glue.mysprykershop.com/abstract-products/001?include=abstract-product-availabilities`: Retrieve information about the abstract product with SKU `001` with its availability.


### Response



<details>
<summary markdown='span'>Response sample: retrieve information about an abstract product with  the details about product availability</summary>

```json
{
    "data": {
        "type": "abstract-products",
        "id": "001",
        "attributes": {
            "sku": "001",
            "averageRating": null,
            "reviewCount": 0,
            "name": "Canon IXUS 160",
            "description": "Add a personal touch Make shots your own with quick and easy control over picture settings such as brightness and colour intensity. Preview the results while framing using Live View Control and enjoy sharing them with friends using the 6.8 cm (2.7”) LCD screen. Combine with a Canon Connect Station and you can easily share your photos and movies with the world on social media sites and online albums like irista, plus enjoy watching them with family and friends on an HD TV. Effortlessly enjoy great shots of friends thanks to Face Detection technology. It detects multiple faces in a single frame making sure they remain in focus and with optimum brightness. Face Detection also ensures natural skin tones even in unusual lighting conditions.",
            "attributes": {
                "megapixel": "20 MP",
                "flash_range_tele": "4.2-4.9 ft",
                "memory_slots": "1",
                "usb_version": "2",
                "brand": "Canon",
                "color": "Red"
            },
            "superAttributesDefinition": [
                "color"
            ],
            "superAttributes": {
                "color": [
                    "Red"
                ]
            },
            "attributeMap": {
                "product_concrete_ids": [
                    "001_25904006"
                ],
                "super_attributes": {
                    "color": [
                        "Red"
                    ]
                },
                "attribute_variants": []
            },
            "metaTitle": "Canon IXUS 160",
            "metaKeywords": "Canon,Entertainment Electronics",
            "metaDescription": "Add a personal touch Make shots your own with quick and easy control over picture settings such as brightness and colour intensity. Preview the results whi",
            "attributeNames": {
                "megapixel": "Megapixel",
                "flash_range_tele": "Flash range (tele)",
                "memory_slots": "Memory slots",
                "usb_version": "USB version",
                "brand": "Brand",
                "color": "Color"
            },
            "url": "/en/canon-ixus-160-1"
        },
        "links": {
            "self": "https://glue.mysprykershop.com/abstract-products/001?include=abstract-product-availabilities"
        },
        "relationships": {
            "abstract-product-availabilities": {
                "data": [
                    {
                        "type": "abstract-product-availabilities",
                        "id": "001"
                    }
                ]
            }
        }
    },
    "included": [
        {
            "type": "abstract-product-availabilities",
            "id": "001",
            "attributes": {
                "availability": true,
                "quantity": "10.0000000000"
            },
            "links": {
                "self": "https://glue.mysprykershop.com/abstract-products/001/abstract-product-availabilities"
            }
        }
    ]
}
```
</details>


<a name="abstract-products-response-attributes"></a>

{% include pbc/all/glue-api-guides/202204.0/retrieve-an-abstract-product-response-attributes.md %} <!-- To edit, see /_includes/pbc/all/glue-api-guides/202204.0/retrieve-an-abstract-product-response-attributes.md -->


For the attributes of abstract product availability, see [Retrieve availability of an abstract product](/docs/pbc/all/warehouse-management-system/{{site.version}}/manage-using-glue-api/retrieve-abstract-product-availability.html#abstract-product-availability-response-attributes)

## Possible errors

| CODE | REASON |
|-|-|
| 301 | Abstract product is not found. |
| 311 | Abstract product SKU is not specified. |