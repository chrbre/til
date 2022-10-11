# what is the timeseries function

	SELECT ...
  		TIMESERIES integer units
  	...

Use the ``TIMESERIES`` clause to return data as a time series broken out by a specified period of time. Since ``TIMESERIES`` is used to trigger certain charts, there is no default value.

To indicate the time range, use integer units. For example:

- TIMESERIES 1 minute
- TIMESERIES 30 minutes
- TIMESERIES 1 hour
- TIMESERIES 30 seconds

TIMESERIES can be combined with arguments such as ``MAX``, ``AUTO``, and ``SLIDE BY`` to further tailor query results.

See more nrql functions [here](https://docs.newrelic.com/docs/query-your-data/nrql-new-relic-query-language/get-started/nrql-syntax-clauses-functions/)
