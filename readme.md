# Custom Product Labels

This theme supports customizable product labels for both product cards and the product detail page (PDP), with controls available via **theme settings** and **variant metafields**.

---

## Theme Settings

Located under: `Theme Settings → Product labels`

### Display Controls
- **Show label on product cards** (`show_product_label_on_card`)
- **Show label on product detail page (PDP)** (`show_product_label_on_pdp`)

### Position Options
- **Card Label Position** (`card_label_position`): `image`, `price`
- **PDP Label Position** (`product_label_position`): `price`, `block`

### Appearance Controls
- **Default Colors**  
  - `product_label_default_text_color` (e.g., `#ffffff`)  
  - `product_label_default_bg_color` (e.g., `#000000`)
- **Border Radius** (`product_label_border_radius`, in `rem`)
- **Padding** (`product_label_padding`, in `rem`)
- **Font Size** (`product_label_font_size`, in `rem`)
- **Font Weight** (`product_label_font_weight`): `400` (normal), `600` (semi-bold)
- **Text Transform** (`product_label_text_transform`): `uppercase`, `capitalize`, `none`
- **Low Stock Threshold** (`product_label_low_stock_threshold`): default `25`

These settings apply globally and act as style defaults unless overridden at the variant level.

---

## Variant Metafields

To customize a product label on a specific variant, use the following metafields (namespace: `custom_labels`):

| Key                       | Type               | Example       | Description                                   |
|---------------------------|--------------------|---------------|-----------------------------------------------|
| `label`                   | Single line text   | `Best Seller` | Label text to be displayed                    |
| `text_color`              | Color              | `#ffffff`     | Override for text color                       |
| `bg_color`                | Color              | `#000000`     | Override for background color                 |
| `label_priority`          | Single line text   | `sale`        | Priority logic: `sale`, `low_stock`, `custom` |

---

## Label Priority Logic

The label resolution follows this logic:

1. **If sold out**, display: `Sold Out`
2. If `label_priority` is:
   - `sale`:  
     - If variant is discounted → show `Sale`  
     - Else → show custom label (if defined)
   - `low_stock`:  
     - If under low stock threshold → show `Low Stock`  
     - Else → show custom label (if defined)
   - `custom`:  
     - Show custom label if defined
3. **If `label_priority` is blank**, fallback to:
   - Custom label (if defined)
   - `Sale` (if discounted)
   - `Low Stock` (if under threshold)

---

## Output & Styling

The label is rendered as:

```html
<div class="custom-product-label" style="...">
  <span class="custom-product-label__text">Label Text</span>
</div>