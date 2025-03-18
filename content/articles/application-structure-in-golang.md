+++
title = 'Application Structure in Golang'
date = 2025-03-11T07:07:07+01:00
draft = true
+++

- Store - for storing/reading data e.g ./store/postgres ./store/cache

- Domain - modelling the domain e.g ./domain/product ./domain/payment ./domain/order
    - Contains both the models and storage interfaces, so anything that stores this data has a
    clear contract on how to work with it.

- Service - (maybe not required) for more complex/general orchestration that works across multiple
  domains
    - e.g ./service/notification ./service/export ./service/notification

- HTTP - invariably we are running everything through an HTTP server
    - e.g ./http/api ./http/admin ./http/website ./http/middleware

- Worker - background tasks
