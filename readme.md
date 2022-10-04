# ical-chrome #

A tolerant, minimal icalendar parser for Google Chrome
(http://tools.ietf.org/html/rfc5545)

## Install - Node.js ##

ical.js is availble on npm:

    npm install --save ical-chrome

## API ##

    ical.parseICS(str)

## Example 1

Print list of upcoming node conferences (see example.js)

```javascript
'use strict';

const ical = require('ical');
const months = ['Jan', 'Feb', 'Mar', 'Apr', 'May', 'Jun', 'Jul', 'Aug', 'Sep', 'Oct', 'Nov', 'Dec'];

const data = ical.parseICS('--content from ical file--');

for (let k in data) {
  if (data.hasOwnProperty(k)) {
    var ev = data[k];
    if (data[k].type == 'VEVENT') {
      console.log(`${ev.summary} is in ${ev.location} on the ${ev.start.getDate()} of ${months[ev.start.getMonth()]} at ${ev.start.toLocaleTimeString('en-GB')}`);
    }
  }
}
```

## Recurrences and Exceptions

Calendar events with recurrence rules can be significantly more complicated to handle correctly.  There are three parts to handling them:

 1. rrule - the recurrence rule specifying the pattern of recurring dates and times for the event.
 2. recurrences - an optional array of event data that can override specific occurrences of the event.
 3. exdate - an optional array of dates that should be excluded from the recurrence pattern.

See example_rrule.js for an example of handling recurring calendar events.
