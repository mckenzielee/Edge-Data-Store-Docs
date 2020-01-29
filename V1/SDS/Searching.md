---
uid: sdsSearching
---

Searching
=====================

You can search text and fields across the Sequential Data Store. This topic covers searching for SdsStreams, SdsTypes, and SdsStreamViews.

Searching for streams
=====================

The search functionality for streams is exposed through the REST API.

The searchable properties are listed in the following table.

| Property          | Searchable  |
|-------------------|-------------|
| Id                | Yes         |
| TypeId            | Yes         |
| Name              | Yes         |
| Description       | Yes         |
| Indexes           | No          |
| InterpolationMode | No          |
| ExtrapolationMode | No          |
| PropertyOverrides | No          |

Searching for streams is possible using the REST API and specifying the optional `query` parameter, as shown here:

```text
GET api/v1/Tenants/default/Namespaces/{namespaceId}/Streams?query={query}&skip={skip}&count={count}
```

The Stream fields valid for search are identified in the fields table located on the [Streams](xref:sdsStreams) page. 

Searching for types
=====================

Similarly, the search functionality for types is exposed through REST API. The query syntax and request parameters are the same. The only difference is the searchable properties differ for types as opposed to streams. Searchable properties are listed in the following table. For more information, see [Types](xref:sdsTypes).

| Property          | Searchable |
|-------------------|------------|
| Id                | Yes        |
| Name              | Yes        |
| Description       | Yes        |
| SdsTypeCode       | No         |
| InterpolationMode | No         |
| ExtrapolationMode | No         |
| Properties        | Yes, with limitations |

Searching for types is also possible using the REST API and specifying the optional `query` parameter, as shown here:

```text
GET api/v1/Tenants/default/Namespaces/{namespaceId}/Types?query={query}&skip={skip}&count={count}
```

The Type fields valid for search are identified in the fields table located on the [Types](xref:sdsTypes) page. The Properties field is identified as being searchable but with limitations: Each SdsTypeProperty of a given SdsType has its name and Id included in the Properties field. This includes nested SdsTypes of the given SdsType. Therefore, the searching of properties will distinguish SdsTypes by their respective lists of relevant SdsTypeProperty Ids and names.

Searching for stream views
=====================

Similarly, the search functionality for stream views is exposed through REST API. The query syntax and the request parameters are the same. The only difference is the resource you are searching on. You can match on different properties for stream views than for streams and types. The searchable properties are listed in the following table. For more information, see [Stream Views](xref:sdsStreamViews).

| Property     | Searchable |
|--------------|------------|
| Id           | Yes        |
| Name         | Yes        |
| Description  | Yes        |
| SourceTypeId | Yes        |
| TargetTypeId | Yes        |
| Properties   | Yes, with limitations |

As previously mentioned, searching for stream views is also possible using the REST API and specifying the optional `query` parameter, as shown here:

```text
GET api/v1/Tenants/default/Namespaces/{namespaceId}/StreamViews?query={query}&skip={skip}&count={count}
```

The Stream View fields valid for search are identified in the fields table located on the [Stream Views](xref:sdsStreamViews) page. The Properties field is identified as being searchable with limitations because SdsStreamViewProperty objects are not searchable. Only the SdsStreamViewProperty's SdsStreamView is searchable by its Id, SourceTypeId, and TargetTypeId, which are used to return the top level SdsStreamView object when searching. This includes nested SdsStreamViewProperties.

How searching works
=====================

By default, the query parameter is applied across all searchable fields of objects that are searched.

For example, you can assume that a namespace contains the following streams:

**streamId** | **Name**  | **Description**
------------ | --------- | ----------------
stream1      | tempA     | The temperature from DeviceA
stream2      | pressureA | The pressure from DeviceA
stream3      | calcA     | calculation from DeviceA values

Using the stream data above, the following table shows the results of a call to get streams with different ``Query`` values:

**QueryString**     | **Streams returned**
------------------  | ----------------------------------------
``temperature``     | Only stream1 returned.
``calc*``           | Only stream3 returned.
``DeviceA*``        | All three streams returned.
``humidity*``       | No streams returned.

The ``skip`` and ``count`` parameters determine which items are returned when a large number of them match the ``query`` criteria. ``count`` indicates the maximum number of items returned. The maximum value of the ``count`` parameter is 1000. ``skip`` indicates the number of matched items to skip over before returning matching items. You use the skip parameter when more items match the search criteria than can be returned in a single call.

The ``orderby`` parameter is supported for searching both streams and types. It returns the result in sorted order.
The default value for ``orderby`` parameter is ascending order. You can change it to descending order by specifying ``desc`` alongside the orderby field value. It can be used in conjunction with ``query``, ``skip``, and ``count`` parameters.

**Request**
The following examples show various ways to use the ``orderby`` parameter.

```text
GET api/v1/Tenants/default/Namespaces/{namespaceId}/Streams?query=name:pump name:pressure&orderby=name

GET api/v1/Tenants/default/Namespaces/{namespaceId}/Streams?query=name:pump name:pressure&orderby=id asc

GET api/v1/Tenants/default/Namespaces/{namespaceId}/Streams?query=name:pump name:pressure&orderby=name desc

GET api/v1/Tenants/default/Namespaces/{namespaceId}/Streams?query=name:pump name:pressure&orderby=name desc&skip=10&count=20
 ```

Search operators
=====================

You can specify search operators in the ``query`` string to return more specific search results.

Operators | Description
----------|-------------------------------------------------------------------
``AND`` | AND operator. For example, ``cat AND dog`` searches for streams containing both "cat" and "dog".  AND must be in all caps.
``OR``  | OR operator. For example, ``cat OR dog`` searches for streams containing either "cat" or "dog" or both.  OR must be in all caps.
``NOT`` | NOT operator. For example, ``cat NOT dog`` searches for streams that have the "cat" term or do not have "dog".  NOT must be in all caps.
``*``   | Wildcard operator. For example, ``cat*`` searches for streams that have a term that starts with "cat", ignoring case.
``:``   | Field-scoped query.  For example, ``id:stream*`` will search for streams where the ``id`` field starts with "stream", but will not search on other fields like ``name`` or ``description``.  **Note:** Field names are camel case and are case sensitive.
``( )`` | Precedence operator. For example, ``motel AND (wifi OR luxury)`` searches for streams containing motel and either wifi or luxury (or both).

**Note:** Regarding wildcard operator ``*``, you can use the wildcard ``*`` only once for each search term, except for the case of a Contains type query clause. In that case, two wildcards are allowed: one as prefix and one as suffix for example, ``*Tank*`` is valid but ``*Ta*nk``, ``Ta*nk*``, and ``*Ta*nk*`` are not supported. The wildcard ``*`` only works when specifying a single search term. For example, you can search for ``Tank*``, ``*Tank``, ``Ta*nk`` but not ``Tank Meter*``.

**: Operator**
---------------

You can determine which fields are searched by using the following syntax:

```text
fieldname:fieldvalue
```

**Request**
The following examples shows the ``':'`` operator.

```text
GET api/v1/Tenants/default/Namespaces/{namespaceId}/Streams?query=name:pump name:pressure
```

**\* Operator**
-----------------

  You can use the ``'*'`` character as a wildcard to specify an incomplete string.
**Query string**     | **Matches field value** | **Does not match field value**
------------------ | --------------------------------- | -----------------------------
``log*`` | log<br>logger | analog
``*log`` | analog<br>alog | logg
``*log*`` | analog<br>alogger | lop
``l*g`` | log<br>logg | lop

  **Supported**     | **Not Supported**
------------------ | ----------------------------------------
``*``<br>``*log``<br>``l*g``<br>``log*``<br>``*log*``	| ``*l*g*``<br>``*l*g``<br>``l*g*``

  **Request**
The following examples shows the ``'*'`` operator.

```text
GET api/v1/Tenants/default/Namespaces/{namespaceId}/Streams?query=log*
```

Other operators examples
---------------------

**Query string**     | **Matches field value** | **Does not match field value**
------------------ | --------------------------------- | -----------------------------
``mud AND log`` | log mud<br>mud log | mud<br>log
``mud OR log`` | log mud<br>mud<br>log |
``mud AND (NOT log)`` | mud | mud log
``mud AND (log OR pump*)`` | mud log<br>mud pumps | mud bath
``name:stream* AND (description:pressure OR description:pump)`` | The name starts with "stream" and the description includes either term "pressure" or term "pump" |
