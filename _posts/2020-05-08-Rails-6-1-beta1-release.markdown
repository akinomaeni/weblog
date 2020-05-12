---
layout: post
title: 'Rails 6.1: Horizontal Sharding, Multi-DB Improvements, Strict Loading, Destroy Associations in Background, Error Objects, and more!'
categories: releases
author: eileencodes
published: true
date: 2020-05-08 10:00:00 -05:00
---
The first beta for Rails 6.1 has been released and wow does it have a lot of great stuff! We've been hard at work these past few months implementing improvements to multiple databases, adding support for destroying associations in jobs instead of in memory, turning errors into objects, and so much more.

It's amazing how Rails has grown over the years and while we have some improvements to make to the [onboarding process](https://weblog.rubyonrails.org/2020/5/7/A-May-of-WTFs/), Rails has never been better. The features in this release focus on adding the functionality you need to keep your application up and running for years to come.

Let's look at some of the new functionality:

## Horizontal Sharding

Rails 6.0 provided the ability to functionally partition (multiple partitions, different schemas) your database but wasn't able to support horizontal sharding (same schema, multiple partitions). Rails wasn't able to support horizonal sharding because models in Active Record could only have one connection per-role per-class. This is now fixed and [Eileen M. Uchitelle](https://github.com/eileencodes) worked with [John Crepezzi](https://github.com/seejohnrun) from GitHub to build out this functionality. Check out the [PR](https://github.com/rails/rails/pull/38531)!

## Multi-DB Improvements

In addition to adding horizontal sharding support we added tons of new functionality and improved a lot of internals for multiple databases. [Kyle Thompson](https://github.com/kylekthompson) added support for [database namespaced tasks](https://github.com/rails/rails/pull/38449) like `db:schema:dump:namespace`, `db:schema:load:namespace`, `db:structure:dump:namespace`, and `db:structure:load`. [Jean Boussier](https://github.com/casperisfine) from Shopify improved [connection pool management](https://github.com/rails/rails/pull/37296). [John Crepezzi](https://github.com/seejohnrun) and [Eileen M. Uchitelle](https://github.com/eileencodes) worked on implementing [many](https://github.com/rails/rails/pull/37185) [improvements](https://github.com/rails/rails/pull/37279) [to](https://github.com/rails/rails/pull/38536) [database](https://github.com/rails/rails/pull/38256) [configurations](https://github.com/rails/rails/pull/38029).

## Strict Loading Associations

In addition to all the database and connection management improvements, [Aaron Patterson](https://github.com/tenderlove) and [Eileen M. Uchitelle](https://github.com/eileencodes) added support for [strict loading associations](https://github.com/rails/rails/pull/37400). With this feature you can ensure that all your associations are loaded eagerly and stop N+1's before they happen. [Kevin Deisz](https://github.com/kddeisz) added additional support to [association declarations](https://github.com/rails/rails/pull/38541).

## Destroy Associations Later

Destroy Associations Later adds `ActiveRecord::Base.destroy_later` which tells your application that you want to run `destroy` in a background job. This can help you avoid timeouts in your application. The [implementation](https://github.com/rails/rails/pull/39149) was a group effort - the PR was started by [George Claghorn](https://github.com/georgeclaghorn) from Basecamp, further support added by [Cory Gwin](https://github.com/gwincr11) of GitHub and finalized by [Rafael França](https://github.com/rafaelfranca) from Shopify.

## Error Objects

Active Model's errors are now objects with an interface that allows your application to more easily handle and interact with errors thrown by models. [The feature](https://github.com/rails/rails/pull/32313) was implemented by [lulalala](https://github.com/lulalala) and includes a query interface, enables more precise testing, and access to error details.

## Active Storage Improvements

Active Storage got a nice update in Rails 6.1! You can now configure attachments for service you want to store them in.The [feature](https://github.com/rails/rails/pull/34935) was implemented by [Dmitry Tsepelev](https://github.com/DmitryTsepelev).

Additionally, Rails 6.1 adds support to Active Storage for [permanent URLs for blobs](https://github.com/rails/rails/pull/36729). Implemented by [Peter Zhu](https://github.com/peterzhu2118) from Shopify, this feature allows configuring your attachments to use a private or public URL and ensures that public URLs will always use a permanent URL.


## Peformance Improvements and Bug Fixes!

A release isn't just about the awesome features you get. It's also about fixing bugs, improving performance, and making Rails more stable for everyone. This release includes an improvement that [avoids making a query if `where` passes an empty array](https://github.com/rails/rails/pull/37266) reported by [Molly Struve](https://github.com/mstruve) and the fix implemented by [John Hawthorn](https://github.com/jhawthorn). [Eileen M. Uchitelle](https://github.com/eileencodes) and [Aaron Patterson](https://github.com/tenderlove) also implemented a [performance improvement](https://github.com/rails/rails/pull/39009) that speeds up `where` queries when we know all the values are an integer.

## The `classic` Autoloader is Deprecated

The `classic` autoloader has served as well since the first Rails release, but there's a new kid in the block and it is going to start its deprecation cycle.

New Rails projects are strongly discouraged from using `classic`, and we recommend that existing projects running on `classic` switch to `zeitwerk` mode when upgrading. Please check the [_Upgrading Ruby on Rails_](https://guides.rubyonrails.org/upgrading_ruby_on_rails.html) guide for tips.


## And more!

There are so many great changes in Rails 6.1. [531](https://contributors.rubyonrails.org/edge/contributors) people made contributions to Rails. Check out the [CHANGELOGS](https://github.com/rails/rails/tree/v6.1.0.beta1) for more details on bug fixes, performance improvements, and other features.

Thank you to everyone who reported a bug, sent a pull request, and helped improve Rails. Rails is better because of your hard work!

We hope you test out Rails 6.1 and love it as much as we do. Please report any bugs to the [Rails issue tracker](https://github.com/rails/rails/issues).
