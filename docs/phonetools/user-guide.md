# PhoneTools User Guide

This guide will walk you through installing, configuring, and using PhoneTools in your Salesforce organisation.

## Table of Contents

1. [Getting Started](#getting-started)
2. [Installation](#installation)
3. [Configuration](#configuration)
4. [Screening Operations](#screening-operations)
5. [Compliance Tracking](#compliance-tracking)
6. [Best Practices](#best-practices)
7. [Troubleshooting](#troubleshooting)

## Getting Started

PhoneTools is a Salesforce AppExchange application that screens your contact phone numbers against the UK Telephone Preference Service (TPS) and Corporate TPS (CTPS) lists. 

### Prerequisites

- Salesforce organisation (any edition)
- Administrator access to install applications
- UK-based phone numbers to screen

## Installation

### Step 1: Install from AppExchange

1. Go to [Salesforce AppExchange](https://appexchange.salesforce.com)
2. Search for "PhoneTools"
3. Click **Install**
4. Select your Salesforce organisation
5. Review permissions and click **Install**

### Step 2: Verify Installation

1. In Salesforce, navigate to **Setup**
2. Search for **Installed Packages**
3. Verify PhoneTools appears in the list

## Configuration

### Add Screening Fields to Records

1. Go to object layout (e.g., Contacts, Leads)
2. Add the following fields to your layout:
   - Phone Screening Status
   - Phone Screening Last Checked
   - Phone Screening Next Due
   - Phone Screening Results (JSON)

### Set Up Automated Screening

1. Navigate to **PhoneTools Settings**
2. Enable **Automated Screening**
3. Set your preferred screening schedule
4. Configure which object types to screen

## Screening Operations

### Manual Screening

1. Open a record with a phone number
2. Click the **Screen Phone Numbers** button
3. View results instantly in the Phone Screening Status field:
   - 🟢 **Green**: Number is safe to call
   - 🟡 **Amber**: Action recommended
   - 🔴 **Red**: Do not call - number is registered

### Batch Screening

Screen multiple records in one operation:

1. Go to list view for your records
2. Select multiple records
3. Click **Screen Phone Numbers** (batch)
4. Wait for processing to complete

### Flow-Based Screening

Use Salesforce Flows to queue immediate screening:

```
Flow: Screen Phone on Record Update
├─ Trigger: Record is created or updated
├─ Action: Queue Phone Screening Job
├─ Wait: For result
└─ Action: Update record with status
```

## Compliance Tracking

### Understanding the 28-Day Cycle

ICO regulations require phone numbers to be screened at least every 28 days. PhoneTools tracks this automatically:

- **Phone Screening Last Checked**: Date of last screening
- **Phone Screening Next Due**: When next screening is required
- Use these fields in reports and workflows to stay compliant

### Create a Compliance Report

1. Click **+ New Report**
2. Select object (Contacts, Leads, etc.)
3. Add columns:
   - Name
   - Phone
   - Phone Screening Status
   - Phone Screening Next Due
4. Filter for records where "Next Due" < TODAY
5. Save and schedule

## Using Screening Results

### JSON Output

The Phone Screening Results field contains detailed JSON data for custom development:

```json
{
  "screening_status": "GREEN",
  "tps_status": "NOT_REGISTERED",
  "ctps_status": "NOT_REGISTERED",
  "last_screened": "2026-06-23",
  "next_due": "2026-07-21"
}
```

### Build Workflows

Use screening status to automate your processes:

- Route GREEN numbers to sales queue
- Alert for AMBER results
- Block calls for RED numbers
- Schedule follow-up screening before 28-day limit

## Best Practices

1. **Screen Proactively**: Set up automated screening rather than manual
2. **Monitor Compliance**: Create dashboard showing compliance status
3. **Plan Ahead**: Schedule screenings before the 28-day limit expires
4. **Test First**: Verify setup with test records before full rollout
5. **Document Compliance**: Keep audit trails of screening activities
6. **Handle Errors Gracefully**: Set up error notifications for failed screenings
7. **Optimize Costs**: Use formula fields to screen only records that need it

## Troubleshooting

### Issue: Screening Button Not Appearing

**Solution**: Verify the PhoneTools field has been added to your page layout and user permissions are correct.

### Issue: Slow Batch Screening

**Solution**: Schedule batch operations during off-peak hours. PhoneTools processes records sequentially to maintain API limits.

### Issue: Permission Denied

**Solution**: Ensure your Salesforce user profile has permission to access PhoneTools objects and the Screening Phone Numbers custom action.

### Issue: Incorrect Screening Results

**Solution**: Verify phone numbers include UK country code (+44) or are formatted as UK numbers. DMA updates daily - try screening again.

## Need More Help?

- Visit our [FAQ](faq.md)
- Email: [support@provenworks.com](mailto:support@provenworks.com)
- EMEA Phone: +44 (0)118 321 7405
- US Phone: +1 (484) 258-2918
- [Book a demo](https://calendly.com/phonetools)
