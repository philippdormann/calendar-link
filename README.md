# 📅 Calendar Link
### Usage

```js
// Usage with TypeScript or ES6
import { google, outlook, office365, yahoo, ics } from "@philippdormann/calendar-link";

// Set event as an object
const event = {
  title: "My birthday party",
  description: "Be there!",
  start: "2019-12-29 18:00:00 +0100",
  duration: [3, "hour"],
};

// Then fetch the link
google(event); // https://calendar.google.com/calendar/render...
outlook(event); // https://outlook.live.com/owa/...
office365(event); // https://outlook.office.com/owa/...
yahoo(event); // https://calendar.yahoo.com/?v=60&title=...
ics(event); // standard ICS file based on https://icalendar.org
```

### Options

| Property           | Description                 | Allowed values                                                                                                                            |
| ------------------ | --------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------- |
| `title` (required) | Event title                 | String                                                                                                                                    |
| `start` (required) | Start time                  | JS Date / ISO 8601 string / Unix Timestamp                                                                                                |
| `end`              | End time                    | JS Date / ISO 8601 string / Unix Timestamp                                                                                                |
| `duration`         | Event duration              | Array with value (Number) and unit (String)                                                                                               |
| `allDay`           | All day event               | Boolean                                                                                                                                   |
| `rRule`            | Recurring event             | iCal [recurrence rule](https://www.rfc-editor.org/rfc/rfc5545#section-3.3.10) string <br />**NOTE:** Only supported by `google` and `ics` |
| `description`      | Information about the event | String                                                                                                                                    |
| `location`         | Event location in words     | String                                                                                                                                    |
| `busy`             | Mark on calendar as busy?   | Boolean                                                                                                                                   |
| `guests`           | Emails of other guests      | Array of emails (String)                                                                                                                  |
| `url`              | Calendar document URL       | String                                                                                                                                    |

#### Notes

- Any one of the fields `end`, `duration`, or `allDay` is required.
- The allowed units in `duration` are listed here: https://day.js.org/docs/en/durations/creating#list-of-all-available-units.
- The `url` field defaults to `document.URL` if a global `document` object exists. For server-side rendering, you should supply the `url` manually.
Not all calendars support the `guests` and `url` fields.
- If you don't pass the start and end time in UTC, Google will convert it to UTC but Outlook won't, so it's a good idea to use UTC when passing dates and times
