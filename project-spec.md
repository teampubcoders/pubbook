# Project name (still required)

## Project idea

LinkedIn/Yelp for pubs, based on NC News

## Why

Pubs/breweries can publicise themselves and network. Can have profile, write articles, arrange events, message each other or customers. Can record beer info.

Customers can keep up-to-date with and rate local/favourite pubs/breweries/beers. Can message pubs and breweries, and each other. Can like/rate/comment/review articles.

# Project specification

## Required classes

Key: @ = unique; ! = non-nullable; % = foreign

### User

- user_id @!
- email @!
- phone !
- password_hash !
- ACL (Jacob can you expand on this please?)
- bio

#### UserBrewery (extends User)

- brewery_name !
- location fields to match whichever postcode API we use (e.g. https://getaddress.io)
- ??? (Jacob!)
- social: website; facebook; instagram; linkedin; pinterest; twitter
- open_to_visitors
- opening times - see questions
- disabled_access
- parking
- other features/facilities?
- rating

#### UserPub (extends User)

- pub_name !
- brewery_id !%
- location fields to match whichever postcode API we use (e.g. https://getaddress.io)
- social: website; facebook; instagram; linkedin; pinterest; twitter
- opening/meal times - see questions
- disabled_access
- parking
- features/facilities - need to figure out what to include/scrape from CAMRA, e.g. real_ale_available; lunchtime_meals; evening_meals; pub_garden; dog_friendly; live_music; wifi etc.
- age_range (???)
- rating

#### UserCustomer (extends User)

- customer_name !
- date_of_birth ! (to make sure over 18 - please, drink responsibly)
- following %
- ??? (Jacob!)

### Drink

- drink_id @!
- drink_name @!
- brewery_id %
- pub_id %
- other???

### Post

- post_id @!
- author !%
- date_posted !
- title !
- body !

#### PostArticle

- headline !
- topic !
- rating
- pictures: picture_url_1...

#### PostComment

- rating
- target_id !%

#### PostEvent

- user_id !%
- headline !
- start_date !
- end_date !
- start_time !
- end_time !
- location !
- open_event !
- invitees %

#### PostReview

- rating
- target_id !%

### Messages

- ???

## Questions

### General

- Should we have any timestamps on objects as a matter of course, or only on articles? E.g. should users and drinks have date_created/date_joined?
- What restrictions should we impose re: picture file type and size for user profiles and articles, or is that more frontend?

### User

- Where should profile pics fit in? Should customers be able to upload multiple profile pics and, if so, how many? Does it make sense for pubs/breweries to have profile pics or do they need to have a different field? I guess we want them to be able to upload several photos of their establishment so again, how many?
- We can infer longitude and latitude of street from postcode; is that enough or can we get it for specific house?
- Should we require customers to record postcode so we know their locale?
- Should customers be able to link their social accounts? If so we should move these to master class.
- Opening times - do we need open_monday, open_tuesday etc. for every day of week, and then open_time_monday, close_time_monday etc? What if they want to record closed for lunch or stuff like that? We'll end up with a shed-load of fields, and then for pubs we'll need to repeat for meal times. Or, is there a simpler way of doing this?
- Do we want 2FA? If not, should customers be able to enter phone number or should it only be on pubs and breweries?
- Jacob - can you expand on fields required for ACL? I can't remember what it stands for.
- CAMRA database (whatpub.com) only shows features/facilities that a pub has, not those it doesn't have - should/how can we scrape the full list?
- How is following going to work?

### Post

- How many pictures should we allow on articles?
- How to make event start/end times unique to specific dates?
- How to manage invitees on events? Reference table for each event?
- If an event isn't at a pub/brewery, we'll need to list facilities/features/restrictions etc.

### Drink

- What info do we want on here?
