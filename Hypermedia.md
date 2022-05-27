# PostgREST + Hypermedia

This fork of postgrest contains additions for creating hypermedia-centric apps with htmx. There are 3 parts:

1. SQL
2. URLs
3. HTML

## Parts

### SQL

An SQL DB is the foundation/single source of truth for these additions. The structure of the DB determines the structure of everything else.
The DB is manipulated through table/view queries and stored procedures. All of these actions are mapped to URLs.

### URLs

URLs represent all the actions that can be performed on a database. Thanks to PostgREST, URLs are automatically generated and mapped
to various actions depending on the database schema. URLs are used directly through HTML.
 
### HTML Extended

HTML extended with htmx allows users to perform actions on the DB directly from the UI via URLs. HTML maps the data in the DB to something tangible
that the user can interact with and use to change the state of the app. HATEOAS; HTML As The Engine Of Application State.

## Editors

PostgREST + Hypermedia provides editors for creating/editing the 3 parts mentioned above.

Two main editors are the **HTML Template Editor** and the **SQL Editor**. URLs are automatically generated from SQL schema.

### HTML Template Editor

The HTML template editor is where you create HTML templates for tables/views/procedures.
It should work as a normal templating engine with the addition of URL builders and htmx helpers.

URL builders determine whether a URL, usually used for a hx-get/hx-post/etc., maps to a table/view/procedure in the database.

```html
<button hx-get="/films?select=title,directors(id,last_name)" hx-headers='{"Accept":"text/html;template=filmsWithDirectorInfo"}'>
  Click Me
</button>
```

When entering a URL in the template, the editor should **help with building CORRECT URLs**
and **help with choosing a template that maps to the result of that URL**.

- Help With Building Correct URLs
  
  As the user types a URL for hx-get/hx-post/etc. a dropdown should show available table names.
  When adding query params to the URL, specific relation/column information should appear according
  to the parameter name (select, order, etc.) and postgREST URL syntax.
  
- Help With Choosing Templates That Map To The Results Of A URL
  
  The return type of queries will need to be known ahead of time, as well as the names being used in the template.
  Column names should map to field names used in the template (except for scalars or procedure outputs).
  
### SQL Editor

