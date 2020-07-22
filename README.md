---
description: >-
  The holistic.dev API is organized around REST with JSON request and responses
  and uses standard HTTP response codes.
---

# API Reference \(beta\)

{% hint style="danger" %}
The current **API** status is **BETA**. Minor changes are possible before leaving this status. After fixing the state, JSON-schemas will be published, with a description of the formats of requests and responses
{% endhint %}

## Authentication

The **holistic.dev API** uses API key to authenticate requests. You can view and manage your API key in the Account Settings.

The **holistic.dev APIs** is a REST-based service. Subsequently, all requests to the APIs require this **HTTP header**:

```http
x-api-key: Your API key
```

## Content type

The **holistic.dev APIs** is also a JSON-based service. You have to add **Content-Type** HTTP header to all your requests:

```javascript
Content-Type: application/json
```

## URL and API versioning

Only one API version is operating at this time. Use this base URL for your requests:

> **https://api.holistic.dev/api/v1**

## Responses

All responses are JSON-based and follow one of these formats:

```javascript
// successful response
{
  "status": "OK",
  "data": {...}
  }
}
```

```javascript
// error response
{
  "status": "ERROR",
  "data": {
    "code": <http-code>,
    "message": "<error-message>",
    "details": <mixed-object(optional)>,
  }
}
```

Http codes and error message you can find at **Errors** section

## Projects

The project represents one database. Each project has a **name** and database **type**. Each project can contain **multiple environments** \(development, test, stage, production\) and various version control system **branches**.

{% hint style="warning" %}
**Multiple environment** and **multiple branches** will be avalible soon.
{% endhint %}

### Create project

{% api-method method="post" host="https://api.holistic.dev/api/v1/" path="project" %}
{% api-method-summary %}
project
{% endapi-method-summary %}

{% api-method-description %}
Create new project
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-headers %}
{% api-method-parameter name="x-api-key" type="string" required=true %}
your api key
{% endapi-method-parameter %}
{% endapi-method-headers %}

{% api-method-body-parameters %}
{% api-method-parameter name="project.name" type="string" required=true %}
project name \(case insensitive\)
{% endapi-method-parameter %}

{% api-method-parameter name="project.db" type="string" required=true %}
"pg" only
{% endapi-method-parameter %}
{% endapi-method-body-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}
**project.uuid** - unique project identifier
{% endapi-method-response-example-description %}

```
{
  "status": "OK",
  "data": {
    "project": {
      "date": "2020-01-01T00:00:00.000Z",
      "name": "project name",
      "uuid": "00000000-0000-0000-0000-000000000000"
    }
  }
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

**Example:**

{% tabs %}
{% tab title="JSON" %}
```javascript
{
	"project": {
		"name": "project name",
		"db": "pg"
	}
}
```
{% endtab %}

{% tab title="Bash" %}
```bash
HOLISTICDEV_API_KEY="<your-api-key>" HOLISTICDEV_PROJECT_NAME="<project-name>"; \
echo "{\"project\":{\"name\":\"$HOLISTICDEV_PROJECT_NAME\",\"db\":\"pg\"}}" | \
curl \
  --header "x-api-key: $HOLISTICDEV_API_KEY" \
  --header "Content-Type: application/json" \
  --request POST --data @- https://api.holistic.dev/api/v1/project/
```
{% endtab %}
{% endtabs %}

### Rename project

{% api-method method="patch" host="https://api.holistic.dev/api/v1/" path="project" %}
{% api-method-summary %}
project
{% endapi-method-summary %}

{% api-method-description %}
Create new project
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-headers %}
{% api-method-parameter name="x-api-key" type="string" required=true %}
your api key
{% endapi-method-parameter %}
{% endapi-method-headers %}

{% api-method-body-parameters %}
{% api-method-parameter name="project.name" type="string" required=true %}
project new name \(case insensitive\)
{% endapi-method-parameter %}

{% api-method-parameter name="project.uuid" type="string" required=true %}
existing project UUID
{% endapi-method-parameter %}
{% endapi-method-body-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}
**project.name** - project new name
{% endapi-method-response-example-description %}

```
{
  "status": "OK",
  "data": {
    "project": {
      "name": "project name",
      "uuid": "00000000-0000-0000-0000-000000000000"
    }
  }
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

**Example:**

{% tabs %}
{% tab title="JSON" %}
```javascript
{
	"project": {
		"name": "project name",
		"uuid": "00000000-0000-0000-0000-000000000000"
	}
}
```
{% endtab %}

{% tab title="Bash" %}
```bash
HOLISTICDEV_API_KEY="<your-api-key>" HOLISTICDEV_PROJECT_NAME="<project-name>"; \
echo "{\"project\":{\"name\":\"$HOLISTICDEV_PROJECT_NAME\",\"db\":\"pg\"}}" | \
curl \
  --header "x-api-key: $HOLISTICDEV_API_KEY" \
  --header "Content-Type: application/json" \
  --request PATCH --data @- https://api.holistic.dev/api/v1/project/
```
{% endtab %}
{% endtabs %}

### List projects

{% api-method method="get" host="https://api.holistic.dev/api/v1/" path="project" %}
{% api-method-summary %}
project
{% endapi-method-summary %}

{% api-method-description %}
Get projects list
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-headers %}
{% api-method-parameter name="x-api-key" type="string" required=true %}
your api key
{% endapi-method-parameter %}
{% endapi-method-headers %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}
\*\*\*\*
{% endapi-method-response-example-description %}

```
{
    "data": [
        {
            "ddl": {
                "ast": {
                    "elements": {
                        "comment": 62,
                        "parsed": 31
                    },
                    "errors": 0
                },
                "compiled": {
                    "functions": 0,
                    "operators": 0,
                    "relations": 12,
                    "schemas": 0,
                    "types": 0
                },
                "date": "2020-01-01T00:00:00.000Z",
                "files": 2,
                "issues": 0,
                "uuid": "00000000-0000-0000-0000-000000000000"
            },
            "dml": {
                "count": 1
            },
            "project": {
                "date": "2020-01-01T00:00:00.000Z",
                "db": "pg",
                "name": "default",
                "uuid": "00000000-0000-0000-0000-000000000000"
            }
        }
    ],
    "status": "OK"
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

**Example:**

{% tabs %}
{% tab title="Bash" %}
```bash
HOLISTICDEV_API_KEY="<your-api-key>"; \
curl \
  --header "x-api-key: $HOLISTICDEV_API_KEY" \
  --header "Content-Type: application/json" \
   --request GET https://api.holistic.dev/api/v1/project/
```
{% endtab %}
{% endtabs %}

### Project details

{% api-method method="get" host="https://api.holistic.dev/api/v1/" path="project/:uuid/details" %}
{% api-method-summary %}
project/:uuid/details
{% endapi-method-summary %}

{% api-method-description %}
Get projects list
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-headers %}
{% api-method-parameter name="x-api-key" type="string" required=true %}
your api key
{% endapi-method-parameter %}
{% endapi-method-headers %}

{% api-method-query-parameters %}
{% api-method-parameter name="uuid" type="string" required=true %}
project uuid
{% endapi-method-parameter %}
{% endapi-method-query-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}
\*\*\*\*
{% endapi-method-response-example-description %}

```
{
    "data": {
        "project": {
            "date": "2020-01-01T00:00:00.000Z",
            "db": "pg",
            "name": "default",
            "uuid": "00000000-0000-0000-0000-000000000000"
        }
    },
    "status": "OK"
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

**Example:**

{% tabs %}
{% tab title="Bash" %}
```bash
HOLISTICDEV_API_KEY="<your-api-key>" HOLISTICDEV_PROJECT_UUID="<project-uuid>"; \
curl \
  --header "x-api-key: $HOLISTICDEV_API_KEY" \
  --header "Content-Type: application/json" \
  --request GET "https://api.holistic.dev/api/v1/project/$HOLISTICDEV_PROJECT_UUID/details"
```
{% endtab %}
{% endtabs %}

### Project DDL details

{% api-method method="get" host="https://api.holistic.dev/api/v1/" path="project/:uuid/ddl" %}
{% api-method-summary %}
project/:uuid/ddl
{% endapi-method-summary %}

{% api-method-description %}
Get projects list
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-headers %}
{% api-method-parameter name="x-api-key" type="string" required=true %}
your api key
{% endapi-method-parameter %}
{% endapi-method-headers %}

{% api-method-query-parameters %}
{% api-method-parameter name="uuid" type="string" required=true %}
project uuid
{% endapi-method-parameter %}
{% endapi-method-query-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}
\*\*\*\*
{% endapi-method-response-example-description %}

```
{
    "data": {
        "ddl": {
            "ast": {
                "elements": {
                    "comment": 62,
                    "parsed": 31
                },
                "errors": 0
            },
            "check": {
                "status": "finished"
            },
            "compiled": {
                "functions": 0,
                "operators": 0,
                "relations": 12,
                "schemas": 0,
                "types": 0
            },
            "date": "2020-01-01T00:00:00.000Z",
            "files": 2,
            "issues": 37,
            "uuid": "00000000-0000-0000-0000-000000000000",
            "version": null
        }
    },
    "status": "OK"
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

**Example:**

{% tabs %}
{% tab title="Bash" %}
```bash
HOLISTICDEV_API_KEY="<your-api-key>" HOLISTICDEV_PROJECT_UUID="<project-uuid>"; \
curl \
  --header "x-api-key: $HOLISTICDEV_API_KEY" \
  --header "Content-Type: application/json" \
  --request GET "https://api.holistic.dev/api/v1/project/$HOLISTICDEV_PROJECT_UUID/ddl"
```
{% endtab %}
{% endtabs %}

### Project DMLs list

{% api-method method="get" host="https://api.holistic.dev/api/v1/" path="project/:uuid/dml/list" %}
{% api-method-summary %}
project/:uuid/dml/list
{% endapi-method-summary %}

{% api-method-description %}
Get projects list
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-headers %}
{% api-method-parameter name="x-api-key" type="string" required=true %}
your api key
{% endapi-method-parameter %}
{% endapi-method-headers %}

{% api-method-query-parameters %}
{% api-method-parameter name="uuid" type="string" required=true %}
project uuid
{% endapi-method-parameter %}
{% endapi-method-query-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}
\*\*\*\*
{% endapi-method-response-example-description %}

```
{
    "data": [
        {
            "dml": {
                "check": {
                    "status": "finished"
                },
                "date": "booking-info.sql",
                "issues": 0,
                "name": "sql-name",
                "source": {
                    "from": "api",
                    "sql": "SELECT   \n  b.book_ref,\n  t.ticket_no,\n  t.passenger_id,\n  t.passenger_name,\n  tf.fare_conditions,\n  tf.amount,\n  f.scheduled_departure_local,\n  f.scheduled_arrival_local,\n  f.departure_city || '(' || f.departure_airport || ')' as departure,\n  f.arrival_city || '(' || f.arrival_airport || ')' as arrival,\n  f.status,\n  bp.seat_no\nFROM\n  bookings b\n  JOIN tickets t ON b.book_ref = t.book_ref\n  JOIN ticket_flights tf ON tf.ticket_no = t.ticket_no\n  JOIN flights_v f ON tf.flight_id = f.flight_id\n  LEFT JOIN boarding_passes bp ON tf.flight_id = bp.flight_id AND tf.ticket_no = bp.ticket_no\nWHERE\n  b.book_ref = '_QWE12'\nORDER BY\n  t.ticket_no,\n  f.scheduled_departure"
                },
                "uuid": "00000000-0000-0000-0000-000000000000",
                "version": null
            }
        }
    ],
    "status": "OK"
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

**Example:**

{% tabs %}
{% tab title="Bash" %}
```bash
HOLISTICDEV_API_KEY="<your-api-key>" HOLISTICDEV_PROJECT_UUID="<project-uuid>"; \
curl \
  --header "x-api-key: $HOLISTICDEV_API_KEY" \
  --header "Content-Type: application/json" \
  --request GET "https://api.holistic.dev/api/v1/project/$HOLISTICDEV_PROJECT_UUID/dml/list"
```
{% endtab %}
{% endtabs %}

## DDL

DDL, aka Data Definition Language, is an SQL subset that includes **CREATE**, **ALTER**, and **DROP** statements. It uses to define database structure. Also, can include DML statements with extension's commands like **create\_hypertable\(\)** from [**TimescaleDB**](https://docs.timescale.com/latest/api#create_hypertable). All supported extensions you can find in the [**extensions list**](extensions.md)**.**  
Knowledge about database structure is the critical requirement for SQL-queries static analysis. We require to upload the database structure described in DDL syntax before process any DML queries.

### Extract DDL from database

If you store database schema in your version control system, you can directly upload it for any project. 

{% hint style="info" %}
DDL can contain multiple files, and we store it as is for better navigation.
{% endhint %}

In case you have not DDL synchronized with production database in your version control system, you should extract DDL directly from target database:

{% tabs %}
{% tab title="Bash" %}
```bash
 PGPASSWORD=<pg-password> pg_dump -h <pg-host> -p <pg-port> -U <pg-username> \
 -d <pg-db-name> --schema-only --no-owner --no-privileges --no-security-labels \
 > ddl.sql
```
{% endtab %}
{% endtabs %}

**database parameters:**

* **&lt;pg-password&gt;**
* **&lt;pg-host&gt;**
* **&lt;pg-port&gt;**
* **&lt;pg-username&gt;**
* **&lt;pg-db-name&gt;**

{% hint style="warning" %}
**pg\_dump** utility knows nothing about extension's necessary routines. E.g., commands like **create\_hypertable\(\)** from [**TimescaleDB**](https://docs.timescale.com/latest/api#create_hypertable) you should add by yourself. We recommend storing it in a separate file and upload both.
{% endhint %}

### Upload DDL

{% api-method method="post" host="https://api.holistic.dev/api/v1/" path="ddl" %}
{% api-method-summary %}
ddl
{% endapi-method-summary %}

{% api-method-description %}
Upload brand new ddl or replace existing ddl with new version
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-headers %}
{% api-method-parameter name="x-api-key" type="string" required=true %}
your api key
{% endapi-method-parameter %}
{% endapi-method-headers %}

{% api-method-body-parameters %}
{% api-method-parameter name="project.name" type="string" required=true %}
project name \(case insensitive\)
{% endapi-method-parameter %}

{% api-method-parameter name="ddl.version" type="string" required=true %}
any string version for history navigate \(case insensitive, can be null\)
{% endapi-method-parameter %}

{% api-method-parameter name="files" type="array" required=true %}
array of objects  
{  
    "name": "&lt;filename:**string**&gt;",  
    "source": "&lt;sql-source:**string**&gt;"  
}  
&lt;sql-source:**string**&gt; is base64 encoded or not
{% endapi-method-parameter %}
{% endapi-method-body-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}
**ddl.uuid** - unique ddl identifier
{% endapi-method-response-example-description %}

```javascript
{
  "status": "OK",
  "data": {
    "ddl": {
      "uuid": "00000000-0000-0000-0000-000000000000"
    }
  }
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

**Example:**

{% tabs %}
{% tab title="JSON" %}
```javascript
{
    "project": {
        "name": "default"
    },
    "ddl": {
        "version": null
    },
    "files": [
        {
            "name": "filename-1.sql",
            "source": "CREATE TABLE aircrafts_data (\n    aircraft_code character(3) NOT NULL,\n    model jsonb NOT NULL,\n    range integer NOT NULL,\n    CONSTRAINT aircrafts_range_check CHECK ((range > 0))\n);\n\nCREATE VIEW aircrafts AS\n SELECT ml.aircraft_code,\n    (ml.model ->> lang()) AS model,\n    ml.range\n   FROM aircrafts_data ml;\n\n\n\nCREATE TABLE airports_data (\n    airport_code character(3) NOT NULL,\n    airport_name jsonb NOT NULL,\n    city jsonb NOT NULL,\n    coordinates point NOT NULL,\n    timezone text NOT NULL\n);\n\n\n\nCREATE VIEW airports AS\n SELECT ml.airport_code,\n    (ml.airport_name ->> lang()) AS airport_name,\n    (ml.city ->> lang()) AS city,\n    ml.coordinates,\n    ml.timezone\n   FROM airports_data ml;\n\n\n\nCREATE TABLE boarding_passes (\n    ticket_no character(13) NOT NULL,\n    flight_id integer NOT NULL,\n    boarding_no integer NOT NULL,\n    seat_no character varying(4) NOT NULL\n);"
        },
        {
            "name": "filename-2.sql",
            "source": "CREATE TABLE bookings (\n    book_ref character(6) NOT NULL,\n    book_date timestamp with time zone NOT NULL,\n    total_amount numeric(10,2) NOT NULL\n);\n\n\nCREATE TABLE flights (\n    flight_id integer NOT NULL,\n    flight_no character(6) NOT NULL,\n    scheduled_departure timestamp with time zone NOT NULL,\n    scheduled_arrival timestamp with time zone NOT NULL,\n    departure_airport character(3) NOT NULL,\n    arrival_airport character(3) NOT NULL,\n    status character varying(20) NOT NULL,\n    aircraft_code character(3) NOT NULL,\n    actual_departure timestamp with time zone,\n    actual_arrival timestamp with time zone,\n    CONSTRAINT flights_check CHECK ((scheduled_arrival > scheduled_departure)),\n    CONSTRAINT flights_check1 CHECK (((actual_arrival IS NULL) OR ((actual_departure IS NOT NULL) AND (actual_arrival IS NOT NULL) AND (actual_arrival > actual_departure)))),\n    CONSTRAINT flights_status_check CHECK (((status)::text = ANY (ARRAY[('On Time'::character varying)::text, ('Delayed'::character varying)::text, ('Departed'::character varying)::text, ('Arrived'::character varying)::text, ('Scheduled'::character varying)::text, ('Cancelled'::character varying)::text])))\n);\n\n\nCREATE VIEW flights_v AS\n SELECT f.flight_id,\n    f.flight_no,\n    f.scheduled_departure,\n    timezone(dep.timezone, f.scheduled_departure) AS scheduled_departure_local,\n    f.scheduled_arrival,\n    timezone(arr.timezone, f.scheduled_arrival) AS scheduled_arrival_local,\n    (f.scheduled_arrival - f.scheduled_departure) AS scheduled_duration,\n    f.departure_airport,\n    dep.airport_name AS departure_airport_name,\n    dep.city AS departure_city,\n    f.arrival_airport,\n    arr.airport_name AS arrival_airport_name,\n    arr.city AS arrival_city,\n    f.status,\n    f.aircraft_code,\n    f.actual_departure,\n    timezone(dep.timezone, f.actual_departure) AS actual_departure_local,\n    f.actual_arrival,\n    timezone(arr.timezone, f.actual_arrival) AS actual_arrival_local,\n    (f.actual_arrival - f.actual_departure) AS actual_duration\n   FROM flights f,\n    airports dep,\n    airports arr\n  WHERE ((f.departure_airport = dep.airport_code) AND (f.arrival_airport = arr.airport_code));\n\n\n\nCREATE VIEW routes AS\n WITH f3 AS (\n         SELECT f2.flight_no,\n            f2.departure_airport,\n            f2.arrival_airport,\n            f2.aircraft_code,\n            f2.duration,\n            array_agg(f2.days_of_week) AS days_of_week\n           FROM ( SELECT f1.flight_no,\n                    f1.departure_airport,\n                    f1.arrival_airport,\n                    f1.aircraft_code,\n                    f1.duration,\n                    f1.days_of_week\n                   FROM ( SELECT flights.flight_no,\n                            flights.departure_airport,\n                            flights.arrival_airport,\n                            flights.aircraft_code,\n                            (flights.scheduled_arrival - flights.scheduled_departure) AS duration,\n                            (to_char(flights.scheduled_departure, 'ID'::text))::integer AS days_of_week\n                           FROM flights) f1\n                  GROUP BY f1.flight_no, f1.departure_airport, f1.arrival_airport, f1.aircraft_code, f1.duration, f1.days_of_week\n                  ORDER BY f1.flight_no, f1.departure_airport, f1.arrival_airport, f1.aircraft_code, f1.duration, f1.days_of_week) f2\n          GROUP BY f2.flight_no, f2.departure_airport, f2.arrival_airport, f2.aircraft_code, f2.duration\n        )\n SELECT f3.flight_no,\n    f3.departure_airport,\n    dep.airport_name AS departure_airport_name,\n    dep.city AS departure_city,\n    f3.arrival_airport,\n    arr.airport_name AS arrival_airport_name,\n    arr.city AS arrival_city,\n    f3.aircraft_code,\n    f3.duration,\n    f3.days_of_week\n   FROM f3,\n    airports dep,\n    airports arr\n  WHERE ((f3.departure_airport = dep.airport_code) AND (f3.arrival_airport = arr.airport_code));\n\n\nCREATE TABLE seats (\n    aircraft_code character(3) NOT NULL,\n    seat_no character varying(4) NOT NULL,\n    fare_conditions character varying(10) NOT NULL,\n    CONSTRAINT seats_fare_conditions_check CHECK (((fare_conditions)::text = ANY (ARRAY[('Economy'::character varying)::text, ('Comfort'::character varying)::text, ('Business'::character varying)::text])))\n);\n\n\nCREATE TABLE ticket_flights (\n    ticket_no character(13) NOT NULL,\n    flight_id integer NOT NULL,\n    fare_conditions character varying(10) NOT NULL,\n    amount numeric(10,2) NOT NULL,\n    CONSTRAINT ticket_flights_amount_check CHECK ((amount >= (0)::numeric)),\n    CONSTRAINT ticket_flights_fare_conditions_check CHECK (((fare_conditions)::text = ANY (ARRAY[('Economy'::character varying)::text, ('Comfort'::character varying)::text, ('Business'::character varying)::text])))\n);\n\n\n\nCREATE TABLE tickets (\n    ticket_no character(13) NOT NULL,\n    book_ref character(6) NOT NULL,\n    passenger_id character varying(20) NOT NULL,\n    passenger_name text NOT NULL,\n    contact_data jsonb\n);\n\n\nALTER TABLE ONLY aircrafts_data\n    ADD CONSTRAINT aircrafts_pkey PRIMARY KEY (aircraft_code);\n\n\nALTER TABLE ONLY airports_data\n    ADD CONSTRAINT airports_data_pkey PRIMARY KEY (airport_code);\n\n\nALTER TABLE ONLY boarding_passes\n    ADD CONSTRAINT boarding_passes_flight_id_boarding_no_key UNIQUE (flight_id, boarding_no);\n\n\nALTER TABLE ONLY boarding_passes\n    ADD CONSTRAINT boarding_passes_flight_id_seat_no_key UNIQUE (flight_id, seat_no);\n\n\nALTER TABLE ONLY boarding_passes\n    ADD CONSTRAINT boarding_passes_pkey PRIMARY KEY (ticket_no, flight_id);\n\nALTER TABLE ONLY bookings\n    ADD CONSTRAINT bookings_pkey PRIMARY KEY (book_ref);\n\n\nALTER TABLE ONLY flights\n    ADD CONSTRAINT flights_flight_no_scheduled_departure_key UNIQUE (flight_no, scheduled_departure);\n\n\nALTER TABLE ONLY flights\n    ADD CONSTRAINT flights_pkey PRIMARY KEY (flight_id);\n\n\nALTER TABLE ONLY seats\n    ADD CONSTRAINT seats_pkey PRIMARY KEY (aircraft_code, seat_no);\n\n\nALTER TABLE ONLY ticket_flights\n    ADD CONSTRAINT ticket_flights_pkey PRIMARY KEY (ticket_no, flight_id);\n\n\nALTER TABLE ONLY tickets\n    ADD CONSTRAINT tickets_pkey PRIMARY KEY (ticket_no);\n\n\nALTER TABLE ONLY boarding_passes\n    ADD CONSTRAINT boarding_passes_ticket_no_fkey FOREIGN KEY (ticket_no, flight_id) REFERENCES ticket_flights(ticket_no, flight_id);\n\nALTER TABLE ONLY flights\n    ADD CONSTRAINT flights_aircraft_code_fkey FOREIGN KEY (aircraft_code) REFERENCES aircrafts_data(aircraft_code);\n\n\nALTER TABLE ONLY flights\n    ADD CONSTRAINT flights_arrival_airport_fkey FOREIGN KEY (arrival_airport) REFERENCES airports_data(airport_code);\n\n\nALTER TABLE ONLY flights\n    ADD CONSTRAINT flights_departure_airport_fkey FOREIGN KEY (departure_airport) REFERENCES airports_data(airport_code);\n\n\nALTER TABLE ONLY seats\n    ADD CONSTRAINT seats_aircraft_code_fkey FOREIGN KEY (aircraft_code) REFERENCES aircrafts_data(aircraft_code) ON DELETE CASCADE;\n\n\nALTER TABLE ONLY ticket_flights\n    ADD CONSTRAINT ticket_flights_flight_id_fkey FOREIGN KEY (flight_id) REFERENCES flights(flight_id);\n\n\nALTER TABLE ONLY ticket_flights\n    ADD CONSTRAINT ticket_flights_ticket_no_fkey FOREIGN KEY (ticket_no) REFERENCES tickets(ticket_no);\n\n\n\nALTER TABLE ONLY tickets\n    ADD CONSTRAINT tickets_book_ref_fkey FOREIGN KEY (book_ref) REFERENCES bookings(book_ref);"
        }
    ]
}
```
{% endtab %}

{% tab title="Bash" %}
```bash
HOLISTICDEV_API_KEY="<your-api-key>" HOLISTICDEV_PROJECT_NAME="<project-name>"; \
DATA=$(cat ddl.sql | base64 -w0)
echo "{\"project\":{\"name\":\"$HOLISTICDEV_PROJECT_NAME\"},\"ddl\":{\"version\":null},\"files\":[{\"name\":\"ddl.sql\",\"source\":\"$DATA\"}]}" | \
curl \
  --header "x-api-key: $HOLISTICDEV_API_KEY" \
  --header "Content-Type: application/json" \
  --request POST --data @- https://api.holistic.dev/api/v1/ddl/
```
{% endtab %}
{% endtabs %}

{% hint style="warning" %}
base64 argument -w0 need to prevent formatting result at Linux-based os
{% endhint %}

{% hint style="warning" %}
All files of the previous version will be replaced, even if their number does not match the number of files of the new version.
{% endhint %}

{% hint style="info" %}
We store the history of all schema changes for future features.
{% endhint %}

## DML

DML, aka Data Manipulation Language, is an SQL subset that includes **SELECT**, **INSERT**, **UPDATE**, and **DELETE** statements.

### Upload DML

{% api-method method="post" host="https://api.holistic.dev/api/v1/" path="dml" %}
{% api-method-summary %}
dml
{% endapi-method-summary %}

{% api-method-description %}
Upload brand new dml or replace existing dml with new version
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-headers %}
{% api-method-parameter name="x-api-key" type="string" required=true %}
your api key
{% endapi-method-parameter %}
{% endapi-method-headers %}

{% api-method-body-parameters %}
{% api-method-parameter name="project.name" type="string" required=true %}
prooject name \(case insensitive\)
{% endapi-method-parameter %}

{% api-method-parameter name="ddl.version" type="string" required=true %}
any string version for history navigate \(case insensitive, can be null\)
{% endapi-method-parameter %}

{% api-method-parameter name="dml" type="object" required=true %}
{  
    "name": "&lt;filename:**string**&gt;",  
    "version:"&lt;version:**string**&gt;"  
    "source": {  
        sql: "&lt;sql-source:**string**&gt;"  
    }  
}  
&lt;version:**string**&gt; can be null  
&lt;sql-source:**string**&gt; is base64 encoded or not
{% endapi-method-parameter %}
{% endapi-method-body-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}
**ddl.uuid** - unique ddl identifier
{% endapi-method-response-example-description %}

```javascript
{
  "status": "OK",
  "data": {
    "ddl": {
      "uuid": "00000000-0000-0000-0000-000000000000"
    }
  }
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

**Example:**

{% tabs %}
{% tab title="JSON" %}
```javascript
{
	"project": {
	    "name": "default"
	},
	"ddl": {
	    "version": null
	 },
	 "dml": {
		"name": "booking-info.sql",
		"version": null,
		"source": {
			"sql": "SELECT   \n  b.book_ref,\n  t.ticket_no,\n  t.passenger_id,\n  t.passenger_name,\n  tf.fare_conditions,\n  tf.amount,\n  f.scheduled_departure_local,\n  f.scheduled_arrival_local,\n  f.departure_city || '(' || f.departure_airport || ')' as departure,\n  f.arrival_city || '(' || f.arrival_airport || ')' as arrival,\n  f.status,\n  bp.seat_no\nFROM\n  bookings b\n  JOIN tickets t ON b.book_ref = t.book_ref\n  JOIN ticket_flights tf ON tf.ticket_no = t.ticket_no\n  JOIN flights_v f ON tf.flight_id = f.flight_id\n  LEFT JOIN boarding_passes bp ON tf.flight_id = bp.flight_id AND tf.ticket_no = bp.ticket_no\nWHERE\n  b.book_ref = '_QWE12'\nORDER BY\n  t.ticket_no,\n  f.scheduled_departure"
		}
	 }
}
```
{% endtab %}

{% tab title="Bash" %}
```bash
HOLISTICDEV_API_KEY="<your-api-key>" HOLISTICDEV_PROJECT_NAME="<project-name>"; \
DATA=$(cat ddl.sql | base64 -w0)
echo "{\"project\":{\"name\":\"$HOLISTICDEV_PROJECT_NAME\"},\"ddl\":{\"version\":null},\"dml\":{\"name\":\"dml.sql\", \"version\": null, \"source\":{ \"sql\":\"$DATA\"}}}" | \
curl \
  --header "x-api-key: $HOLISTICDEV_API_KEY" \
  --header "Content-Type: application/json" \
  --request POST --data @- https://api.holistic.dev/api/v1/dml/
```
{% endtab %}
{% endtabs %}

{% hint style="warning" %}
base64 argument -w0 need to prevent formatting result at Linux-based os
{% endhint %}

{% hint style="info" %}
We store the history of all schema changes for future features.
{% endhint %}

## pg\_stat\_statements

The [**pg\_stat\_statements**](https://www.postgresql.org/docs/current/pgstatstatements.html) module provides a means for tracking execution statistics of all SQL statements executed by a server.

The **holistic.dev API** can process whole pg\_stat\_statements snapshot at one request.

{% hint style="info" %}
Exporting the pg\_stat\_statements content is the most comfortable, most flexible, and secure way to organize the automatic export of SQL-queries from Postgresql. This extension is easy to configure for both on-premise installations and cloud providers: [AWS](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/CHAP_PostgreSQL.html), [GCP](https://cloud.google.com/sql/docs/postgres/extensions#miscellaneous-extensions), [AZURE](https://docs.microsoft.com/en-in/azure/postgresql/concepts-extensions#pg_stat_statements), [ALIBABA CLOUD](https://www.alibabacloud.com/help/doc-detail/52953.htm), [DIGITAL OCEAN](https://www.digitalocean.com/docs/databases/postgresql/resources/supported-extensions/), [YANDEX CLOUD](https://cloud.yandex.com/docs/managed-postgresql/operations/cluster-extensions#postgresql), and others.
{% endhint %}

{% hint style="success" %}
**Privacy**

**pg\_stat\_statements** extension normalizes query entries. Normalization is a process whereby similar queries, typically differing only in their constants \(though the exact rules are somewhat more subtle than that\) are recognized as equivalent, and are tracked as a single entry.  This is particularly useful for non-prepared queries.  
  
The normalization process intercepts constants in SQL statements run by users and replaces them with a placeholder \(identified as a dollar mark with number\).  
  
For this reason, all data values that were used in SQL-statement will be blacked out and will not be visible at holistic.dev  
  
But **normalization** has another side.

When normalizing the parameters of functions and expressions, it is quite often impossible to define the type of result unambiguously. For example, the addition operator has 42 types of its arguments, and the normalized query**`SELECT`**`$1 + $2` can return 20 different response types. Such ambiguity negatively affects the analyzer's accuracy. The result of this will be less accurate analysis results - some rules will not be applied.
{% endhint %}

{% api-method method="post" host="https://api.holistic.dev/api/v1/" path="pg\_stat\_statements" %}
{% api-method-summary %}
pg\_stat\_statements
{% endapi-method-summary %}

{% api-method-description %}
Upload **pg\_stat\_statements** snapshot
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-headers %}
{% api-method-parameter name="x-api-key" type="string" required=true %}
your api key
{% endapi-method-parameter %}
{% endapi-method-headers %}

{% api-method-body-parameters %}
{% api-method-parameter name="pgss" type="string" required=true %}
json string \(base64 encoded or not\)
{% endapi-method-parameter %}

{% api-method-parameter name="project.name" type="string" required=true %}
project name
{% endapi-method-parameter %}
{% endapi-method-body-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}
**pgss.income** - pg\_stat\_statements queries in your request  
**pgss.new** - new queries, which will be analyzed
{% endapi-method-response-example-description %}

```javascript
{
  "status": "OK",
  "data": {
    "pgss": {
      "income": 100,
      "new": 100
    }
  }
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% tabs %}
{% tab title="Bash" %}
```bash
HOLISTICDEV_API_KEY="<your-api-key>" HOLISTICDEV_PROJECT_NAME="<project-name>"; \
PG=$(PGPASSWORD=<pg-password> psql -t -A -h <pg-host> -p <pg-port> -U <pg-username> -d <pg-db-name> -c "SELECT json_agg(u) FROM (SELECT DISTINCT ON (queryid) queryid :: varchar as name, query as source, SUM(calls) :: varchar AS calls, SUM(total_time) :: varchar AS total_time, MIN(min_time) :: varchar AS min_time, MAX(max_time) :: varchar AS max_time, AVG(mean_time) :: varchar AS mean_time, SUM(rows) :: varchar AS rows FROM pg_stat_statements pgss JOIN pg_database pgd ON pgss.dbid = pgd.oid WHERE pgd.datname = current_database() AND queryid IS NOT NULL GROUP BY queryid, query) u" | base64 -w0); \
echo "{\"pgss\":\"$PG\", \"project\":{\"name\":\"$HOLISTICDEV_PROJECT_NAME\"}}" | \
curl \
  --header "x-api-key: $HOLISTICDEV_API_KEY" \
  --header "Content-Type: application/json" \
  --request POST --data @- https://api.holistic.dev/api/v1/pg_stat_statements/
```
{% endtab %}
{% endtabs %}

{% hint style="warning" %}
base64 argument -w0 need to prevent formatting result at Linux-based os
{% endhint %}

**holistic.dev parameters:**

* **&lt;your-api-key&gt;** - your account api key
* **&lt;project-name&gt;** - project name

**database parameters:**

* **&lt;pg-password&gt;**
* **&lt;pg-host&gt;**
* **&lt;pg-port&gt;**
* **&lt;pg-username&gt;**
* **&lt;pg-db-name&gt;**

{% hint style="warning" %}
You need to **upload DDL** \(database schema\) before upload pg\_stat\_statements snapshot!
{% endhint %}

{% hint style="warning" %}
Make sure that the **&lt;pg-username&gt;** has enough permissions to retrieve the query results. If there are problems with the output, the easiest way to fix it is **DROP EXTENSION** and **CREATE EXTENSION** again.
{% endhint %}

{% hint style="info" %}
Query in sample script aggregat
{% endhint %}

## Check Results

After adding DDL or DML source, we try to parse and analyze it. It can take some time, especially for big DDL. Because of these reasons parsing and analyzing doing asynchronous way.   
  
When we ship new parser or analyzer, we rebuild all internal objects and analyze them with new rules.  
  
You can reach check results for the last **DDL** by **project name** or **&lt;ddl-uuid&gt;**.   
**DML** check result can be reached only by **&lt;dml-uuid&gt;**.   
  
All of them have similar results format.  


{% hint style="info" %}
UUID point to exact DDL/DML version, not the last one.
{% endhint %}

{% api-method method="get" host="https://api.holistic.dev/api/v1/" path="ddl/:uuid/check-result/" %}
{% api-method-summary %}
ddl/:uuid/check-result
{% endapi-method-summary %}

{% api-method-description %}

{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-headers %}
{% api-method-parameter name="x-api-key" type="string" required=true %}
your api key
{% endapi-method-parameter %}
{% endapi-method-headers %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```
{
    "data": {
        "ddl": {
            "uuid": "00000000-0000-0000-0000-000000000000"
        },
        "analysis": {
            "ddl": [
                [
                    {
                        "name": "char-type",
                        "description": "Recommended avoid to use a precision specification for CHAR type for column \"aircraft_code\" in relation \"aircrafts_data\"",
                        "location": 1,
                        "position": {
                            "line": 1,
                            "column": 1
                        }
                    }
                ]
            ],
            "dml": [],
            "details": [
                {
                    "kind": [
                        "architect"
                    ],
                    "name": "char-type",
                    "tags": [
                        "CHAR"
                    ],
                    "class": "DDL",
                    "places": [
                        "CREATE MATERIALIZED VIEW",
                        "CREATE TABLE"
                    ],
                    "complexity": {
                        "type": "static",
                        "level": 1,
                        "nested": 0,
                        "multiple": true
                    },
                    "description": {
                        "template": "Recommended avoid to use a precision specification for CHAR type for column \"%columnname%\" in relation \"%relationname%\""
                    }
                }
            ],
            "config": [
                {
                    "char-type": "warning"
                }
            ],
            "statistics": {
                "ddl": {
                    "kind": {
                        "architect": 14,
                        "error": 0,
                        "performance": 13
                    },
                    "total": 25
                },
                "dml": {
                    "kind": {
                        "architect": 30,
                        "error": 0,
                        "performance": 21
                    },
                    "total": 38
                },
                "common": {
                    "kind": {
                        "architect": 7,
                        "error": 0,
                        "performance": 0
                    },
                    "total": 7
                }
            }
        }
    },
    "status": "OK"
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="get" host="https://api.holistic.dev/api/v1/" path="project/:name/ddl/check-result/" %}
{% api-method-summary %}
project/:name/ddl/check-result
{% endapi-method-summary %}

{% api-method-description %}

{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-headers %}
{% api-method-parameter name="x-api-key" type="string" required=true %}
your api key
{% endapi-method-parameter %}
{% endapi-method-headers %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```
{
    "data": {
        "ddl": {
            "uuid": "00000000-0000-0000-0000-000000000000"
        },
        "analysis": {
            "ddl": [
                [
                    {
                        "name": "char-type",
                        "description": "Recommended avoid to use a precision specification for CHAR type for column \"aircraft_code\" in relation \"aircrafts_data\"",
                        "location": 1,
                        "position": {
                            "line": 1,
                            "column": 1
                        }
                    }
                ]
            ],
            "dml": [],
            "details": [
                {
                    "kind": [
                        "architect"
                    ],
                    "name": "char-type",
                    "tags": [
                        "CHAR"
                    ],
                    "class": "DDL",
                    "places": [
                        "CREATE MATERIALIZED VIEW",
                        "CREATE TABLE"
                    ],
                    "complexity": {
                        "type": "static",
                        "level": 1,
                        "nested": 0,
                        "multiple": true
                    },
                    "description": {
                        "template": "Recommended avoid to use a precision specification for CHAR type for column \"%columnname%\" in relation \"%relationname%\""
                    }
                }
            ],
            "config": [
                {
                    "char-type": "warning"
                }
            ],
            "statistics": {
                "ddl": {
                    "kind": {
                        "architect": 14,
                        "error": 0,
                        "performance": 13
                    },
                    "total": 25
                },
                "dml": {
                    "kind": {
                        "architect": 30,
                        "error": 0,
                        "performance": 21
                    },
                    "total": 38
                },
                "common": {
                    "kind": {
                        "architect": 7,
                        "error": 0,
                        "performance": 0
                    },
                    "total": 7
                }
            }
        }
    },
    "status": "OK"
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="get" host="https://api.holistic.dev/api/v1/" path="dml/:uuid/check-result/" %}
{% api-method-summary %}
dml/:uuid/check-result
{% endapi-method-summary %}

{% api-method-description %}

{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-headers %}
{% api-method-parameter name="x-api-key" type="string" required=true %}
your api key
{% endapi-method-parameter %}
{% endapi-method-headers %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```
{
    "data": {
        "dml": {
            "uuid": "00000000-0000-0000-0000-000000000000"
        },
        "analysis": {
            "ddl": [],
            "dml": [],
            "details": [],
            "config": [],
            "statistics": {
                "ddl": {
                    "kind": {
                        "architect": 14,
                        "error": 0,
                        "performance": 13
                    },
                    "total": 25
                },
                "dml": {
                    "kind": {
                        "architect": 30,
                        "error": 0,
                        "performance": 21
                    },
                    "total": 38
                },
                "common": {
                    "kind": {
                        "architect": 7,
                        "error": 0,
                        "performance": 0
                    },
                    "total": 7
                }
            }
        }
    },
    "status": "OK"
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

## Errors

The **holistic.dev API** uses conventional **HTTP response codes** to indicate the success or failure of an API request. In general: Codes in the **2xx** range indicate success. Codes in the **4xx** range indicate an error that failed given the information provided \(e.g., a required parameter was omitted, a charge failed, etc.\). Codes in the **5xx** range indicate an error with holistic.dev's servers.

### Error statuses

* **200 - OK**    Everything worked as expected.
* **400 - Bad Request**    The request was unacceptable, often due to missing a required parameter.
* **401 - Unauthorized**    No valid API key provided.
* **403 - Forbidden**    The API key doesn't have permissions to perform the request.
* **404 - Not Found**    The requested resource doesn't exist.
* **409 - Conflict**    The request conflicts with another request \(perhaps due to using the same idempotent key\).
* **429 - Too Many Requests**    Too many requests hit the API too quickly. We recommend an exponential backoff of your requests.
* **500 - Server Error**     Something went wrong on holistic.dev's end.

### Error response messages

coming soon

