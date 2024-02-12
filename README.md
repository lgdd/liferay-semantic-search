# Liferay Semantic Search

A Docker Compose setup to start using Semantic Search with Liferay DXP.

## Usage

```
docker compose up -d --build
```

This will start the following services:

- MySQL (8)
- Elasticsearch (8.11.4)
- Liferay DXP (2023.Q4)
- Txtai (latest)
- Kibana (8.11.4)

> MySQL and Kibana are not necessary but nice to have. You could comment those services in the Compose file. For MySQL, don't forget to comment Liferay DXP configuration as well.

Once everything started, you can login into Liferay DXP and start creating supported content for semantic search (see supported asset types in the [docs](https://learn.liferay.com/w/dxp/using-search/liferay-enterprise-search/search-experiences/semantic-search)).

The necessary blueprint and element to execute a semantic search should be already created thanks to the batch client extension (see the [source](liferay/workspace/client-extensions/semantic-search-batch) & the [docs](https://learn.liferay.com/w/dxp/building-applications/client-extensions/batch-client-extensions)).

All you need to do, once you have some content, is to configure your search page and add the blueprint widget configured to use the `Semantic Search Blueprint`. If you want the semantic search to work with the search bar autocomplete feature, you can configure the search bar to use the `Semantic Search Blueprints` intead of the default suggestions.

## For Liferay PaaS

If you want to use this stack on Liferay PaaS, you will need to add the `txtai` folder in the Cloud workspace in order to add a new custom service thanks to the [LCP.json](txtai/LCP.json) file you can find in it.

For Liferay, you need to deploy the [Semantic Search configuration file](liferay\files\osgi\configs\com.liferay.search.experiences.configuration.SemanticSearchConfiguration.config) and activate the feature flag by adding `feature.flag.LPS-122920=true` in the `portal-ext.properties` or by adding the environment variable `LIFERAY_FEATURE_PERIOD_FLAG_PERIOD__UPPERCASEL__UPPERCASEP__UPPERCASES__MINUS__NUMBER1__NUMBER2__NUMBER2__NUMBER9__NUMBER2__NUMBER0_=true`.

## Import Data

If you're looking to import a lot of data, you can find [this repo](https://github.com/lgdd/liferay-stackexchange-importer) that contains a Python script to import Stack Exchange posts as Liferay Message Board entities.