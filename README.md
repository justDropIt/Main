# JustDropIt

## Table of Contents
1. [Overview](#Overview)
1. [Product Spec](#Product-Spec)
1. [Wireframes](#Wireframes)
2. [Schema](#Schema)

## Overview
### Description
JustDropIt is an app that allows you to anonymously post comments about your classes and professors.

### App Evaluation
[Evaluation of your app across the following attributes]
- **Category:** Education, Music, Reference, Social Networking
- **Mobile:** iOS
- **Story:** The app allows university students to choose the right classes to set a strong base for their future. 
- **Market:** University Students
- **Habit:** As a social media application, this app will attract teenagers to gossip about their professors often.
- **Scope:** All students

## Product Spec

### 1. User Stories (Required and Optional)

**Required Must-have Stories**

* Login Screen
* Connect to parse
* Home view
* Search view
* Professor view
* Create view
* User can post
* User can reset

**Optional Nice-to-have Stories**

* Spotify Songs
* Commenting on posts

### 2. Screen Archetypes

* Login Screen
   * Icon and Title
   * Dropdown list of Universities
   * Enter Button
* Home View
   * Table of posts
   * Navbar with Title, Settings and Search icons
   * Posts with Professor, Text, Upvotes and upvotes buttons
* Search View
    * Search bar
    * Table view of professors with create button
* Professor View
    * Professor name
    * Table view with posts
* Create View
    * Professor name
    * Text field
    * Post button

### 3. Navigation

**Tab Navigation** (Tab to Screen)

* Settings tab to settings view
* Search tab to search view
* Name tab to Home view

**Flow Navigation** (Screen to Screen)

* Search view
   * Professor view of selected professor
   * Create view of selected professor

## Wireframes
![](https://i.imgur.com/gnipK6p.jpg)


### [BONUS] Digital Wireframes & Mockups

### [BONUS] Interactive Prototype

## Schema 
### Models

| Property | Type   | Description |
|----------|--------|-----------|
| ObjectId | String | Unique id for the user post |
| Author   |Pointer to User| Name of author |
| Media    | file   | Song that user posts |
| Caption | String | Song caption by author |
| CommentCount | interger |Number of comments made to the post |
| UpVotes | interger |Number of likes on the post |
| DownVotes | interger |Number of dislikes on the post |
| createdAt | DateTime | Date when post was created |

### Networking
<!--- [Add list of network requests by screen ] -->
#### List of network requests by screen 

* Home feed screen:
  * (Read/Get) Query all university name
  
```Swift 
    let queryA = PFQuery(className: “University”)
query.whereKey(“university”, equalTo: currentUniversity)
query.order(byAscending: “Name”)
query.findObjectsInBackground {(schools: [PFObject]?, error: Error?) in
	If let error = error {
		print (error.localizedDescription)
	} else if let schools = schools {
		print(“Successfully retrieved \(school.count) schools.”)
    }
```
  * (Read/Get) Query all professor/faculty names

```Swift
let queryB = PFQuery(className: “Prof”)
query.whereKey(“prof”, equalTo: currentProfessor)
query.order(byAscending: “Name”)
query.findObjectsInBackground {(profs: [PFObject]?, error: Error?) in
	If let error = error {
		print (error.localizedDescription)
	} else if let profs = profs {
		print(“Successfully retrieved \(profs.count) professors.”)
}

```
  *  (Read/Get) Query all the posts under prof/faculty name

```Swift
let queryC = PFQuery(className: “Posts”)
query.whereKey(“prof”, equalTo: currentProfessor)
query.order(byDescending: “createdBy”)
query.findObjectsInBackground {(posts: [PFObject]?, error: Error?) in
	If let error = error {
		print (error.localizedDescription)
	} else if let posts = posts {
		print(“Successfully retrieved \(posts.count) post.”)
}

```
* Create Post screen:
  * Create new post object

```Swift
let post = PFObject(className: Posts)
post[“post”] = “Hi”
post[“author”] = “User123456789”
post[“CreatedBy”] = “Mar 5”
post.saveInBackground { (succeeded, error) in
	If (succedded) {
		// the object had been saved.
	} else { 
		// there was problem
}
}

```

<!-- - [Create basic snippets for each Parse network request] -->
- [OPTIONAL: List endpoints if using existing API such as Yelp]
