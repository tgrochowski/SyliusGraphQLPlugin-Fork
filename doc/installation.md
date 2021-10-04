
1. Require plugin with composer:

    ```bash
    composer require bitbag/graphql-plugin
    ```

1. Add plugin dependencies to your `config/bundles.php` file:

    ```php
        return [
         ...
        
            BitBag\SyliusGraphqlPlugin\BitBagSyliusGraphqlPlugin::class => ['all' => true],
        ];
    ```

1. Import required config by adding  `config/packages/bitbag_sylius_graphql_plugin.yaml` file:

    ```yaml
    # config/packages/bitbag_sylius_graphql_plugin.yaml
    
    parameters:
        bitbag_graphql.model.refresh_token.class: 'Gesdinet\JWTRefreshTokenBundle\Entity\RefreshToken'

    
    imports:
        - { resource: "@BitBagSyliusGraphqlPlugin/Resources/config/config.yml" }
    ```    

4. In _sylius.yaml add mappings for promotion and product attribute so graphql can see them properly

    ```yml
    sylius_attribute:
        driver: doctrine/orm
        resources:
            product:
                subject: Sylius\Component\Core\Model\Product
                attribute_value:
                    classes:
                        model: BitBag\SyliusGraphqlPlugin\Model\ProductAttributeValue
    
    sylius_promotion:
        resources:
            promotion_coupon:
                classes:
                    model: Sylius\Component\Promotion\Model\PromotionCoupon
            promotion:
                classes:
                    model: Sylius\Component\Core\Model\Promotion    
    ```

5. Import routing in routes.yaml

    ```yml
    bitbag_sylius_graphql_plugin:
        resource: "@BitBagSyliusGraphqlPlugin/Resources/config/routing.yml"
   ```