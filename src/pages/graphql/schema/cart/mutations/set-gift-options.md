---
title: setGiftOptionsOnCart mutation
edition: ee
---

# setGiftOptionsOnCart mutation

The `setGiftOptionsOnCart` mutation allows the buyer to set the following gift options on the cart level:

*  Gift messages
*  Gift wrapping
*  A gift receipt to accompany the order
*  A printed card to accompany the order

<InlineAlert variant="info" slots="text" />

Gift messages are a feature of Magento Open Source. All other gift options require Adobe Commerce.

To remove a gift message, set the `gift_message` object to null. To remove gift wrapping, set the `gift_wrapping_id` attribute to null.

Use the [updateCartItems mutation](update-items.md) to set gift messages and gift wrapping on individual items.

These options are configured on the **Stores** > Configuration > **Sales** > **Sales** > **Gift Options** screen. To determine whether these options are enabled, specify these attributes in the [`storeConfig` query](../../store/queries/store-config.md).

*  `allow_gift_receipt`
*  `allow_gift_wrapping_on_order`
*  `allow_printed_card`
*  `cart_gift_wrapping`
*  `cart_printed_card`
*  `printed_card_price`
*  `sales_gift_wrapping`
*  `sales_printed_card`

Gift wrapping is available for simple, configurable, bundle products as well as physical gift cards.

## Syntax

`mutation: {setGiftOptionsOnCart(input: SetGiftOptionsOnCartInput): SetGiftOptionsOnCartOutput}`

## Example usage

The following example adds a gift message, gift wrapping, and a gift receipt to the cart.

**Request:**

```graphql
mutation {
  setGiftOptionsOnCart(
    input: {
      cart_id: "8k0Q4MpH2IGahWrTRtqM61YV2MtLPApz"
      gift_message: {
        to: "Alex"
        from: "Veronica"
        message: "Happy Birthday!"
      }
      gift_wrapping_id: "Mg=="
      gift_receipt_included: true
      printed_card_included: false
    }
  ) {
    cart {
      id
      gift_message {
        to
        from
        message
      }
      gift_wrapping {
        uid
      }
      gift_receipt_included
      printed_card_included
      items {
        quantity
        prices {
          price {
            value
            currency
          }
        }
      }
      prices {
        gift_options {
          gift_wrapping_for_order {
            value
            currency
          }
        }
        grand_total {
          value
          currency
        }
      }
    }
  }
}
```

**Response:**

```json
{
  "data": {
    "setGiftOptionsOnCart": {
      "cart": {
        "id": "8k0Q4MpH2IGahWrTRtqM61YV2MtLPApz",
        "gift_message": {
            "to": "Alex"
            "from": "Veronica"
            "message": "Happy Birthday!"
        }
        "gift_wrapping": {
          "uid": "Mg=="
        },
        "gift_receipt_included": true,
        "printed_card_included": false,
        "items": [
          {
            "quantity": 1,
            "prices": {
              "price": {
                "value": 32,
                "currency": "USD"
              }
            }
          },
          {
            "quantity": 1,
            "prices": {
              "price": {
                "value": 84,
                "currency": "USD"
              }
            }
          }
        ],
        "prices": {
          "gift_options": {
            "gift_wrapping_for_order": {
              "value": 7,
              "currency": "USD"
            }
          },
          "grand_total": {
            "value": 132.57,
            "currency": "USD"
          }
        }
      }
    }
  }
}
```

## Input attributes

The `SetGiftOptionsOnCartInput` object can contain the following attributes:

Attribute |  Data Type | Description
--- | --- | ---
`cart_id` | String! | The unique ID that identifies the shopper's cart
`gift_message` | [GiftMessageInput](#GiftMessageInput) | Gift message details for the cart
`gift_receipt_included` | Boolean! | Indicates whether the customer requested a gift receipt for the cart
`gift_wrapping_id` | ID | The unique ID for a `GiftWrapping` object to be used for the cart
`printed_card_included` | Boolean! | Indicates whether the customer requested a printed card for the cart

### GiftMessageInput

The `GiftMessageInput` object must contain the following attributes:

Attribute |  Data Type | Description
--- | --- | ---
`from` | String! | The name of the gift sender
`message` | String! | The text of the gift message
`to` | String! | The name of the gift recipient

## Output attributes

The `SetGiftOptionsOnCartOutput` object contains the `Cart` object.

Attribute |  Data Type | Description
--- | --- | ---
`cart` |[Cart!](#cart-object) | Describes the contents of the specified shopping cart

### Cart object

import CartObject from '/src/_includes/graphql/cart-object-24.md'

<CartObject />

[Cart query output](../../cart/queries/cart.md#output-attributes) provides more information about the `Cart` object.

## Errors

Error | Description
--- | ---
`Could not find a cart with ID "XXX"` | The specified `cart_id` value does not exist in the `quote_id_mask` table.
`Field SetBillingAddressOnCartInput.cart_id of required type String! was not provided.` | The value specified in the `SetShippingAddressesOnCartInput`.`cart_id` argument is empty.
`Field CartAddressInput.firstname of required type String! was not provided.` | The value specified in the `shipping_addresses`.`firstname` argument is empty.
`Field CartAddressInput.lastname of required type String! was not provided.` | The value specified in the `shipping_addresses`.`lastname` argument is empty.
`Field CartAddressInput.city of required type String! was not provided.` | The value specified in the `shipping_addresses`.`city` argument is empty.
`Field CartAddressInput.street of required type String! was not provided.` | The value specified in the `shipping_addresses`.`street` argument is empty.
`Field CartAddressInput.country_code of required type String! was not provided.` | The value specified in the `shipping_addresses`.`country_code` argument is empty.
`Field SetBillingAddressOnCartInput.billing_address of required type BillingAddressInput! was not provided.` | The `shipping_addresses` input attribute of type `ShippingAddressInput` is missing.
