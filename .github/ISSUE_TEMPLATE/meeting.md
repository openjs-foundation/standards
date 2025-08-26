<% const timezones = [
  'America/Los_Angeles',
  'America/Denver',
  'America/Chicago',
  'America/New_York',
  'Europe/London',
  'Europe/Amsterdam',
  'Europe/Madrid',
  'Europe/Paris',
  'Asia/Shanghai',
  'Asia/Tokyo',
]; %>

## Date/Time

| Timezone | Date/Time |
|----------|-----------|
<%= timezones.map((zone) => {
  const zonedDate = date.toZonedDateTimeISO(zone)
  const formatter = new Intl.DateTimeFormat('en-US', {
    weekday: 'short',
    month: 'short',
    day: '2-digit',
    year: 'numeric',
    hour: '2-digit',
    minute: '2-digit',
    hour12: true,
    timeZone: zone
  })
  const formattedDate = formatter.format(new Date(zonedDate.epochMilliseconds))
  return `| ${zone} | ${formattedDate} |`
}).join('\n') %>

Or in your local time:

- https://www.timeanddate.com/worldclock/fixedtime.html?msg=<%= encodeURIComponent(title) %>&iso=<%= date.toZonedDateTimeISO('UTC').toPlainDateTime().toString().slice(0, 16).replace(/[-:]/g, '') %>&p1=1440&ah=1

## Joining the meeting

- link for participants: <%= meetingLink %>

> [!IMPORTANT]  
> Meeting is recorded

## Agenda

### OpenJS announcements, reminders & FYIs

- Add any project shares, news, FYIs or reminders to share with the community
  
### Liaison reports

- TC39
- TC53
- TC54
- TC55
- Ecma
- W3C AC
- W3C TAG
- W3C WGs
- OSI
- OPA
- Unicode MessageFormat Working Group
- IETF

### [Review open issues & PRs](https://github.com/openjs-foundation/standards/labels/meeting)

Extracted from **<%= agendaLabel %>** labelled issues and pull requests from **<%= owner %>/<%= repo %>** prior to the meeting.

<%= agendaIssues.map((i) => {
  return `* ${i.html_url}`
}).join('\n') %>

- Add issues that need review, assignment, triage, or other clarification

## Opens

- Add any other items

---

Please use the following emoji reactions in this post to indicate your
availability.

- 👍 - Attending
- 👎 - Not attending
- 😕 - Not sure yet
