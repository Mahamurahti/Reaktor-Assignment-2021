# Reaktor-Assignment-2021 
Assignment brief for junior developers 2021.

# My implementation
My goal was to make the app with Vue, since I have just learned it and I'm most comfortable with it.
The running application can be found from https://assignment.muuta.net/. 

# Instructions
Your client is a clothing brand that is looking for a simple web app to use in their warehouses. To do their work
efficiently, the warehouse workers need a fast and simple listing page per product category, where they can check 
simple product and availability information from a single UI. There are three product categories they are interested 
in for now: gloves, facemasks, and beanies. Therefore, you should implement three web pages corresponding to those 
categories that list all the products in a given category. One requirement is to be easily able to switch between 
product categories quickly. You are free to implement any UI you want, as long as it can display multiple products 
at once in a straightforward and explicit listing. At this point, it is not necessary to implement filtering or 
pagination functionality on the page.

The client does not have a ready-made API for this purpose. Instead, they have two different legacy APIs that 
combined can provide the needed information. The legacy APIs are on critical-maintenance-only mode, and thus 
further changes to them are not possible. The client knows the APIs are not excellent, but they are asking you to 
work around any issues in the APIs in your new application. The client has instructed you that both APIs have an internal 
cache of about 5 minutes.

# API documentation

``GET /v2/products/:category`` – Return a listing of products in a given category.

``GET /v2/availability/:manufacturer`` – Return a list of availability info.

The APIs are running at https://bad-api-assignment.reaktor.com/.
