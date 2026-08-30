---
name: infront-domain-handoff
description: Guide the onsite handoff of Infront Kosan's company domain, Vercel website, and Microsoft 365 email. Use for preparation, execution, verification, or recovery of this project's domain and email migration; do not use for ordinary website development.
---

# Infront Domain Handoff

Use [the onsite runbook](../../../docs/onsite-domain-email-migration.md) as the source of truth. Read it completely before changing a registrar, DNS, Vercel domain, Microsoft 365 tenant, or Outlook account.

## Intended outcome

- Primary candidate: `infront-kosan.co.jp`, subject to final registrar availability and client approval.
- Website: apex domain and `www` served by the existing Vercel project.
- Email: Microsoft 365 / Exchange Online using the company domain in Outlook.
- Legacy eo mail remains available during a transition period.
- The client company owns every account, recovery method, subscription, and renewal payment.

## Operating rules

1. Begin in assessment mode. Record the existing eo addresses, Outlook versions, mailbox count, storage method, aliases, forwarding, DNS, and account owners.
2. Never request, copy into the repository, commit, or display passwords, recovery codes, payment details, or Microsoft session tokens.
3. Do not purchase a domain, start a paid subscription, edit production DNS, change an MX record, or remove an old account without the client's explicit confirmation at that step.
4. Before any DNS edit, export or screenshot the complete current zone and record its nameservers and TTL values.
5. Do not change MX until every required Microsoft 365 user/mailbox exists and domain ownership has been verified using TXT. A verified domain alone is not permission to cut over mail.
6. Keep website and mail routing separate: Vercel uses web records; Microsoft 365 uses MX/TXT/CNAME records. Preserve unrelated records.
7. Configure SPF, DKIM, and DMARC. Ensure there is only one SPF TXT record at the apex.
8. Test external inbound and outbound mail before declaring success. Test the apex site, `www`, HTTPS, desktop Outlook, and at least one phone.
9. Keep eo mail active for at least the client-approved transition window; recommend one to three months. Do not promise that an address on eo's domain can be transferred to Microsoft 365.
10. If required mailbox information, company authority, account ownership, or rollback data is missing, stop before the relevant mutation and explain exactly what is needed.

## Handoff record

At completion, update the runbook's handoff record without secrets. Record the chosen domain, registrar, account owner, renewal owner/date, Microsoft tenant admin owner, DNS host, Vercel project, mailbox list, cutover time, verification results, legacy-mail end date, and unresolved items.
