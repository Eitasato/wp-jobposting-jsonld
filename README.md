# jobposting_Markup

A WordPress plugin that outputs Google for Jobs structured data (schema.org `JobPosting`, JSON-LD) on job posting pages.

## Scope

This repository contains only the core part of the original implementation: the JSON-LD output.
The original setup also notified Google of new and updated job pages through the Indexing API, triggered by post status changes. That code is not included here.

## How it works

- Hooks into `wp_head` and outputs a JSON-LD script on static pages and single posts of the `introduce` post type.
- Builds the data from the post itself:
  - `title`: post title
  - `description`: post content
  - `datePosted`: post date
- Reads the job location and hiring organization from taxonomies:
  - `category4`: prefecture (`addressRegion`)
  - `introduce_tag`: city (`addressLocality`)
  - `company`: company name, with the term description used as the company URL
- If no company is set, the organization name falls back to `confidential`.
- Registers the `company` taxonomy for the `introduce` post type.

## Requirements

The `introduce` post type and the `category4` and `introduce_tag` taxonomies must be registered by the theme or another plugin.

## Known limitations

- Recommended properties such as `validThrough`, `employmentType`, and `baseSalary` are not output.
- PHP warnings may be logged for posts without a company term. 

