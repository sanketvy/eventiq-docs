# EventIQ - Data Flow


## Payment FLow

### Services Involved :
1. Application client
2. Identity Service
3. Stripe

### Process :
1. EventIQ has to support below three business plans :
   1. FREE - 0$
      1. 1K Monthly Events
      2. 1 Project
      3. Less Realtime Features
   2. PRO - 100$ monthly
      1. 1M Monthly Events
      2. 5 Projects
      3. ALl Realtime Features
   3. ENTERPRISE - 1000$ Monthly
      1. Unlimited Events
      2. Unlimited Projects
      3. All Realtime Features

2. To support this plans, eventIQ maps the users with roles mainly :
   1. FREE_USER
   2. PRO_USER
   3. PREMIUM_USER

3. Based on roles, it is decided which user can avail which services in the system.
4. User when logins first time, is by default on FREE_USER mode. He can evaluate the platform and can create 1 project with 1K events access.
5. Subsequently, user can upgrade the level by moving to Pro or Enterprise plan by paying from settings, and the limits will come in effects afterward.
6. Based on role, we update the maximum projects and events count in the database.


## Analytics Processing Flow:

1. User does some activity in the browser which generates a event by the SDK. The event is then passed to `ingestion-service` which then passes it to `events kafka queue`. 
2. The event is then pulled by `event-worker`, which processes the event using business rules, and then saves the processed event to the database, and it is pushed to `analytics kafka queue`.
3. `analytic-worker` then pulls the processed event from `analytics kafka queue`, and do the processing on the event in realtime.
4. for realtime event processing, we use 5 minute timeframe for aggregating events data. So, for every five minutes we aggregate the data of that project for those 5 minutes in a distributed redis cache. 

## Dashboard Analytics :

### User Analytics on clicking elements :
1. **Event**: `CLICK`
2. **Analytics**: 
   1. Show click by browser
   2. Show click by country
   3. Show click by region
   4. Show number of clicks on different elements by max to min

### User Analytics on page loading :
1. **Event**: `VISIT`
2. **Analytics**: 
   1. Top page visits
   2. page visits by browser
   3. page visits by country
   4. page visits by region

### User Analytics on session start and end :
1. **Event**: `SESSION_START` & `SESSION_END`
2. **Analytics**: 
   1. Number of users starting new session in given timeframe
   2. Number of users ending sessions in a given timeframe
   3. Average users using per minute

### User behaviour with input forms:
1. **Event** : `FORM_INTERACT` & `FORM_SUBMIT`
2. **Analytics**:
   1. Number of users starting form but not ending form.
   2. Form submission Rate.
   3. Form Drop Off Rate.

### Errors faced by users:
1. **Event** : `ERROR`
2. **Analytics** : 
   1. Number of errors total faced by users
   2. Number of errors faced per user
   3. Number of errors faced per browser
   4. Number of errors faced per country

### Referer - Where the users are coming from:
1. **Event** : `REFERER`
2. **Analytics** :
   1. Count per different referer

