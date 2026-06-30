# Task 3 – Integration Design

## Introduction

This document describes how the OrthoNow consultation landing page can be integrated with HubSpot CRM, Karix WhatsApp API, and Google Ads Conversion Tracking. The objective is to capture patient enquiries, automate communication, and measure marketing conversions efficiently.

---

# 1. Integration Flow

The overall data flow is shown below:

Patient

↓

Landing Page (HTML Form)

↓

Backend API

↓

HubSpot CRM

↓

Karix WhatsApp API

↓

Google Ads Conversion Tracking

When a user submits the consultation form, the landing page sends the patient's details to a backend API. The backend processes the request and communicates with the required third-party services.

---

# 2. HubSpot CRM Integration

### Purpose

HubSpot CRM is used to store patient enquiries as leads.

### Process

1. User submits the consultation form.
2. The backend validates the submitted data.
3. The patient's information (Name and Phone Number) is sent to HubSpot using its Contacts API.
4. A new contact is created in HubSpot CRM.
5. The sales or support team can follow up with the patient.

### Data Sent

- Full Name
- Phone Number
- Form Name
- Lead Source

---

# 3. Karix WhatsApp Integration

### Purpose

Karix is used to send an automatic WhatsApp confirmation message after a successful consultation request.

### Process

1. After the lead is successfully created in HubSpot, the backend sends a request to the Karix WhatsApp API.
2. Karix delivers a confirmation message to the patient's registered mobile number.

### Example Message

Hello!

Thank you for booking your consultation with OrthoNow.

Our team will contact you shortly to confirm your appointment.

---

# 4. Google Ads Conversion Tracking

### Purpose

Google Ads Conversion Tracking measures successful consultation requests generated through advertising campaigns.

### Process

1. After successful form submission, a conversion event is triggered.
2. Google Tag Manager sends the event to Google Analytics 4 (GA4).
3. The conversion is imported into Google Ads.
4. Google Ads uses this data to optimise future advertising campaigns.

### Conversion Event

```
consultation_form_submitted
```

---

# 5. Error Handling

If any external service is temporarily unavailable:

- Validate all user inputs before sending data.
- Retry failed API requests when possible.
- Log errors for debugging.
- Display a successful confirmation message to the user without exposing technical errors.
- Prevent duplicate lead creation by checking request status.

---

# Conclusion

This integration design enables efficient lead management, automated patient communication, and accurate marketing performance tracking. By connecting the landing page with HubSpot CRM, Karix WhatsApp API, and Google Ads Conversion Tracking, OrthoNow can improve patient engagement and optimise its digital marketing campaigns.