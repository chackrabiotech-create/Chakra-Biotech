# SEO Implementation Guide - Chakra Biotech Frontend

## Overview

This document outlines the comprehensive SEO implementation for the Chakra Biotech website, including metadata, structured data, sitemaps, and best practices.

## 1. Metadata Configuration

### Root Layout (`src/app/layout.tsx`)

- **Title Template**: Dynamic titles for all pages
- **Open Graph**: Social media sharing optimization
- **Twitter Cards**: Enhanced Twitter sharing
- **Robots**: Search engine crawling instructions
- **Verification**: Google/Bing verification codes

### Page-Specific Metadata

Each route has its own `layout.tsx` with optimized metadata:

- `/about` - Company information and mission
- `/products` - Product catalog
- `/training` - Training programs
- `/blog` - Blog articles
- `/gallery` - Image gallery
- `/contact` - Contact information
- `/pharmacy` - Wellness and pharmaceutical applications

## 2. Structured Data (JSON-LD)

### Available Schema Types

Located in `src/lib/seo/structured-data.ts`:

1. **Organization Schema** - Company information
2. **Local Business Schema** - Physical location details
3. **Product Schema** - Individual product pages
4. **Article Schema** - Blog posts
5. **Breadcrumb Schema** - Navigation hierarchy
6. **FAQ Schema** - Frequently asked questions

### Usage Example

```tsx
import { StructuredData } from "@/components/seo/StructuredData";
import { generateProductSchema } from "@/lib/seo/structured-data";

export default function ProductPage() {
  const productData = generateProductSchema({
    name: "Premium Aeroponic Saffron",
    description: "100% pure saffron",
    price: 2500,
    image: "/product.jpg",
    rating: 4.8,
    reviewCount: 150,
  });

  return (
    <>
      <StructuredData data={productData} />
      {/* Page content */}
    </>
  );
}
```

## 3. Sitemap

### Dynamic Sitemap (`src/app/sitemap.ts`)

- Automatically generates XML sitemap
- Includes all static routes
- Can be extended to include dynamic routes (products, blog posts)
- Accessible at: `/sitemap.xml`

### Adding Dynamic Routes

Uncomment and modify the example in `sitemap.ts`:

```typescript
const products = await fetch(
  `${process.env.NEXT_PUBLIC_API_URL}/products`,
).then((res) => res.json());

const productRoutes = products.data.products.map((product: any) => ({
  url: `${siteUrl}/products/${product.slug}`,
  lastModified: new Date(product.updatedAt),
  changeFrequency: "weekly" as const,
  priority: 0.7,
}));
```

## 4. Robots.txt

### Configuration (`src/app/robots.ts`)

- Allows all search engines
- Disallows `/api/` and `/admin/` routes
- Points to sitemap location

## 5. Open Graph Images

### Default Image

- Location: `/public/og.webp`
- Dimensions: 1200x630px (recommended)
- Used across all pages for social sharing

### Custom OG Images

To use custom images per page, update the metadata in each layout:

```typescript
openGraph: {
  images: [
    {
      url: "/custom-og-image.webp",
      width: 1200,
      height: 630,
      alt: "Custom description",
    },
  ],
}
```

## 6. Environment Variables

### Required Variables

Create `.env.local` file:

```env
NEXT_PUBLIC_SITE_URL=https://chakrabiotech.com
NEXT_PUBLIC_API_URL=http://localhost:5000/api
NEXT_PUBLIC_WHATSAPP_NUMBER=919876543210
```

### Optional SEO Variables

```env
NEXT_PUBLIC_GOOGLE_VERIFICATION=your-verification-code
NEXT_PUBLIC_BING_VERIFICATION=your-verification-code
NEXT_PUBLIC_GA_ID=G-XXXXXXXXXX
```

## 7. Best Practices

### Title Optimization

- Keep titles under 60 characters
- Include primary keyword
- Use template for consistency
- Format: "Page Title | Chakra Biotech LLP"

### Description Optimization

- Keep between 150-160 characters
- Include call-to-action
- Use relevant keywords naturally
- Unique for each page

### Keywords

- Focus on long-tail keywords
- Include location-based keywords (Jaipur, Rajasthan)
- Use industry-specific terms (aeroponic, CEA, indoor cultivation)

### Image Optimization

- Use descriptive alt text
- Optimize file sizes (WebP format)
- Include keywords in filenames
- Proper dimensions for OG images

## 8. Performance Optimization

### Next.js Features

- Automatic code splitting
- Image optimization with `next/image`
- Font optimization
- Route prefetching

### Recommendations

1. Use `next/image` for all images
2. Implement lazy loading for below-fold content
3. Minimize JavaScript bundle size
4. Enable compression (Gzip/Brotli)
5. Use CDN for static assets

## 9. Monitoring & Analytics

### Google Search Console

1. Verify ownership using verification code
2. Submit sitemap: `https://chakrabiotech.com/sitemap.xml`
3. Monitor crawl errors
4. Track search performance

### Google Analytics

1. Add GA tracking code to root layout
2. Track page views and user behavior
3. Set up conversion goals
4. Monitor bounce rate and engagement

## 10. Local SEO

### Google My Business

- Claim and verify business listing
- Add accurate business information
- Upload photos of facility
- Encourage customer reviews
- Post regular updates

### Local Citations

- Ensure NAP (Name, Address, Phone) consistency
- List on relevant directories
- Focus on agriculture and agri-tech directories

## 11. Content Strategy

### Blog SEO

- Target specific keywords per article
- Use proper heading hierarchy (H1, H2, H3)
- Include internal links
- Add meta descriptions
- Use schema markup for articles

### Product Pages

- Unique descriptions for each product
- Include specifications and features
- Add customer reviews
- Use product schema markup
- Optimize images with alt text

## 12. Technical SEO Checklist

- [x] Meta titles and descriptions
- [x] Open Graph tags
- [x] Twitter Card tags
- [x] Structured data (JSON-LD)
- [x] XML sitemap
- [x] Robots.txt
- [x] Canonical URLs
- [x] Mobile responsiveness
- [ ] SSL certificate (HTTPS)
- [ ] Page speed optimization
- [ ] Schema validation
- [ ] Broken link checks

## 13. Validation Tools

### Testing Your SEO

1. **Google Rich Results Test**: Test structured data
   - https://search.google.com/test/rich-results

2. **Schema Markup Validator**: Validate JSON-LD
   - https://validator.schema.org/

3. **PageSpeed Insights**: Check performance
   - https://pagespeed.web.dev/

4. **Mobile-Friendly Test**: Verify mobile optimization
   - https://search.google.com/test/mobile-friendly

## 14. Maintenance

### Regular Tasks

- Update sitemap when adding new content
- Monitor search console for errors
- Update meta descriptions based on performance
- Refresh structured data as needed
- Check for broken links monthly
- Update content regularly

### Quarterly Reviews

- Analyze search performance
- Update keyword strategy
- Review and optimize underperforming pages
- Check competitor SEO strategies
- Update business information

## 15. Resources

### Documentation

- Next.js Metadata API: https://nextjs.org/docs/app/building-your-application/optimizing/metadata
- Schema.org: https://schema.org/
- Google Search Central: https://developers.google.com/search

### Tools

- Google Search Console
- Google Analytics
- Ahrefs / SEMrush
- Screaming Frog SEO Spider
- GTmetrix

---

## Support

For questions or issues related to SEO implementation, refer to:

- Next.js documentation
- Google Search Central guidelines
- Schema.org documentation

Last Updated: January 2026
