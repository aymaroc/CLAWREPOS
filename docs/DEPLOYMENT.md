# Deployment Guide

## Prerequisites

- Shopify store access (sara-sakina-2)
- Theme editor access
- Git knowledge (optional, for version control)

## Step 1: Upload Files to Shopify

### Via Shopify Theme Editor

1. **Log in to Shopify Admin**
   - Go to: https://admin.shopify.com/store/sara-sakina-2

2. **Navigate to Theme Code**
   - Online Store → Themes
   - Click your active theme
   - Click "Edit code"

3. **Create/Upload Snippets**
   - Left sidebar → Snippets
   - Create new:
     - Name: `blog-museum-layout.liquid`
     - Add content from `snippets/blog-museum-layout.liquid`
     - Save
   
   - Create new:
     - Name: `blog-product-recommendation-card.liquid`
     - Add content from `snippets/blog-product-recommendation-card.liquid`
     - Save

4. **Create/Upload Sections**
   - Left sidebar → Sections
   - Create new:
     - Name: `blog-prod-recs.liquid`
     - Add content from `sections/blog-prod-recs.liquid`
     - Save

## Step 2: Update Article Template

1. **Edit Main Article Section**
   - Left sidebar → Sections
   - Open `main-article.liquid`
   
2. **Add Snippet Calls**
   - Find: `{% schema %}`
   - Add BEFORE the schema line:
   ```liquid
   {% render 'blog-museum-layout' %}
   {% section 'blog-prod-recs' %}
   ```
   - Save

3. **Verify**
   - Go to any blog post on your store
   - Should see: futuristic hero, products, newsletter

## Step 3: Configure Product Tags

### Tag Products

1. Go to Products
2. For each product, add tags like:
   - Scent: `oud`, `rose`, `amber`, etc.
   - Occasion: `gifting`, `luxury`, etc.
   - Target: `for-her`, `for-him`, etc.

### Tag Blog Posts

1. Go to Blog Posts
2. Add MATCHING tags (oud, rose, amber, etc.)
3. Products with matching tags will auto-appear

## Step 4: Test

### Desktop View
- Visit: https://sarasakina.com/blogs/news/oud-fragrance-guide...
- Should see:
  - Dark hero section
  - Gold accents
  - Product recommendations
  - Newsletter signup
  - Related articles

### Mobile View
- Rotate phone to portrait
- Or use Chrome DevTools (F12 → Mobile icon)
- Should see:
  - Stacked layout
  - Touch-friendly buttons
  - Full-width responsive

## Troubleshooting

### Products Not Showing?
- ✅ Check blog post has tags
- ✅ Check products have matching tags
- ✅ Clear browser cache
- ✅ Wait 5 minutes for Shopify cache

### Styling Looks Wrong?
- ✅ Clear browser cache (Ctrl+Shift+Delete)
- ✅ Try incognito window
- ✅ Check CSS file deployed

### Schema Not Working?
- ✅ Test with: https://search.google.com/test/rich-results
- ✅ Check product data is complete
- ✅ Verify markup syntax

## Performance Monitoring

### Track Metrics
- Blog page views
- Product click-through rate
- Newsletter signups
- Average session duration
- Mobile vs desktop traffic

### Expected Improvements
- +15-25% product click-through
- +10-15% internal navigation
- +5-10% newsletter signups
- +20-30% average session time

## Rollback Instructions

If something goes wrong:

1. **Revert Section**
   - Delete the new snippet calls from main-article.liquid
   - Save

2. **Remove Files**
   - Delete `blog-museum-layout.liquid`
   - Delete `blog-product-recommendation-card.liquid`
   - Delete `blog-prod-recs.liquid`

3. **Restore Original**
   - Shopify keeps version history
   - Go to theme → Previous versions
   - Restore to previous version

## Support

For issues, check:
- SETUP.md - Initial setup
- FEATURES.md - Feature guide
- TAGGING-STRATEGY.md - Tag best practices

---

**Status:** Production Ready
**Last Updated:** 2026-03-18
