# Task 1 – GTM Event Schema

## Introduction

The purpose of this document is to define the GTM events that should be implemented on the OrthoNow website. These events will help measure important user actions such as appointment bookings, phone calls, WhatsApp clicks, PDF downloads, and user engagement. The collected event data will be processed through Google Tag Manager (GTM) and sent to Google Analytics 4 (GA4) for reporting, funnel analysis, audience creation, and conversion tracking.

---

# 1. GTM Event Schema

| Event Name | Trigger Type | Key Parameters (Minimum 3) | GA4 Report / Audience |
|------------|--------------|----------------------------|-----------------------|
| booking_step_complete | Custom Event (dataLayer) | clinic_location, specialty, page_name | Funnel Exploration |
| booking_step_complete | Custom Event (dataLayer) | patient_name, phone_number, preferred_date | Funnel Exploration |
| booking_step_complete | Custom Event (dataLayer) | booking_id, clinic_location, specialty | Conversions Report, Google Ads Conversion |
| call_now_click | Click Trigger | phone_number, clinic_location, page_name | Engagement Report |
| whatsapp_click | Link Click | page_name, clinic_location, traffic_source | Engaged Users Audience |
| patient_guide_download | Form Submission + File Download | guide_name, patient_phone, page_name | Lead Generation Audience |
| clinic_page_view | Page View | clinic_name, city, page_url | Pages & Screens Report |
| blog_scroll_90 | Scroll Depth Trigger (90%) | article_name, category, scroll_percentage | Content Engagement Report |

---

# 2. Booking Funnel Tracking

The appointment booking form contains three steps.

**Step 1**
- Select Clinic Location
- Select Specialty

**Step 2**
- Enter Name
- Enter Phone Number
- Select Preferred Date

**Step 3**
- Confirm Appointment

Each step of the booking form sends a custom `window.dataLayer.push()` event when the user successfully completes that step. Google Tag Manager listens for these events and forwards them to Google Analytics 4 (GA4), allowing the booking journey to be analysed through Funnel Exploration reports.

---

## Step 1 dataLayer Push

```javascript
window.dataLayer = window.dataLayer || [];

window.dataLayer.push({
  event: "booking_step_complete",
  step_number: 1,
  step_name: "location_specialty_selected",
  clinic_location: "Bengaluru",
  specialty: "Orthopaedics"
});
```

---

## Step 2 dataLayer Push

```javascript
window.dataLayer.push({
  event: "booking_step_complete",
  step_number: 2,
  step_name: "patient_details_entered",
  patient_name: "Rahul Sharma",
  phone_number: "9876543210",
  preferred_date: "2026-07-25"
});
```

---

## Step 3 dataLayer Push

```javascript
window.dataLayer.push({
  event: "booking_step_complete",
  step_number: 3,
  step_name: "booking_confirmed",
  booking_id: "ORTHO10234",
  clinic_location: "Bengaluru",
  specialty: "Orthopaedics"
});
```

---

# 3. Funnel Drop-off Tracking

The booking journey will be measured using the three booking step events.

Booking Funnel

Step 1 → Select Clinic & Specialty

↓

Step 2 → Enter Patient Details

↓

Step 3 → Booking Confirmed

If users leave the process before completing the next step, GA4 Funnel Exploration will automatically show the drop-off percentage.

For example:

- 100 users complete Step 1
- 70 users complete Step 2
- 45 users complete Step 3

This indicates:

- 30% drop-off between Step 1 and Step 2
- 25% drop-off between Step 2 and Step 3

This data helps identify which booking step causes users to abandon the process and where improvements should be made.

---

# 4. Google Ads Conversion

**Recommended Conversion Event**

```
booking_completed
```

### Why?

The booking_completed event represents a successful appointment booking, which is the primary business objective of the website.

Unlike clicks or page views, this event directly measures completed conversions and allows Google Ads to optimize campaigns toward users who are most likely to book a consultation.

This event can be imported into Google Ads as a Primary Conversion, allowing Smart Bidding strategies such as Maximize Conversions or Target CPA to optimize campaigns based on completed appointment bookings.

---

# Conclusion

The proposed GTM event schema provides complete visibility into the user journey on the OrthoNow website. It enables accurate tracking of appointment bookings, phone calls, WhatsApp interactions, content engagement, and lead generation. This implementation will help the marketing team analyse user behaviour, reduce booking drop-offs, and optimise Google Ads campaigns using reliable conversion data.