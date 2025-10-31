# Django Interview Refresh

Keep these ORM patterns and framework concepts handy so you can surface Django-specific depth quickly. Pair this with the [Python interview refresh](python.md) for language fundamentals.

## Quick Refresh
- Explain Django’s MTV (Model-Template-View) architecture and request lifecycle.
- Contrast `select_related` vs `prefetch_related` and when to apply each for query optimization.
- Review how Django handles configuration via settings, middleware, and apps.

## Interview Prompts
- **Query optimization:** Discuss how `select_related` joins foreign keys in a single query while `prefetch_related` performs separate queries suited for many-to-many relationships. Show an example where each shines.
- **Authentication & authorization:** Outline the default auth system, custom user models, and per-object permissions.
- **Scaling patterns:** Talk about caching (per-view, per-template, low-level), async support with channels, and background task integration (Celery, RQ).

## Deep Dive Later
- [select_related vs prefetch_related in Django ORM](https://stackoverflow.com/a/31237071/718722) for nuanced query behavior and performance tips.
