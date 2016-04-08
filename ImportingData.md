# Introduction #

This page explains how to import data quality signals (bugs, tests and test results, and code changes) into your Test Analytics project.

Data import consists of two parts:

  1. Configure the data you want imported via Test Analytics
  1. Set up a data import process

## Configure the data you want imported ##

The web frontend of Test Analytics allows you to configure what data you want imported into your project.

## Set up a data import process ##

Data is imported into Test Analytics via an external tool you create and run.  This tool will access your repositories (your TCM, source control repository, or bug tool), grab your project's data, and upload it in a format that Test Analytics understands.

Test Analytics has an API end point that will tell your tool what data it is interested in.  This endpoint is:
> https://test-analytics.appspot.com/api/data

Accessing this URL will emit a configuration XML like the following:

```
<?xml version="1.0" encoding="UTF-8" standalone="no"?>
<TestAnalytics>
  <DataRequests ProjectID="8675309">
    <DataRequest Type="Issue Tracker">
      <Parameter Name="Owner">example</Parameter>
      <Parameter Name="Label">webstore</Parameter>
    </DataRequest>
  </DataRequests>
</TestAnalytics>
```

The example above is telling you that a project is interested in importing data from Issue Tracker, with the parameters specified (with the Owner of 'example' and the Label 'webstore').  Your external data import tool would then connect to Issue Tracker, issue a query to match these issues, and then transmit those issues to Test Analytics.

You upload data via submitting a POST request to the following URL:
> https://test-analytics.appspot.com/api/upload

You will need to post a JSON array containing the data you would like to import.  For example:

```
{
  [
    'bug': {
                'projectId': '8675309',
                'title': 'bug title',
                ...
              }
    ]
}
```

All items must include the projectId for the project you would like the data to belong to.  The following additional fields are supported:

  * bug (fields: bugId, title, path, severity, priority, groups, url, status, statusDate)
  * test (fields: testId, title, tags, url, result, resultDate)
  * checkin (fields: checkinId, summary, directories, url, state, stateDate)