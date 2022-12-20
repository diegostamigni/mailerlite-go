<a href="https://www.mailerlite.com"><img src="https://app.mailerlite.com/assets/images/logo-color.png" width="200px"/></a>

MailerLite Golang SDK

[![MIT licensed](https://img.shields.io/badge/license-MIT-blue.svg)](./LICENSE)

# Table of Contents
- [Installation](#installation)
- [Usage](#usage)
  - [Subscribers](#subscribers)
    - [Get a list of subscribers](#get-a-list-of-subscribers)
    - [Get a single subscriber](#get-a-single-subscriber)
    - [Count all subscribers](#count-all-subscribers)
    - [Create a subscriber](#create-a-subscriber)
    - [Update a subscriber](#update-a-subscriber)
    - [Delete a subscriber](#delete-a-subscriber)
  - [Groups](#groups)
    - [Get a list of groups](#get-a-list-of-groups)
    - [Create a group](#create-a-group)
    - [Update a group](#update-a-group)
    - [Delete a group](#delete-a-group)
    - [Get subscribers belonging to a group](#get-subscribers-belonging-to-a-group)
    - [Assign subscriber to a group](#assign-subscribers-to-a-group)
  - [Segments](#segments)
    - [Get a list of segments](#get-a-list-of-segments)
    - [Update a segment](#update-a-segment)
    - [Delete a segment](#delete-a-segment)
    - [Get subscribers belonging to a segment](#get-subscribers-belonging-to-a-segment)
  - [Fields](#fields)
    - [Get a list of fields](#get-a-list-of-fields)
    - [Create a field](#create-a-field)
    - [Update a field](#update-a-field)
    - [Delete a field](#delete-a-field)
  - [Automations](#automations)
    - [Get a list of automations](#get-a-list-of-automations)
    - [Get an automation](#get-an-automation)
    - [Get subscribers activity for an automation](#get-subscribers-activity-for-an-automation)
  - [Campaigns](#campaigns)
    - [Get a list of campaigns](#get-a-list-of-campaigns)
    - [Get a campaign](#get-a-campaign)
    - [Create a campaign](#update-a-campaign)
    - [Update a campaign](#update-a-campaign)
    - [Schedule a campaign](#schedule-a-campaign)
    - [Cancel a ready campaign](#cancel-a-ready-campaign)
    - [Delete a campaign](#delete-a-campaign)
    - [Get subscribers activity for a campaign](#get-subscribers-activity-for-an-campaign)
  - [Forms](#forms)
    - [Get a list of forms](#get-a-list-of-forms)
    - [Get a form](#get-a-form)
    - [Update a form](#update-a-form)
    - [Delete a form](#delete-a-form)
    - [Get subscribers of a form](#get-subscribers-of-a-form)
  - [Batching](#batching)
    - [Create a new batch](#create-a-new-batch)
  - [Webhooks](#webhooks)
    - [Get a list of webhooks](#get-a-list-of-webhooks)
    - [Get a webhook](#get-a-webhook)
    - [Create a webhook](#update-a-webhook)
    - [Update a webhook](#update-a-webhook)
    - [Delete a webhook](#delete-a-webhook)
  - [Timezones](#timezones)
    - [Get a list of timezones](#get-a-list-of-timezones)
  - [Campaign languages](#languages)
    - [Get a list of languages](#get-a-list-of-languages)
## Subscribers

### Get a list of subscribers

```go
package main

import (
	"context"
	"log"

	"github.com/mailerlite/mailerlite-go"
)

var APIToken = "Api Token Here"

func main() {
	client := mailerlite.NewClient(APIToken)

	ctx := context.TODO()

	listOptions := &mailerlite.ListSubscriberOptions{
		Limit:  200,
		Page:   0, 
		Filters: &[]mailerlite.Filter{{
            Name:  "status",
            Value: "active",
        }},
	}

	subscribers, _, err := client.Subscriber.List(ctx, listOptions)
	if err != nil {
		log.Fatal(err)
	}

	log.Print(subscribers.Meta.Total)
}
```

### Get a single subscriber

```go
package main

import (
	"context"
	"log"

	"github.com/mailerlite/mailerlite-go"
)

var APIToken = "Api Token Here"

func main() {
	client := mailerlite.NewClient(APIToken)

	ctx := context.TODO()

	getOptions := &mailerlite.GetSubscriberOptions{
		ID: 123456789,
		//Email: "client@example.com"
	}

	subscriber, _, err := client.Subscriber.Get(ctx, getOptions)
	if err != nil {
		log.Fatal(err)
	}

	log.Print(subscribers.Data.Email)
}
```

### Count all subscribers

```go
package main

import (
	"context"
	"log"

	"github.com/mailerlite/mailerlite-go"
)

var APIToken = "Api Token Here"

func main() {
	client := mailerlite.NewClient(APIToken)

	ctx := context.TODO()

	count, _, err := client.Subscriber.Count(ctx)
	if err != nil {
		log.Fatal(err)
	}

	log.Print(count.Total)
}
```

### Create a subscriber

```go
package main

import (
	"context"
	"log"

	"github.com/mailerlite/mailerlite-go"
)

var APIToken = "Api Token Here"

func main() {
	client := mailerlite.NewClient(APIToken)

	ctx := context.TODO()

	subscriber := &mailerlite.Subscriber{
		Email: "example@example.com",
		Fields: map[string]interface{}{
			"city": "Vilnius",
		},
	}

	newSubscriber, _, err := client.Subscriber.Create(ctx, subscriber)
	if err != nil {
		log.Fatal(err)
	}

	log.Print(newSubscriber.Data.Email)
}
```

### Update a subscriber

```go
package main

import (
	"context"
	"log"

	"github.com/mailerlite/mailerlite-go"
)

var APIToken = "Api Token Here"

func main() {
	client := mailerlite.NewClient(APIToken)

	ctx := context.TODO()

	subscriber := &mailerlite.Subscriber{
		Email: "example@example.com",
		Fields: map[string]interface{}{
			"company": "MailerLite",
		},
	}

	newSubscriber, _, err := client.Subscriber.Create(ctx, subscriber)
	if err != nil {
		log.Fatal(err)
	}

	log.Print(newSubscriber.Data.Email)
}
```

### Delete a subscriber

```go
package main

import (
	"context"
	"log"

	"github.com/mailerlite/mailerlite-go"
)

var APIToken = "Api Token Here"

func main() {
	client := mailerlite.NewClient(APIToken)

	ctx := context.TODO()

	_, _, err := client.Subscriber.Delete(ctx, "subscriber-id")
	if err != nil {
		log.Fatal(err)
	}

	log.Print("Subscriber Deleted")
}
```

## Groups

### Get a list of groups

```go
package main

import (
	"context"
	"log"

	"github.com/mailerlite/mailerlite-go"
)

var APIToken = "Api Token Here"

func main() {
	client := mailerlite.NewClient(APIToken)

	ctx := context.TODO()

	listOptions := &mailerlite.ListGroupOptions{
		Page:  1,
		Limit: 10,
		Sort: mailerlite.SortByName,
	}

	groups, _, err := client.Group.List(ctx, listOptions)
	if err != nil {
		log.Fatal(err)
	}

	log.Print(groups.Meta.Total)
}
```

### Create a group

```go
package main

import (
	"context"
	"log"

	"github.com/mailerlite/mailerlite-go"
)

var APIToken = "Api Token Here"

func main() {
	client := mailerlite.NewClient(APIToken)

	ctx := context.TODO()

	_, _, err := client.Group.Create(ctx, "group-name")
	if err != nil {
		log.Fatal(err)
	}
}
```

### Update a group

```go
package main

import (
	"context"
	"log"

	"github.com/mailerlite/mailerlite-go"
)

var APIToken = "Api Token Here"

func main() {
	client := mailerlite.NewClient(APIToken)

	ctx := context.TODO()

	_, _, err := client.Group.Update(ctx, "group-id", "Group Name")
	if err != nil {
		log.Fatal(err)
	}
}
```

### Delete a group

```go
package main

import (
	"context"
	"log"

	"github.com/mailerlite/mailerlite-go"
)

var APIToken = "Api Token Here"

func main() {
	client := mailerlite.NewClient(APIToken)

	ctx := context.TODO()

	_, err := client.Group.Delete(ctx, "69861610909337422")
	if err != nil {
		log.Fatal(err)
	}
}
```

### Get subscribers belonging to a group

```go
package main

import (
	"context"
	"log"

	"github.com/mailerlite/mailerlite-go"
)

var APIToken = "Api Token Here"

func main() {
	client := mailerlite.NewClient(APIToken)

	ctx := context.TODO()

	listSubscriberOptions := &mailerlite.ListGroupSubscriberOptions{
		GroupID: "group-id",
		Filters: &[]mailerlite.Filter{{
			Name:  "status",
			Value: "active",
		}},
	}
		
	subscribers, _, err := client.Group.Subscribers(ctx, listSubscriberOptions)
	if err != nil {
		log.Fatal(err)
	}

	log.Print(subscribers.Meta.Total)
}
```

### Assign subscriber to a group

```go
package main

import (
	"context"
	"log"

	"github.com/mailerlite/mailerlite-go"
)

var APIToken = "Api Token Here"

func main() {
	client := mailerlite.NewClient(APIToken)

	ctx := context.TODO()

	_, _, err := client.Group.Assign(ctx, "group-id", "subscriber-id")
	if err != nil {
		log.Fatal(err)
	}
}
```

### Unassign subscriber from a group

```go
package main

import (
	"context"
	"log"

	"github.com/mailerlite/mailerlite-go"
)

var APIToken = "Api Token Here"

func main() {
	client := mailerlite.NewClient(APIToken)

	ctx := context.TODO()

	_, _, err := client.Group.UnAssign(ctx, "group-id", "subscriber-id")
	if err != nil {
		log.Fatal(err)
	}
}
```

## Segments

### Get a list of segments

```go
package main

import (
	"context"
	"log"

	"github.com/mailerlite/mailerlite-go"
)

var APIToken = "Api Token Here"

func main() {
	client := mailerlite.NewClient(APIToken)

	ctx := context.TODO()

	listOptions := &mailerlite.ListSegmentOptions{
		Page:  1,
		Limit: 10,
	}

	_, _, err := client.Segment.List(ctx, listOptions)
	if err != nil {
		log.Fatal(err)
	}
}
```

### Update a segment

```go
package main

import (
	"context"
	"log"

	"github.com/mailerlite/mailerlite-go"
)

var APIToken = "Api Token Here"

func main() {
	client := mailerlite.NewClient(APIToken)

	ctx := context.TODO()

	_, _, err := client.Segment.Update(ctx, "segment-id", "Segment Name")
	if err != nil {
		log.Fatal(err)
	}
}
```

### Delete a segment

```go
package main

import (
	"context"
	"log"

	"github.com/mailerlite/mailerlite-go"
)

var APIToken = "Api Token Here"

func main() {
	client := mailerlite.NewClient(APIToken)

	ctx := context.TODO()

	_, err := client.Segment.Delete(ctx, "segment-id")
	if err != nil {
		log.Fatal(err)
	}
}
```

### Get subscribers belonging to a segment

```go
package main

import (
	"context"
	"log"

	"github.com/mailerlite/mailerlite-go"
)

var APIToken = "Api Token Here"

func main() {
	client := mailerlite.NewClient(APIToken)

	ctx := context.TODO()

	listSubscriberOptions := &mailerlite.ListSegmentSubscriberOptions{
		SegmentID: "segment-id",
		Filters: &[]mailerlite.Filter{{
			Name:  "status",
			Value: "active",
		}},
	}
	
	_, _, err := client.Segment.Subscribers(ctx, listSubscriberOptions)
	if err != nil {
		log.Fatal(err)
	}
}
```

## Fields

### Get a list of fields

```go
package main

import (
	"context"
	"log"

	"github.com/mailerlite/mailerlite-go"
)

var APIToken = "Api Token Here"

func main() {
	client := mailerlite.NewClient(APIToken)

	ctx := context.TODO()

	listOptions := &mailerlite.ListFieldOptions{
		Page:   1,
		Limit:  10,
		Filters: &[]mailerlite.Filter{{
			Name:  "keyword",
			Value: "name",
		}},
		Sort:   mailerlite.SortByName,
	}
	
	_, _, err := client.Field.List(ctx, listOptions)
	if err != nil {
		log.Fatal(err)
	}
}
```

### Create a field

```go
package main

import (
	"context"
	"log"

	"github.com/mailerlite/mailerlite-go"
)

var APIToken = "Api Token Here"

func main() {
	client := mailerlite.NewClient(APIToken)

	ctx := context.TODO()

	// text, number or data
	_, _, err := client.Field.Create(ctx, "field-name", "field-type")
	if err != nil {
		log.Fatal(err)
	}
}
```

### Update a field

```go
package main

import (
	"context"
	"log"

	"github.com/mailerlite/mailerlite-go"
)

var APIToken = "Api Token Here"

func main() {
	client := mailerlite.NewClient(APIToken)

	ctx := context.TODO()

	_, _, err := client.Field.Update(ctx, "field-id", "Field name")
	if err != nil {
		log.Fatal(err)
	}
}
```

### Delete a field

```go
package main

import (
	"context"
	"log"

	"github.com/mailerlite/mailerlite-go"
)

var APIToken = "Api Token Here"

func main() {
	client := mailerlite.NewClient(APIToken)

	ctx := context.TODO()

	_, err := client.Field.Delete(ctx, "field-id")
	if err != nil {
		log.Fatal(err)
	}
}
```

## Automations

### Get a list of automations
### Get an automation
### Get subscribers activity for an automation

## Campaigns

### Get a list of campaigns
### Get a campaign
### Create a campaign
### Update a campaign
### Schedule a campaign
### Cancel a ready campaign
### Delete a campaign
### Get subscribers activity for a campaign

## Forms

### Get a list of forms
### Get a form
### Update a form
### Delete a form
### Get subscribers of a form

## Batching

### Create a new batch

## Webhooks

### Get a list of webhooks
### Get a webhook
### Create a webhook
### Update a webhook
### Delete a webhook

## Timezones

### Get a list of timezones

## Campaign languages

### Get a list of languages


# Testing

[pkg/testing](https://golang.org/pkg/testing/)

```
$ go test
```

<a name="support-and-feedback"></a>
# Support and Feedback

In case you find any bugs, submit an issue directly here in GitHub.

You are welcome to create SDK for any other programming language.

If you have any trouble using our API or SDK feel free to contact our support by email [info@mailerlite.com](mailto:info@mailerlite.com)

The official API documentation is at [https://developers.mailerlite.com](https://developers.mailerlite.com)


<a name="license"></a>
# License

[The MIT License (MIT)](LICENSE)
