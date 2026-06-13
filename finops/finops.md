# Choozle FinOps

Financial operations guidance for managing Choozle API and platform spend.

## Pricing Model

Choozle operates on a **prepaid account balance** model with a monthly subscription fee:

| Component | Cost |
|-----------|------|
| Platform Subscription | Starting at $99/month |
| Media Costs | Variable (billed from account balance) |
| Data Targeting Costs | Variable (charged per campaign use) |
| Ad Serving Costs | Variable (included in media fees) |
| Third-Party Tool Costs | Variable (60+ data provider access) |
| Optimization Fees | Variable |
| Managed Service Fee | 10% of campaign spend (optional) |

## Account Balance Management

- **Minimum Recommended Balance:** $500
- **Billing Currency:** U.S. dollars
- **Auto-Refill:** Configure auto-refill triggers to avoid campaign suspension
- **Campaign Suspension Threshold:** Campaigns pause automatically if balance is insufficient for 24+ hours
- **Prepayment Requirement:** Account balance must be funded before campaigns go live

## Cost Controls

### Budget Allocation
- Set per-campaign and per-ad-group budget caps
- Use campaign scheduling to limit spend windows
- Real-time pacing metrics (spend, impressions, CPM, CPA) available in dashboard and via API

### Data Costs
- 60+ third-party data providers with variable CPM premiums
- First-party data via LiveRamp integration reduces dependency on paid data
- Private marketplace deals (10,000+ available) may offer more predictable CPMs

### API Cost Considerations
- No per-API-call charges documented; API access is included in platform subscription
- Reporting API (`/api/reports`) does not incur additional fees beyond subscription
- Third-party integration tools (e.g., Improvado, Fivetran) may have separate licensing costs

## Optimization Recommendations

1. **Use AI Optimization:** Platform's ten-dimension AI optimization helps shift spend toward high-performing inventory, improving ROAS
2. **Monitor Pacing Daily:** Use the Reporting API to pull daily spend data and compare against budget pacing targets
3. **Leverage First-Party Data:** Onboard CRM/first-party data via LiveRamp to reduce spend on third-party data targeting
4. **Private Marketplace Deals:** Negotiate PMP deals for more cost-predictable, premium inventory
5. **Set Auto-Refill Conservatively:** Set auto-refill triggers at 20-30% of typical monthly spend to avoid over-committing balance

## API-Based Spend Monitoring

Use the Reporting API to programmatically monitor spend:

```
GET https://app.choozle.com/api/reports?account_id={id}&date_start={YYYY-MM-DD}&date_end={YYYY-MM-DD}
```

Key spend metrics returned:
- `spend` — total media spend
- `impressions` — total impressions delivered
- `clicks` — total clicks
- `cpm` — effective CPM
- `cpa` — cost per acquisition
- `cpc` — cost per click

## References

- Choozle Terms of Service: https://choozle.com/terms-of-service/
- Choozle Help Center: https://help.choozle.com/
- Reporting API Documentation: https://app.choozle.com/apidoc/
