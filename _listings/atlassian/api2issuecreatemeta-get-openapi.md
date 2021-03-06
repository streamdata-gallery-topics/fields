---
swagger: "2.0"
x-collection-name: Atlassian
x-complete: 0
info:
  title: Jira Cloud API Get create issue meta
  description: |-
    Returns the metadata for creating issues. This includes the available projects, issue types, fields (with information whether those fields are required) and field types. Projects, in which the user does not have permission to create issues, will not be returned.

    The fields in the createmeta response correspond to the fields on the issue's Create screen for the specific project/issuetype. Fields hidden from the screen will not be returned in the createmeta response.

    Fields will only be returned if `expand=projects.issuetypes.fields` is set.

    The results can be filtered by project and/or issue type, controlled by the query parameters.
  termsOfService: http://atlassian.com/terms/
  version: 1.0.0
basePath: /
schemes:
- http
produces:
- application/json
consumes:
- application/json
paths:
  /api/2/field:
    get:
      summary: Get fields
      description: |-
        Returns all issue fields in Jira, both system and custom fields.

        **[Permissions](https://confluence.atlassian.com/x/FQiiLQ) required:** None, however the following rules apply:

        *   Fields that cannot be added to the issue navigator are always returned.
        *   Fields that cannot be placed on an issue screen are always returned.
        *   Fields that depend on global Jira settings are only returned if the setting is enabled. That is, timetracking fields, subtasks, votes, and watches.
        *   For all other fields, this method only returns the fields that the current user has permission to see (that is, the field can be used in at least one project that the user can see).
      operationId: com.atlassian.jira.rest.v2.issue.FieldResource.getFields_get
      x-api-path-slug: api2field-get
      responses:
        200:
          description: OK
      tags:
      - Fields
    post:
      summary: Create custom field
      description: |-
        Creates a custom field.

        **[Permissions](https://confluence.atlassian.com/x/FQiiLQ) required:** _Administer Jira_ global permission.
      operationId: com.atlassian.jira.rest.v2.issue.FieldResource.createCustomField_post
      x-api-path-slug: api2field-post
      responses:
        200:
          description: OK
      tags:
      - Custom
      - Field
  /api/2/screens/{screenId}/availableFields:
    get:
      summary: Get available screen fields
      description: Gets available fields for screen. i.e ones that haven't already
        been added.
      operationId: com.atlassian.jira.rest.v2.issue.ScreensResource.getAvailableScreenFields_get
      x-api-path-slug: api2screensscreenidavailablefields-get
      parameters:
      - in: path
        name: screenId
        description: id of screen
      responses:
        200:
          description: OK
      tags:
      - Available
      - Screen
      - Fields
  /api/2/screens/{screenId}/tabs/{tabId}/fields:
    get:
      summary: Get all screen tab fields
      description: Gets all fields for a given tab
      operationId: com.atlassian.jira.rest.v2.issue.ScreensResource.getAllScreenTabFields_get
      x-api-path-slug: api2screensscreenidtabstabidfields-get
      parameters:
      - in: query
        name: projectKey
        description: the key of the project; this parameter is optional
      - in: path
        name: screenId
        description: id of screen
      - in: path
        name: tabId
        description: id of tab
      responses:
        200:
          description: OK
      tags:
      - Screen
      - Tab
      - Fields
    post:
      summary: Add screen tab field
      description: Adds field to the given tab.
      operationId: com.atlassian.jira.rest.v2.issue.ScreensResource.addScreenTabField_post
      x-api-path-slug: api2screensscreenidtabstabidfields-post
      parameters:
      - in: path
        name: screenId
        description: id of screen
      - in: path
        name: tabId
        description: id of tab
      responses:
        200:
          description: OK
      tags:
      - Screen
      - Tab
      - Field
  /api/2/customFieldOption/{id}:
    get:
      summary: Get custom field option
      description: "Returns a custom field option. For example, an option in a cascading
        select list.  \n  \n**[Permissions](https://developer.atlassian.com/cloud/jira/platform/rest/#permissions)
        required:** None."
      operationId: com.atlassian.jira.rest.v2.issue.customfield.CustomFieldOptionResource.getCustomFieldOption_get
      x-api-path-slug: api2customfieldoptionid-get
      parameters:
      - in: path
        name: id
        description: The ID of the custom field option
      responses:
        200:
          description: OK
      tags:
      - Custom
      - Field
      - Option
  /api/2/field/{fieldKey}/option:
    get:
      summary: Get all issue field options
      description: |-
        Returns all options defined for a select list issue field. A select list issue field is a type of [issue field](https://developer.atlassian.com/cloud/jira/platform/modules/issue-field/) that allows a user to select an value from a list of options.

        **[Permissions](https://confluence.atlassian.com/x/FQiiLQ) required:** _Administer Jira_ global permission. Jira permissions are not required for the app providing the field.
      operationId: com.atlassian.jira.rest.v2.issue.field.IssueFieldOptionResource.getAllIssueFieldOptions_get
      x-api-path-slug: api2fieldfieldkeyoption-get
      parameters:
      - in: path
        name: fieldKey
        description: 'The field key is specified in the following format: **$(app-key)__$(field-key)**'
      - in: query
        name: maxResults
        description: The maximum number of items to return per page
      - in: query
        name: startAt
        description: The starting index of the returned objects
      responses:
        200:
          description: OK
      tags:
      - Issue
      - Field
      - Options
    post:
      summary: Create issue field option
      description: |-
        Creates an option for a select list issue field.

        **[Permissions](https://confluence.atlassian.com/x/FQiiLQ) required:** _Administer Jira_ global permission. Jira permissions are not required for the app providing the field.
      operationId: com.atlassian.jira.rest.v2.issue.field.IssueFieldOptionResource.createIssueFieldOption_post
      x-api-path-slug: api2fieldfieldkeyoption-post
      parameters:
      - in: path
        name: fieldKey
      responses:
        200:
          description: OK
      tags:
      - Issue
      - Field
      - Option
  /api/2/field/{fieldKey}/option/suggestions/edit:
    get:
      summary: Get selectable issue field options
      description: |-
        Returns options defined for a select list issue field that can be viewed and selected by the currently logged in user.

        **[Permissions](https://confluence.atlassian.com/x/FQiiLQ) required:** Permission to access Jira.
      operationId: com.atlassian.jira.rest.v2.issue.field.IssueFieldOptionResource.getSelectableIssueFieldOptions_get
      x-api-path-slug: api2fieldfieldkeyoptionsuggestionsedit-get
      parameters:
      - in: path
        name: fieldKey
        description: 'The field key is specified in the following format: **$(app-key)__$(field-key)**'
      - in: query
        name: maxResults
        description: The maximum number of items to return per page
      - in: query
        name: projectId
        description: Filters the results to options that are only available in the
          specified project
      - in: query
        name: startAt
        description: The starting index of the returned objects
      responses:
        200:
          description: OK
      tags:
      - Selectable
      - Issue
      - Field
      - Options
  /api/2/field/{fieldKey}/option/suggestions/search:
    get:
      summary: Get visible issue field options
      description: |-
        Returns options defined for a select list issue field that can be viewed by the currently logged in user.

        **[Permissions](https://confluence.atlassian.com/x/FQiiLQ) required:** Permission to access Jira.
      operationId: com.atlassian.jira.rest.v2.issue.field.IssueFieldOptionResource.getVisibleIssueFieldOptions_get
      x-api-path-slug: api2fieldfieldkeyoptionsuggestionssearch-get
      parameters:
      - in: path
        name: fieldKey
        description: 'The field key is specified in the following format: **$(app-key)__$(field-key)**'
      - in: query
        name: maxResults
        description: The maximum number of items to return per page
      - in: query
        name: projectId
        description: Filters the results to options that are only available in the
          specified project
      - in: query
        name: startAt
        description: The starting index of the returned objects
      responses:
        200:
          description: OK
      tags:
      - Visible
      - Issue
      - Field
      - Options
  /api/2/field/{fieldKey}/option/{optionId}:
    get:
      summary: Get issue field option
      description: |-
        Returns an option from a select list issue field.

        **[Permissions](https://confluence.atlassian.com/x/FQiiLQ) required:** _Administer Jira_ global permission. Jira permissions are not required for the app providing the field.
      operationId: com.atlassian.jira.rest.v2.issue.field.IssueFieldOptionResource.getIssueFieldOption_get
      x-api-path-slug: api2fieldfieldkeyoptionoptionid-get
      parameters:
      - in: path
        name: fieldKey
        description: 'The field key is specified in the following format: **$(app-key)__$(field-key)**'
      - in: path
        name: optionId
        description: The ID of the option to be returned
      responses:
        200:
          description: OK
      tags:
      - Issue
      - Field
      - Option
    put:
      summary: Update issue field option
      description: |-
        Updates an option for a select list issue field. If the option does not exist, a new option is created.

        **[Permissions](https://confluence.atlassian.com/x/FQiiLQ) required:** _Administer Jira_ global permission. Jira permissions are not required for the app providing the field.
      operationId: com.atlassian.jira.rest.v2.issue.field.IssueFieldOptionResource.updateIssueFieldOption_put
      x-api-path-slug: api2fieldfieldkeyoptionoptionid-put
      parameters:
      - in: path
        name: fieldKey
        description: 'The field key is specified in the following format: **$(app-key)__$(field-key)**'
      - in: path
        name: optionId
        description: The ID of the option to be updated
      responses:
        200:
          description: OK
      tags:
      - Issue
      - Field
      - Option
    delete:
      summary: Delete issue field option
      description: |-
        Deletes an option from a select list issue field.

        **[Permissions](https://confluence.atlassian.com/x/FQiiLQ) required:** _Administer Jira_ global permission. Jira permissions are not required for the app providing the field.
      operationId: com.atlassian.jira.rest.v2.issue.field.IssueFieldOptionResource.deleteIssueFieldOption_delete
      x-api-path-slug: api2fieldfieldkeyoptionoptionid-delete
      parameters:
      - in: path
        name: fieldKey
        description: 'The field key is specified in the following format: **$(app-key)__$(field-key)**'
      - in: path
        name: optionId
        description: The ID of the option to be deleted
      responses:
        200:
          description: OK
      tags:
      - Issue
      - Field
      - Option
  /api/2/field/{fieldKey}/option/{optionId}/issue:
    delete:
      summary: Replace issue field option
      description: |-
        Deselects a select list issue field option in all issues that it has been selected in. A different option can be selected to replace the deselected option. The update can also be limited to a smaller set of issues by using a JQL query.

        This is an [asynchronous method](#async). The response object will contain a link to the long-running task. For example, _https://your-domain.atlassian.net/rest/api/2/task/10127_.

        **[Permissions](https://confluence.atlassian.com/x/FQiiLQ) required:** _Administer Jira_ global permission. Jira permissions are not required for the app providing the field.
      operationId: com.atlassian.jira.rest.v2.issue.field.IssueFieldOptionResource.replaceIssueFieldOption_delete
      x-api-path-slug: api2fieldfieldkeyoptionoptionidissue-delete
      parameters:
      - in: path
        name: fieldKey
        description: 'The field key is specified in the following format: **$(app-key)__$(field-key)**'
      - in: query
        name: jql
        description: A JQL query that specifies the issues to be updated
      - in: path
        name: optionId
        description: The ID of the option to be deselected
      - in: query
        name: replaceWith
        description: The ID of the option that will replace the currently selected
          option
      responses:
        200:
          description: OK
      tags:
      - Replace
      - Issue
      - Field
      - Option
  /api/2/jql/autocompletedata/suggestions:
    get:
      summary: Get field auto complete for query string
      description: Returns auto complete suggestions for JQL search.
      operationId: com.atlassian.jira.rest.v2.search.SearchAutoCompleteResource.getFieldAutoCompleteForQueryString_get
      x-api-path-slug: api2jqlautocompletedatasuggestions-get
      parameters:
      - in: query
        name: fieldName
        description: the field name for which the suggestions are generated
      - in: query
        name: fieldValue
        description: the portion of the field value that has already been provided
          by the user
      - in: query
        name: predicateName
        description: the predicate for which the suggestions are generated
      - in: query
        name: predicateValue
        description: the portion of the predicate value that has already been provided
          by the user
      responses:
        200:
          description: OK
      tags:
      - Field
      - Auto
      - Completequery
      - String
  /api/2/screens/addToDefault/{fieldId}:
    post:
      summary: Add field to default screen
      description: Adds field or custom field to the default tab
      operationId: com.atlassian.jira.rest.v2.issue.ScreensResource.addFieldToDefaultScreen_post
      x-api-path-slug: api2screensaddtodefaultfieldid-post
      parameters:
      - in: path
        name: fieldId
        description: id of field / custom field
      responses:
        200:
          description: OK
      tags:
      - Field
      - To
      - Default
      - Screen
  /api/2/screens/{screenId}/tabs/{tabId}/fields/{id}:
    delete:
      summary: Remove screen tab field
      description: Removes field from given tab
      operationId: com.atlassian.jira.rest.v2.issue.ScreensResource.removeScreenTabField_delete
      x-api-path-slug: api2screensscreenidtabstabidfieldsid-delete
      parameters:
      - in: path
        name: id
      - in: path
        name: screenId
        description: id of screen
      - in: path
        name: tabId
        description: id of tab
      responses:
        200:
          description: OK
      tags:
      - Remove
      - Screen
      - Tab
      - Field
  /api/2/screens/{screenId}/tabs/{tabId}/fields/{id}/move:
    post:
      summary: Move screen tab field
      description: Moves field on the given tab
      operationId: com.atlassian.jira.rest.v2.issue.ScreensResource.moveScreenTabField_post
      x-api-path-slug: api2screensscreenidtabstabidfieldsidmove-post
      parameters:
      - in: path
        name: id
      - in: path
        name: screenId
        description: id of screen
      - in: path
        name: tabId
        description: id of tab
      responses:
        200:
          description: OK
      tags:
      - Move
      - Screen
      - Tab
      - Field
  /api/2/issue/createmeta:
    get:
      summary: Get create issue meta
      description: |-
        Returns the metadata for creating issues. This includes the available projects, issue types, fields (with information whether those fields are required) and field types. Projects, in which the user does not have permission to create issues, will not be returned.

        The fields in the createmeta response correspond to the fields on the issue's Create screen for the specific project/issuetype. Fields hidden from the screen will not be returned in the createmeta response.

        Fields will only be returned if `expand=projects.issuetypes.fields` is set.

        The results can be filtered by project and/or issue type, controlled by the query parameters.
      operationId: com.atlassian.jira.rest.v2.issue.IssueResource.getCreateIssueMeta_get
      x-api-path-slug: api2issuecreatemeta-get
      parameters:
      - in: query
        name: issuetypeIds
        description: Multi-value parameter defining issue type IDs to be used for
          the results filtering
      - in: query
        name: issuetypeNames
        description: Multi-value parameter defining issue type names to be used for
          the results filtering
      - in: query
        name: projectIds
        description: Multi-value parameter defining project IDs to be used for the
          results filtering
      - in: query
        name: projectKeys
        description: Multi-value parameter defining project keys to be used for the
          results filtering
      responses:
        200:
          description: OK
      tags:
      - Create
      - Issue
      - Meta
  /api/2/issue/{issueIdOrKey}/editmeta:
    get:
      summary: Get edit issue meta
      description: |-
        Returns the metadata for editing an issue.

        The fields returned by editmeta resource are the ones shown on the issue's Edit screen. Fields hidden from the screen will not be returned unless `overrideScreenSecurity` parameter is set to true.

        If an issue cannot be edited in Jira because of its workflow status (for example the issue is closed), then no fields will be returned, unless `overrideEditableFlag` is set to true.
      operationId: com.atlassian.jira.rest.v2.issue.IssueResource.getEditIssueMeta_get
      x-api-path-slug: api2issueissueidorkeyeditmeta-get
      parameters:
      - in: path
        name: issueIdOrKey
        description: ID or key of the issue
      - in: query
        name: overrideEditableFlag
        description: Allows retrieving edit metadata for fields in non-editable status
          (jira
      - in: query
        name: overrideScreenSecurity
        description: Allows retrieving edit metadata for the fields hidden on Edit
          screen
      responses:
        200:
          description: OK
      tags:
      - Edit
      - Issue
      - Meta
  /api/2/issue/{issueIdOrKey}/transitions:
    get:
      summary: Get transitions
      description: |-
        Returns a list of transitions available for this issue for the current user.

        Specify `expand=transitions.fields` parameter to retrieve the fields required for a transition together with their types.

        Fields metadata corresponds to the fields available in a transition screen for a particular transition. Fields hidden from the screen will not be returned in the metadata.
      operationId: com.atlassian.jira.rest.v2.issue.IssueResource.getTransitions_get
      x-api-path-slug: api2issueissueidorkeytransitions-get
      parameters:
      - in: path
        name: issueIdOrKey
        description: ID or key of the issue to return transitions for
      - in: query
        name: skipRemoteOnlyCondition
        description: Flag to skip evaluation of {@link RemoteOnlyCondition}
      - in: query
        name: transitionId
      responses:
        200:
          description: OK
      tags:
      - Transitions
  /api/2/issue/{issueIdOrKey}/worklog/{id}:
    put:
      summary: Update worklog
      description: |-
        Updates an existing worklog entry.

        Note that:

        *   Fields possible for editing are: comment, visibility, started, timeSpent and timeSpentSeconds.
        *   Either timeSpent or timeSpentSeconds can be set.
        *   Fields which are not set will not be updated.
        *   For a request to be valid, it has to have at least one field change.
      operationId: com.atlassian.jira.rest.v2.issue.IssueWorklogsResource.updateWorklog_put
      x-api-path-slug: api2issueissueidorkeyworklogid-put
      parameters:
      - in: query
        name: adjustEstimate
        description: (optional) allows you to provide specific instructions to update
          the remaining time estimate of the issue
      - in: query
        name: expand
        description: 'optional comma separated list of parameters to expand: properties
          (provides worklog properties)'
      - in: path
        name: id
        description: id of the worklog to be updated
      - in: path
        name: issueIdOrKey
        description: a string containing the issue id or key the worklog belongs to
      - in: query
        name: newEstimate
        description: (required when new is selected for adjustEstimate) the new value
          for the remaining estimate field
      - in: query
        name: notifyUsers
        description: (optional) whether or not users should be notified by email,
          true by default
      - in: query
        name: overrideEditableFlag
        description: Updates the issue even if the issue is not editable due to being
          in a status with jira
      responses:
        200:
          description: OK
      tags:
      - Worklog
x-streamrank:
  polling_total_time_average: 0
  polling_size_download_average: 0
  streaming_total_time_average: 0
  streaming_size_download_average: 0
  change_yes: 0
  change_no: 0
  time_percentage: 0
  size_percentage: 0
  change_percentage: 0
  last_run: ""
  days_run: 0
  minute_run: 0
---