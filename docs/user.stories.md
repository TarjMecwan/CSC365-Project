# User Stories and Exceptions for ShoeMarket

This document outlines the user stories and exceptions/error scenarios for the ShoeMarket e-commerce platform. The user stories detail the primary functions and goals of our users, while the exceptions cover potential error scenarios and our planned responses to ensure a smooth user experience.

## User Stories

User stories describe the interactions and goals of the users within the ShoeMarket platform. They follow the format: As a [persona], I [want to], [so that].

1. As a sneaker enthusiast, I want to filter shoe listings by size, so that I can quickly find shoes that fit me.
2. As a collector, I want to filter by brand and release date, so that I can find specific collectible shoes.
3. As a bargain hunter, I want to sort listings by price, so that I can find the best deals available.

## Exceptions

Exceptions detail the error scenarios we anticipate and how the system is designed to handle them to maintain usability and user satisfaction.

1. Exception: Search/filter yields no results.
 - The system will suggest broadening search criteria and offer to notify the user when products matching their criteria are listed.
2. Exception: A listed item is sold out or no longer available.
 - The listing will be automatically removed or updated, and users who have shown interest will be notified.
3. Exception: User attempts to register with an already used email.
 - The system will inform the user that the email is already in use and suggest they log in or reset their password.