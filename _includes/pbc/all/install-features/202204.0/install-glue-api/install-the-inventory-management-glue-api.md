

This document describes how to install the Inventory Management feature API into a Spryker project.

## Prerequisites

To start feature integration, overview and install the necessary features:

| NAME | VERSION | INTEGRATION GUIDE |
| --- | --- | --- |
| Spryker Core| {{site.version}}| [Glue API: Spryker Core feature integration](/docs/scos/dev/feature-integration-guides/{{site.version}}/glue-api/glue-api-spryker-core-feature-integration.html)|
| Product | {{site.version}} | [Glue API: Products feature integration](/docs/scos/dev/feature-integration-guides/{{site.version}}/glue-api/glue-api-product-feature-integration.html) |
|Inventory Management| {{site.version}} | |


## 1) Install the required modules using Composer

Install the required modules:
```bash
composer require spryker/product-availabilities-rest-api:"^2.0.0" --update-with-dependencies
```

{% info_block warningBox "Verification" %}

Make sure that the following modules have been installed:

| MODULE | EXPECTED DIRECTORY |
| --- | --- |
| ProductAvailabilitiesRestApi| vendor/spryker/product-availabilities-rest-api|
| ProductsRestApi| vendor/spryker/products-rest-api |

{% endinfo_block %}

## 2) Set up transfer objects

Run the following command to generate transfer changes:

```bash
console transfer:generate
```

{% info_block warningBox "Verification" %}

Make sure that the following changes have been applied in transfer objects:

| TRANSFER | TYPE | EVENT | PATH |
| --- | --- | --- | --- |
| RestAbstractProductAvailabilityAttributesTransfer| class| created| src/Generated/Shared/Transfer/RestAbstractProductAvailabilityAttributesTransfer|
| RestConcreteProductAvailabilityAttributesTransfer| class| created| src/Generated/Shared/Transfer/RestConcreteProductAvailabilityAttributesTransfer|

{% endinfo_block %}

## 3) Enable resources and relationships

Activate the following plugins:  

| PLUGIN | SPECIFICATION | PREREQUISITES | NAMESPACE |
| --- | --- | --- | --- |
|AbstractProductAvailabilitiesRoutePlugin | Registers the abstract product availabilities resource. | None | Spryker\Glue\ProductAvailabilitiesRestApi\Plugin |
| ConcreteProductAvailabilitiesRoutePlugin | Registers the concrete product availabilities resource. | None | Spryker\Glue\ProductAvailabilitiesRestApi\Plugin |
| AbstractProductAvailabilitiesByResourceIdResourceRelationshipPlugin | Adds the abstract product availability resource as a relationship to the abstract product resource. | None | Spryker\Glue\ProductAvailabilitiesRestApi\Plugin\GlueApplication |
| ConcreteProductAvailabilitiesByResourceIdResourceRelationshipPlugin | Adds the concrete product availability resource as a relationship to the concrete product resource. | None |Spryker\Glue\ProductAvailabilitiesRestApi\Plugin\GlueApplication |


<details open>
<summary markdown='span'>src/Pyz/Glue/GlueApplication/GlueApplicationDependencyProvider.php</summary>

```php
<?php

namespace Pyz\Glue\GlueApplication;

use Spryker\Glue\GlueApplication\GlueApplicationDependencyProvider as SprykerGlueApplicationDependencyProvider;
use Spryker\Glue\GlueApplicationExtension\Dependency\Plugin\ResourceRelationshipCollectionInterface;
use Spryker\Glue\ProductAvailabilitiesRestApi\Plugin\AbstractProductAvailabilitiesRoutePlugin;
use Spryker\Glue\ProductAvailabilitiesRestApi\Plugin\ConcreteProductAvailabilitiesRoutePlugin;
use Spryker\Glue\ProductAvailabilitiesRestApi\Plugin\GlueApplication\AbstractProductAvailabilitiesByResourceIdResourceRelationshipPlugin;
use Spryker\Glue\ProductAvailabilitiesRestApi\Plugin\GlueApplication\ConcreteProductAvailabilitiesByResourceIdResourceRelationshipPlugin;
use Spryker\Glue\ProductsRestApi\ProductsRestApiConfig;

class GlueApplicationDependencyProvider extends SprykerGlueApplicationDependencyProvider
{
    /**
     * @return \Spryker\Glue\GlueApplicationExtension\Dependency\Plugin\ResourceRoutePluginInterface[]
     */
    protected function getResourceRoutePlugins(): array
    {
        return [
            new AbstractProductAvailabilitiesRoutePlugin(),
            new ConcreteProductAvailabilitiesRoutePlugin(),
        ];
    }

    /**
     * @param \Spryker\Glue\GlueApplicationExtension\Dependency\Plugin\ResourceRelationshipCollectionInterface $resourceRelationshipCollection
     *
     * @return \Spryker\Glue\GlueApplicationExtension\Dependency\Plugin\ResourceRelationshipCollectionInterface
     */
    protected function getResourceRelationshipPlugins(
        ResourceRelationshipCollectionInterface $resourceRelationshipCollection
    ): ResourceRelationshipCollectionInterface {
        $resourceRelationshipCollection->addRelationship(
            ProductsRestApiConfig::RESOURCE_ABSTRACT_PRODUCTS,
            new AbstractProductAvailabilitiesByResourceIdResourceRelationshipPlugin()
        );
        $resourceRelationshipCollection->addRelationship(
            ProductsRestApiConfig::RESOURCE_CONCRETE_PRODUCTS,
            new ConcreteProductAvailabilitiesByResourceIdResourceRelationshipPlugin()
        );

        return $resourceRelationshipCollection;
    }
}
```
</details>

{% info_block warningBox "Verification" %}

Make sure that the following endpoints are available:

*   `http://mysprykershop.com/abstract-products/{% raw %}{{{% endraw %}abstract_sku{% raw %}}}{% endraw %}/abstract-product-availabilities`
*   `http://mysprykershop.com/concrete-products/{% raw %}{{{% endraw %}concrete_sku{% raw %}}}{% endraw %}/concrete-product-availabilities`

Send the `GET http://mysprykershop.com/abstract-products/{% raw %}{{{% endraw %}abstract_sku{% raw %}}}{% endraw %}?include=abstract-product-availabilities` and make sure that the response includes relationships to the `abstract-product-availabilities` resource.

Send the `GET http://mysprykershop.com/concrete-products/{% raw %}{{{% endraw %}concrete_sku{% raw %}}}{% endraw %}?include=concrete-product-availabilities` and make sure that the response includes relationships to the `concrete-product-availabilities` resource.

{% endinfo_block %}  