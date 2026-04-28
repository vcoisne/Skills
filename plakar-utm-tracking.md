# Plakar UTM Tracking Skill
## Social + Affiliate Link Attribution System

### Purpose
This skill defines a **consistent, scalable system** for generating UTM-tagged links across:
- Social media
- Affiliate / partner channels
- Campaign tracking

It is designed to:
- Eliminate inconsistent naming
- Enable clean attribution
- Support automation via APIs or link tools

---

## Core Rule
Every tracked URL MUST include:

```
utm_source
utm_medium
utm_campaign
utm_content
```

No exceptions. No freeform parameters.

---

## 1. Parameter Definitions

### utm_source (WHO sends traffic)

#### Owned channels
- linkedin
- twitter
- youtube
- newsletter

#### Partners / affiliates
Format:
```
partner_<name>
```

Examples:
- partner_aws
- partner_acme
- partner_devto

**Rule:**  
If Plakar does not control the channel → use `partner_` prefix.

---

### utm_medium (CHANNEL TYPE)
Allowed values (strict list):
- social
- affiliate
- email
- paid
- referral

**Rules:**
- Do not invent new values
- Do not combine concepts (e.g. "paid-social")

---

### utm_campaign (INITIATIVE)
Format:
```
<type>-<descriptor>-<quarter-or-theme>
```

Examples:
- launch-plakar-backup-q2
- evergreen-kubernetes-backup
- promo-summer-2026
- feature-ceph-support

**Rules:**
- Campaign = business initiative (not individual post)
- Avoid exact dates → prefer quarters or themes
- Multiple links/posts should share the same campaign

---

### utm_content (VARIANT / CREATIVE)
Used to differentiate content performance.

#### Social examples
- video-demo
- thread-problem
- carousel-benefits
- cta-book-demo

#### Affiliate examples
- review-article
- banner-cta
- textlink-footer

**Rule:**  
This is the main A/B testing dimension.

---

## 2. Examples

### Social post (LinkedIn)
```
utm_source=linkedin
utm_medium=social
utm_campaign=launch-plakar-backup-q2
utm_content=video-demo
```

---

### Social post (Twitter thread)
```
utm_source=twitter
utm_medium=social
utm_campaign=launch-plakar-backup-q2
utm_content=thread-problem
```

---

### Affiliate blog post
```
utm_source=partner_acme
utm_medium=affiliate
utm_campaign=evergreen-kubernetes-backup
utm_content=review-article
```

---

### Affiliate banner
```
utm_source=partner_acme
utm_medium=affiliate
utm_campaign=promo-summer-2026
utm_content=banner-cta
```

---

## 3. System Design Principles

### 1. Consistency over flexibility
- Use predefined values only
- Avoid free text

### 2. Lowercase only
- Prevent duplicates (LinkedIn ≠ linkedin)

### 3. Hyphen-separated values
- Improves readability and reporting

### 4. Separation of concerns
- source = platform or partner
- medium = channel type
- campaign = initiative
- content = creative

---

## 4. Anti-Patterns (DO NOT DO)

### ❌ Mixing dimensions
```
utm_source=linkedin_ads
utm_medium=paid-social
```

### ✅ Correct
```
utm_source=linkedin
utm_medium=paid
```

---

### ❌ Generic affiliate source
```
utm_source=affiliate
```

### ✅ Correct
```
utm_source=partner_acme
```

---

### ❌ One campaign per post
```
utm_campaign=linkedin-post-1
utm_campaign=linkedin-post-2
```

### ✅ Correct
```
utm_campaign=launch-plakar-backup-q2
```

---

## 5. Automation Guidelines

### Link generation
- Use a centralized system (API or link tool)
- Never build UTMs manually

### Templates
```
?utm_source={source}&utm_medium={medium}&utm_campaign={campaign}&utm_content={content}
```

### CMS / workflow integration
- Use dropdowns for all parameters
- Store generated links per channel
- Auto-generate at publish time when possible

---

## 6. Affiliate Tracking Enhancement

For partners:
- Assign unique short links per partner
- Include UTMs underneath

Benefits:
- Redundant attribution (link ID + UTMs)
- Protection against UTM stripping
- Cleaner partner reporting

---

## 7. Outcomes

This system enables:
- Channel-level attribution (source + medium)
- Campaign performance tracking
- Creative-level insights (content)
- Reliable partner attribution

Without this system:
- Traffic becomes unattributed
- Campaign analysis breaks
- Partner ROI is unclear

---

## 8. Implementation Checklist
- [ ] Define approved values for all parameters
- [ ] Centralize link creation
- [ ] Enforce templates
- [ ] Remove manual UTM creation
- [ ] Educate team and partners
- [ ] Audit links regularly

---

## Summary

This skill ensures that all Plakar links are:
- Structured
- Consistent
- Automatable
- Measurable

It turns link tracking from a manual task into a **scalable growth system**.
