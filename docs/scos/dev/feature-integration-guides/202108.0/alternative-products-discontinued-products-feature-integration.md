---
title: Alternative products + discontinued products feature integration
description: This guide describes all the steps needed to be performed in order to integrate the Alternative Products + Discontinued Products features into your project.
last_updated: Jun 16, 2021
template: feature-integration-guide-template
originalLink: https://documentation.spryker.com/2021080/docs/alternative-products-discontinued-products-feature-integration
originalArticleId: eb447174-6a43-4adb-8914-747a9771c4a9
redirect_from:
  - /2021080/docs/alternative-products-discontinued-products-feature-integration
  - /2021080/docs/en/alternative-products-discontinued-products-feature-integration
  - /docs/alternative-products-discontinued-products-feature-integration
  - /docs/en/alternative-products-discontinued-products-feature-integration
---

## Install feature core

### Prerequisites

Please review and install the necessary features before beginning the integration.

| NAME | VERSION |
| --- | --- |
| Alternative Products | {{page.version}} |
| Discontinued Products | {{page.version}} |

### 1) Set up behavior

Register the following plugins:

| PLUGIN | SPECIFICATION | PREREQUISITES | NAMESPACE |
| --- | --- | --- | --- |
| DiscontinuedCheckAlternativeProductApplicablePlugin | Checks if product alternatives should be shown for the product. | Expects `SKU `and `idProductConcrete` to be set for `ProductViewTransfer`. | Spryker\Client\ProductDiscontinuedStorage\Plugin\ProductAlternativeStorage |
| DiscontinuedCheckAlternativeProductApplicablePlugin | Checks if product alternatives should be shown for the product. | None | Spryker\Zed\ProductDiscontinued\Communication\Plugin\ProductAlternative |

**src/Pyz/Client/ProductAlternativeStorage/ProductAlternativeStorageDependencyProvider.php**

```php
<?php

namespace Pyz\Client\ProductAlternativeStorage;

use Spryker\Client\ProductAlternativeStorage\ProductAlternativeStorageDependencyProvider as SprykerProductAlternativeStorageDependencyProvider;
use Spryker\Client\ProductDiscontinuedStorage\Plugin\ProductAlternativeStorage\DiscontinuedCheckAlternativeProductApplicablePlugin;

class ProductAlternativeStorageDependencyProvider extends SprykerProductAlternativeStorageDependencyProvider
{
    /**
     * @return \Spryker\Client\ProductAlternativeStorageExtension\Dependency\Plugin\AlternativeProductApplicablePluginInterface[]
     */
    protected function getAlternativeProductApplicableCheckPlugins(): array
    {
        return [
            new DiscontinuedCheckAlternativeProductApplicablePlugin(),
        ];
    }
}
```

**src/Pyz/Zed/ProductAlternative/ProductAlternativeDependencyProvider.php**

```php
<?php

namespace Pyz\Zed\ProductAlternative;

use Spryker\Zed\ProductAlternative\ProductAlternativeDependencyProvider as SprykerProductAlternativeDependencyProvider;
use Spryker\Zed\ProductDiscontinued\Communication\Plugin\ProductAlternative\DiscontinuedCheckAlternativeProductApplicablePlugin;

class ProductAlternativeDependencyProvider extends SprykerProductAlternativeDependencyProvider
{
    /**
     * @return \Spryker\Zed\ProductAlternativeExtension\Dependency\Plugin\AlternativeProductApplicablePluginInterface[]
     */
    protected function getAlternativeProductApplicablePlugins(): array
    {
        return [
            new DiscontinuedCheckAlternativeProductApplicablePlugin(), #ProductDiscontinuedFeature
        ];
    }
}
```

{% info_block warningBox "Verification" %}
Make sure that you can see alternatives for products that are marked as **discontinued** on the product details page.
{% endinfo_block %}


{% info_block infoBox "Store relation" %}

If the [Product Labels feature](/docs/scos/user/features/{{page.version}}/product-labels-feature-overview.html) is integrated into your project, make sure to define store relations for *Discontinued* and *Alternatives available* product labels by re-importing [product_label_store.csv](/docs/scos/dev/data-import/{{page.version}}/data-import-categories/merchandising-setup/product-merchandising/file-details-product-label-store.csv.html). Otherwise, the product labels are not displayed on the Storefront.

{% endinfo_block %}
