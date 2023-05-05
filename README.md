<p align="center">
    <a href="https://github.com/yiisoft" target="_blank">
        <img src="https://avatars0.githubusercontent.com/u/993323" height="100px">
    </a>
    <h1 align="center">Yii2 Google Calendar Api Extension</h1>
    <br>
</p>




Installation
------------

The preferred way to install this extension is through [composer](http://getcomposer.org/download/):

```
composer require --prefer-dist vadgab/yii2-google-calendar-api
```

Basic information
-----------

This application operates with Google Calendar Service Account-based  authentication, meaning the login process happens in the background. It  enables querying, creating, modifying, and deleting calendar-related  events for third-party users without the need for authentication in a  pop-up window.

## Configuration

You will need to create a Service Account in the Google Cloud Console,  to which you must grant the appropriate permissions to access the calendar, as well as a authentication key, which you download and place  for the application to access, and provide the path to it.

![image-20230505121456420](./doc/images\image-20230505121456420.png)

![image-20230505121615217](./doc/images\image-20230505121615217.png)

## Basic Usage 

##### getEvents() - Get event, list

> parameters
>
> - Params (opcional) - full param list : https://developers.google.com/calendar/api/v3/reference/events/list
>
>   

```php
use vadgab\Yii2GoogleCalendar\GoogleCalendar;

$serviceAccount = new GoogleCalendar(
            "your_service_email", 
            "./../your_downloaded_key.json", array(
            "https://www.googleapis.com/auth/calendar",
            "https://www.googleapis.com/auth/calendar.events"
        )
    );        

$serviceAccount->calendarId = "calendarId";  //required
$params = ['timeMin'=>'2020-06-03T10:00:00Z']; //opcional
$serviceAccount->evenId = "eventId"; //opcional
$events = $serviceAccount->getEvents($params);

echo "<pre>"; var_dump($events); echo "</pre>";
```

##### insertEvent() - Add event on your calendar

> ###### parameters
>
> - payload (require) - full param list : https://developers.google.com/calendar/api/v3/reference/events/insert
>
> 

```php
use vadgab\Yii2GoogleCalendar\GoogleCalendar;

$serviceAccount = new GoogleCalendar(
            "your_service_email", 
            "./../your_downloaded_key.json", array(
            "https://www.googleapis.com/auth/calendar",
            "https://www.googleapis.com/auth/calendar.events"
        )
    );        

$serviceAccount->calendarId = "calendarId";  //required
$payload = array(
    'summary' => 'Teszt Event',
    'description' => 'Teszt description',
    'location' => 'Budapest',
    'start' => array('dateTime' => "2023-05-10T10:00:00Z"),
    'end' => array('dateTime' => "2023-05-10T11:00:00Z"),
);
       $events = $serviceAccount->insertEvent($payload);


echo "<pre>";
var_dump($events);
echo "</pre>";

```

> ##### Response
>
> array(18) {
>   ["kind"]=>
>   string(14) "calendar#event"
>   ["etag"]=>
>   string(18) ""************""
>   ["id"]=>
>   string(26) "tme6m9k9g4p0n6sr48693oq4fo"
>   ["status"]=>
>   string(9) "confirmed"
>   ["htmlLink"]=>
>   string(93) "https://www.google.com/calendar/event?eid=*******************************"
>   ["created"]=>
>   string(24) "2023-05-05T11:17:57.000Z"
>   ["updated"]=>
>   string(24) "2023-05-05T11:17:57.483Z"
>   ["summary"]=>
>   string(11) "Teszt Event"
>   ["description"]=>
>   string(17) "Teszt description"
>   ["location"]=>
>   string(8) "Budapest"
>   ["creator"]=>
>   array(1) {
>     ["email"]=>
>     string(75) "**************************"
>   }
>   ["organizer"]=>
>   array(2) {
>     ["email"]=>
>     string(19) "****************"
>     ["self"]=>
>     bool(true)
>   }
>   ["start"]=>
>   array(2) {
>     ["dateTime"]=>
>     string(25) "2023-05-10T12:00:00+02:00"
>     ["timeZone"]=>
>     string(3) "UTC"
>   }
>   ["end"]=>
>   array(2) {
>     ["dateTime"]=>
>     string(25) "2023-05-10T13:00:00+02:00"
>     ["timeZone"]=>
>     string(3) "UTC"
>   }
>   ["iCalUID"]=>
>   string(37) "**************"
>   ["sequence"]=>
>   int(0)
>   ["reminders"]=>
>   array(1) {
>     ["useDefault"]=>
>     bool(true)
>   }
>   ["eventType"]=>
>   string(7) "default"
> }

##### updateEvent() - Add event on your calendar

> ###### parameters
>
> - payload (require) - full param list : https://developers.google.com/calendar/api/v3/reference/events/update
>
> 

```php
use vadgab\Yii2GoogleCalendar\GoogleCalendar;

$serviceAccount = new GoogleCalendar(
            "your_service_email", 
            "./../your_downloaded_key.json", array(
            "https://www.googleapis.com/auth/calendar",
            "https://www.googleapis.com/auth/calendar.events"
        )
    );        

$serviceAccount->calendarId = "calendarId";  //required
$serviceAccount->eventId = "eventId";  //required
$payload = array(
    'summary' => 'Teszt Event update',
    'description' => 'Teszt description update',
    'location' => 'Budapest',
    'start' => array('dateTime' => "2023-05-10T10:00:00Z"),
    'end' => array('dateTime' => "2023-05-10T11:00:00Z"),
);
$events = $serviceAccount->updateEvent($payload);


echo "<pre>";
var_dump($events);
echo "</pre>";

```

> ##### Response
>
> array(18) {
>   ["kind"]=>
>   string(14) "calendar#event"
>   ["etag"]=>
>   string(18) ""************""
>   ["id"]=>
>   string(26) "tme6m9k9g4p0n6sr48693oq4fo"
>   ["status"]=>
>   string(9) "confirmed"
>   ["htmlLink"]=>
>   string(93) "https://www.google.com/calendar/event?eid=*******************************"
>   ["created"]=>
>   string(24) "2023-05-05T11:17:57.000Z"
>   ["updated"]=>
>   string(24) "2023-05-05T11:17:57.483Z"
>   ["summary"]=>
>   string(11) "Teszt Event update"
>   ["description"]=>
>   string(17) "Teszt description update"
>   ["location"]=>
>   string(8) "Budapest"
>   ["creator"]=>
>   array(1) {
>     ["email"]=>
>     string(75) "**************************"
>   }
>   ["organizer"]=>
>   array(2) {
>     ["email"]=>
>     string(19) "****************"
>     ["self"]=>
>     bool(true)
>   }
>   ["start"]=>
>   array(2) {
>     ["dateTime"]=>
>     string(25) "2023-05-10T12:00:00+02:00"
>     ["timeZone"]=>
>     string(3) "UTC"
>   }
>   ["end"]=>
>   array(2) {
>     ["dateTime"]=>
>     string(25) "2023-05-10T13:00:00+02:00"
>     ["timeZone"]=>
>     string(3) "UTC"
>   }
>   ["iCalUID"]=>
>   string(37) "**************"
>   ["sequence"]=>
>   int(0)
>   ["reminders"]=>
>   array(1) {
>     ["useDefault"]=>
>     bool(true)
>   }
>   ["eventType"]=>
>   string(7) "default"
> }

##### deleteEvent() - Delete event on your calendar

```php
use vadgab\Yii2GoogleCalendar\GoogleCalendar;

$serviceAccount = new GoogleCalendar(
            "your_service_email", 
            "./../your_downloaded_key.json", array(
            "https://www.googleapis.com/auth/calendar",
            "https://www.googleapis.com/auth/calendar.events"
        )
    );        

$serviceAccount->calendarId = "calendarId";  //required
$serviceAccount->eventId = "eventId";  //required
$events = $serviceAccount->deleteEvent();


```

##### 
