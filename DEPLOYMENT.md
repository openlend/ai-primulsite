# 🚀 Deployment Checklist
## ai.primulsite.ro Landing Page

---

## ✅ Pre-Deployment

- [x] Landing page built (index.html)
- [x] README documentation complete
- [x] All sections implemented
- [x] Mobile responsive design
- [x] SEO meta tags added
- [x] Structured data (Schema.org) included
- [x] Form validation working
- [ ] Backend form endpoint configured
- [ ] Analytics tracking code added

---

## 📤 Deployment Steps

### Step 1: Prepare File

```bash
# From Docker container
docker cp CONTAINER_ID:/data/.openclaw/workspace/projects/primulsite/landing/index.html ~/Desktop/

# Or directly access file at:
/data/.openclaw/workspace/projects/primulsite/landing/index.html
```

### Step 2: Upload to Server

**Via cPanel File Manager (RECOMMENDED):**

1. Login to cPanel:
   ```
   URL: https://primulsite.ro:2083
   Username: [your_username]
   Password: [your_password]
   ```

2. Navigate to File Manager

3. Go to: `/public_html/`

4. Create `ai` folder (if not exists):
   - Click "New Folder"
   - Name: `ai`
   - Click "Create New Folder"

5. Enter `ai` folder

6. Upload `index.html`:
   - Click "Upload"
   - Select file from Desktop
   - Wait for upload to complete

7. Verify file permissions:
   - Right-click index.html
   - Select "Change Permissions"
   - Set to: 644 (read/write for owner, read for group/world)

### Step 3: Configure DNS (if needed)

**If subdomain doesn't exist:**

1. In cPanel, go to "Subdomains"
2. Create subdomain:
   ```
   Subdomain: ai
   Domain: primulsite.ro
   Document Root: /public_html/ai
   ```
3. Click "Create"
4. Wait 5-15 minutes for DNS propagation

### Step 4: Test

1. Open browser (incognito mode recommended)

2. Visit: `https://ai.primulsite.ro`

3. Check:
   - [ ] Page loads without errors
   - [ ] All sections visible
   - [ ] Mobile view works (DevTools)
   - [ ] Form validation works
   - [ ] Smooth scrolling works
   - [ ] CTAs scroll to contact form

---

## 🔧 Post-Deployment Configuration

### 1. Form Backend Integration

**Option A: EmailJS (Recommended - Free, Easy)**

1. Sign up: https://www.emailjs.com/
2. Create email service (Gmail/Outlook)
3. Create email template
4. Get Service ID + Template ID
5. Add to index.html before `</body>`:
   ```html
   <script src="https://cdn.jsdelivr.net/npm/@emailjs/browser@3/dist/email.min.js"></script>
   <script>
     emailjs.init('YOUR_PUBLIC_KEY');
   </script>
   ```
6. Update form submission (line ~1190)

**Option B: Custom Backend**
- Build API endpoint at `https://api.primulsite.ro/leads`
- Update fetch URL in JavaScript

**Option C: Webhook (Make.com / Zapier)**
- Create webhook trigger
- Connect to Gmail/CRM
- Update fetch URL

### 2. Google Analytics 4

1. Create GA4 property: https://analytics.google.com/

2. Get Measurement ID (format: G-XXXXXXXXXX)

3. Add before `</head>` in index.html:
   ```html
   <!-- Google Analytics -->
   <script async src="https://www.googletagmanager.com/gtag/js?id=G-XXXXXXXXXX"></script>
   <script>
     window.dataLayer = window.dataLayer || [];
     function gtag(){dataLayer.push(arguments);}
     gtag('js', new Date());
     gtag('config', 'G-XXXXXXXXXX');
   </script>
   ```

### 3. Google Search Console

1. Visit: https://search.google.com/search-console

2. Add property: `ai.primulsite.ro`

3. Verify ownership (DNS TXT record or HTML file)

4. Submit sitemap (create simple sitemap.xml):
   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <urlset xmlns="http://www.sitemaps.org/schemas/sitemap/0.9">
     <url>
       <loc>https://ai.primulsite.ro/</loc>
       <changefreq>weekly</changefreq>
       <priority>1.0</priority>
     </url>
   </urlset>
   ```

### 4. Bing Webmaster Tools

1. Visit: https://www.bing.com/webmasters

2. Add site: `ai.primulsite.ro`

3. Verify ownership (meta tag or file)

4. Submit sitemap

5. **CRITICAL:** This is the main product - ensure site is indexed properly!

### 5. Facebook Pixel (Optional)

If running Facebook ads:

1. Get Pixel ID from Facebook Business Manager

2. Add before `</head>`:
   ```html
   <!-- Facebook Pixel -->
   <script>
     !function(f,b,e,v,n,t,s){if(f.fbq)return;n=f.fbq=function(){n.callMethod?
     n.callMethod.apply(n,arguments):n.queue.push(arguments)};
     if(!f._fbq)f._fbq=n;n.push=n;n.loaded=!0;n.version='2.0';
     n.queue=[];t=b.createElement(e);t.async=!0;
     t.src=v;s=b.getElementsByTagName(e)[0];
     s.parentNode.insertBefore(t,s)}(window, document,'script',
     'https://connect.facebook.net/en_US/fbevents.js');
     fbq('init', 'YOUR_PIXEL_ID');
     fbq('track', 'PageView');
   </script>
   ```

3. Add event tracking on form submit:
   ```javascript
   fbq('track', 'Lead');
   ```

---

## 🧪 Testing Checklist

### Functionality Tests

- [ ] **Homepage loads:** https://ai.primulsite.ro
- [ ] **Hero section:** Headline + CTA visible
- [ ] **Stats bar:** 4 stats display correctly
- [ ] **Problem section:** 3 cards render
- [ ] **Solution section:** 2-column layout (desktop)
- [ ] **How it works:** 3 steps visible
- [ ] **Testimonial:** Carmen quote + avatar
- [ ] **Pricing:** 3 packages with correct prices
- [ ] **Contact form:** All 4 fields + submit button
- [ ] **Footer:** Links work
- [ ] **Smooth scroll:** CTAs scroll to contact form
- [ ] **Form validation:** Required fields validated
- [ ] **Success message:** Shows after submit

### Mobile Tests (< 768px)

- [ ] **Responsive layout:** Single column on mobile
- [ ] **Navigation:** Logo + CTA button visible
- [ ] **Hero:** Headline readable, CTA tappable
- [ ] **Stats:** Stack vertically
- [ ] **Cards:** Stack vertically
- [ ] **Form:** Full width, easy to fill
- [ ] **Touch targets:** Buttons > 44px height

### Performance Tests

1. **PageSpeed Insights:**
   - URL: https://pagespeed.web.dev/
   - Target: Score > 90 (mobile & desktop)

2. **GTmetrix:**
   - URL: https://gtmetrix.com/
   - Target: Grade A, Load time < 2s

3. **WebPageTest:**
   - URL: https://www.webpagetest.org/
   - Target: First Contentful Paint < 1s

### SEO Tests

1. **Google Rich Results Test:**
   - URL: https://search.google.com/test/rich-results
   - Check: LocalBusiness + Service structured data validates

2. **Mobile-Friendly Test:**
   - URL: https://search.google.com/test/mobile-friendly
   - Check: Page is mobile-friendly

3. **Meta Tags:**
   - View source: Ctrl+U
   - Verify: title, description, og:tags present

### Browser Compatibility

- [ ] **Chrome:** Latest version
- [ ] **Firefox:** Latest version
- [ ] **Safari:** Latest version (Mac/iOS)
- [ ] **Edge:** Latest version
- [ ] **Mobile Safari:** iOS 14+
- [ ] **Mobile Chrome:** Android 10+

---

## 📊 Analytics Setup

### Key Metrics to Track

**Traffic:**
- Page views
- Unique visitors
- Traffic sources (organic, direct, social, paid)
- Geographic location (Romania focus)

**Engagement:**
- Bounce rate (target: < 40%)
- Average session duration (target: > 2 min)
- Scroll depth (% who see pricing)
- CTA click rate (hero + nav)

**Conversions:**
- Form submissions (goal: track as conversion)
- Form start rate (first field focus)
- Form completion rate (submit / start)
- Package interest (which pricing CTA clicked)

**Technical:**
- Page load time
- Core Web Vitals (LCP, FID, CLS)
- Error rate (JavaScript errors)
- Device breakdown (mobile vs desktop)

### Event Tracking (GA4)

```javascript
// Hero CTA click
gtag('event', 'cta_click', {
  'location': 'hero',
  'text': 'Verifică GRATUIT'
});

// Pricing CTA click
gtag('event', 'pricing_cta_click', {
  'package': 'Setup Pro',
  'price': '2500'
});

// Form submission
gtag('event', 'form_submit', {
  'form_name': 'contact',
  'form_destination': '/thank-you'
});
```

---

## 🔒 Security Checklist

- [ ] **HTTPS:** Site uses SSL (check padlock)
- [ ] **Form validation:** Client-side + server-side
- [ ] **CSRF protection:** If using backend
- [ ] **Rate limiting:** Prevent spam submissions
- [ ] **Email validation:** Verify real email addresses
- [ ] **Phone validation:** Romanian format (+40)
- [ ] **reCAPTCHA:** Consider adding if spam is issue
- [ ] **GDPR compliance:** Privacy policy link (if collecting data)

---

## 🚨 Troubleshooting

### Issue: Page doesn't load

**Check:**
1. DNS propagation (can take 24h)
2. File permissions (should be 644)
3. Server error logs (cPanel → Error Log)
4. .htaccess file (shouldn't block ai subdomain)

### Issue: Styling broken

**Check:**
1. CSS inline (not external file)
2. Browser cache (Ctrl+Shift+R to hard refresh)
3. View source - CSS should be in `<style>` tag

### Issue: Form doesn't work

**Check:**
1. JavaScript console (F12 → Console tab)
2. Form endpoint configured (currently placeholder)
3. CORS settings (if using external API)
4. Network tab (F12 → Network) to see request

### Issue: Structured data errors

**Test:**
1. Google Rich Results Test
2. Schema.org Validator
3. Check JSON-LD syntax (comma errors common)

---

## 📞 Support Contacts

**Technical Issues:**
- Developer: Atlas (via Radu)
- Email: radu@radubalas.com
- WhatsApp: +40730688360

**Hosting Issues:**
- cPanel support: Check hosting provider docs
- DNS issues: Check domain registrar

**Marketing Questions:**
- Agency: PrimulSite.ro
- Email: contact@primulsite.ro

---

## ✅ Final Checklist

**Before Going Live:**

- [ ] File uploaded to `/public_html/ai/index.html`
- [ ] DNS configured (ai.primulsite.ro)
- [ ] SSL certificate active (HTTPS)
- [ ] Page loads without errors
- [ ] Mobile responsive verified
- [ ] Form backend configured
- [ ] Analytics tracking added
- [ ] Search Console submitted
- [ ] Bing Webmaster Tools submitted
- [ ] Performance tested (PageSpeed > 90)
- [ ] SEO validated (Rich Results Test)
- [ ] Cross-browser tested
- [ ] Team notified of launch

**After Launch:**

- [ ] Monitor analytics daily (first week)
- [ ] Check form submissions work
- [ ] Monitor page speed weekly
- [ ] Review Search Console weekly
- [ ] Track conversion rate
- [ ] A/B test headlines (after 100+ visitors)
- [ ] Collect user feedback
- [ ] Update pricing if needed
- [ ] Add testimonials as they come in

---

## 🎯 Success Metrics (30 Days)

**Traffic Goals:**
- 500+ unique visitors
- 50+ organic search visitors
- < 40% bounce rate

**Conversion Goals:**
- 20+ form submissions (4% conversion rate)
- 5+ free audit requests
- 2+ paid package sales

**Technical Goals:**
- PageSpeed score > 90
- 0 JavaScript errors
- < 2s page load time
- 100% mobile usability

---

**🗺️ Built by Atlas - March 16, 2026**

_"Make it STUNNING - this needs to convert leads."_ ✅ DONE.
