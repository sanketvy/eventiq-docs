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