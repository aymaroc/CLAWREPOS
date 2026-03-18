# SEO Enhancement via Metaobjects

## Overview
Add metaobjects to EXISTING product cards and blog templates for enhanced SEO without creating new sections.

## Product Card Metaobjects

### 1. Product Enhancements Metaobject
**Namespace:** `product_enhancements`

```json
{
  "fields": [
    {
      "key": "scent_profile",
      "type": "string",
      "description": "Primary scent (e.g., 'Oud', 'Rose', 'Fresh')"
    },
    {
      "key": "scent_notes",
      "type": "string",
      "description": "Detailed scent notes"
    },
    {
      "key": "occasion_tags",
      "type": "list.string",
      "description": "Suitable occasions"
    },
    {
      "key": "longevity_hours",
      "type": "number_integer",
      "description": "Fragrance longevity in hours"
    },
    {
      "key": "sillage_level",
      "type": "string",
      "description": "Projection level (Light, Moderate, Heavy)"
    }
  ]
}
```

### 2. Schema.org Structured Data
Add to product templates:

```liquid
<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@type": "Product",
  "name": "{{ product.title }}",
  "description": "{{ product.description }}",
  "image": "{{ product.featured_image | img_url: '500x500' }}",
  "brand": {
    "@type": "Brand",
    "name": "Sara Sakina"
  },
  "offers": {
    "@type": "AggregateOffer",
    "priceCurrency": "{{ shop.currency }}",
    "lowPrice": "{{ product.price_min | money_without_currency }}",
    "highPrice": "{{ product.price_max | money_without_currency }}",
    "availability": "{% if product.available %}InStock{% else %}OutOfStock{% endif %}"
  },
  "aggregateRating": {
    "@type": "AggregateRating",
    "ratingValue": "{{ product.metafields.judgeme.rating }}",
    "reviewCount": "{{ product.metafields.judgeme.review_count }}"
  }
}
</script>
```

## Blog Template Metaobjects

### 1. Blog Post Enhancement Metaobject
**Namespace:** `blog_post_enhancements`

```json
{
  "fields": [
    {
      "key": "featured_products",
      "type": "list.product_reference",
      "description": "Featured products in this post"
    },
    {
      "key": "scent_categories",
      "type": "list.string",
      "description": "Scent profiles mentioned"
    },
    {
      "key": "reading_time_minutes",
      "type": "number_integer",
      "description": "Estimated reading time"
    },
    {
      "key": "seo_keywords",
      "type": "string",
      "description": "Primary SEO keywords"
    },
    {
      "key": "meta_description",
      "type": "string",
      "description": "Custom meta description"
    }
  ]
}
```

### 2. Blog Article Schema
```liquid
<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@type": "BlogPosting",
  "headline": "{{ article.title }}",
  "description": "{{ article.excerpt_or_content | strip_html | truncatewords: 30 }}",
  "image": "{{ article.image | img_url: '1200x600' }}",
  "datePublished": "{{ article.published_at | date: '%Y-%m-%dT%H:%M:%SZ' }}",
  "dateModified": "{{ article.updated_at | date: '%Y-%m-%dT%H:%M:%SZ' }}",
  "author": {
    "@type": "Person",
    "name": "{{ article.author }}"
  },
  "publisher": {
    "@type": "Organization",
    "name": "Sara Sakina",
    "logo": {
      "@type": "ImageObject",
      "url": "{{ shop.url }}/logo.png"
    }
  }
}
</script>
```

## Implementation Instructions

### Step 1: Add to Product Card Template
In your product card Liquid file, add metafield references:

```liquid
{% if product.metafields.product_enhancements.scent_profile %}
  <span data-scent-profile>{{ product.metafields.product_enhancements.scent_profile }}</span>
{% endif %}

{% if product.metafields.product_enhancements.longevity_hours %}
  <span data-longevity>{{ product.metafields.product_enhancements.longevity_hours }}hr longevity</span>
{% endif %}
```

### Step 2: Add to Blog Templates
In your blog article template:

```liquid
{% if article.metafields.blog_post_enhancements.reading_time_minutes %}
  <span data-reading-time>{{ article.metafields.blog_post_enhancements.reading_time_minutes }} min read</span>
{% endif %}
```

### Step 3: Inject Schema Markup
Add schema.org JSON-LD to both templates (see above).

## SEO Benefits

✅ Rich snippets in search results
✅ Better SERP appearance
✅ Voice search optimization
✅ Schema validation passes
✅ Featured snippet eligibility
✅ Improved click-through rate

## Animation Integration

Combine with animations-injection.liquid for:
- Metafield data animates in with stagger effect
- Schema rich snippets visible in search
- Product details slide up on hover
- Reading time fades in on scroll
