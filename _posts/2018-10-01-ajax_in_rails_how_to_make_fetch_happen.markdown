---
layout: post
title:      "Ajax in Rails: How to make 'fetch' happen."
date:       2018-10-01 16:53:55 +0000
permalink:  ajax_in_rails_how_to_make_fetch_happen
---


For the Jquery/Javascript section of the Flatiron School curriculum, I've been challenged to incorporate Asynchronous Javascript, aka AJAX into a Rails application that I had previously built. 


This application, called Inscape, is essentially a instagram clone focused on providing users access to content that inspires mindfulness. The domain model includes photos, comments and profiles.

The task: I wanted to use the method fetch() on my User Profile Show Page to make an ajax call to the server for all of that given User's photos and then and inject the photo information into the DOM.

### So what is "fetch()" and how does it work?

According to MDN documentation, `.fetch()` is a global window method that “provides an easy, logical way to fetch resources asynchronously across the network.”

The first argument that it requires is the URL where we can find the data or resources we want to request. 

I wanted to request all of  a given user’s photos. 

In order to do so, I needed to get that user’s id which I found I could do if I stored their id in the data property in a button.

On my show page I built a button storing that profiles id as a data attribute between my ERB tags. I also gave that button a class called “js-get-photos” so that I could select that element to attach an event listener to it (more on this later.):

```html
<!-- in profiles/show.html.erb  -->

<button type="button" class="js-get-photos" data-id="<%=@profile.id%>">All Photos</button><br>

```

In my javascript photos.js file I store that profile id in a variable “id” and interpolate it into the url. 
```javascript
function getProfilePhotos(e){
  e.preventDefault();
  const id = e.target.dataset["id"]
  fetch(`/profiles/${id}/photos`)
    .then(response => response.json())
    .then(data => appendPhotosAndHideFeatured(data));
}
```

The fetch api uses javascript promises, which you can find more about [here](https://davidwalsh.name/fetch), to handle the responses. `Then`  allows us as developers to chain together events. We use fetch to make a request THEN pass fetch a function to execute once a response is given back to us. 

Once the photo data response was obtained, I wanted my application to convert that data into Javascript objects. So I built a Photo class constructor which would accept data in the form of JSON. 

The JSON photo data would look like this for each profile’s photos. It would be an array of hashes:

```javascript
[
{
id: 13,
description: "Universe",
title: "3..2..1",
image: "/system/photos/images/000/000/013/original/adam-miller-1053911-unsplash.jpg?1537996909",
created_at: "2018-09-26T21:21:52.250Z",
formatted_date: "Sep 26, 2018",
user: {
id: 3,
email: "test@example.com",
username: "Kim"
},
comments: [
{
id: 9,
content: "hey!",
user: {
id: 3,
email: "text@example.com",
created_at: "2018-09-26T21:16:32.036Z",
updated_at: "2018-09-26T21:16:32.076Z",
provider: "facebook",
uid: "10200678680709549"
},
photo_id: 13,
created_at: "2018-09-26T21:28:19.375Z",
updated_at: "2018-09-26T21:28:19.375Z"
},
{
id: 15,
content: "test",
user: {
id: 2,
email: "sasha@example.com",
created_at: "2018-09-26T21:13:39.662Z",
updated_at: "2018-09-26T21:35:59.591Z",
provider: null,
uid: null
},
photo_id: 13,
created_at: "2018-09-30T20:03:07.491Z",
updated_at: "2018-09-30T20:03:07.491Z"
}
]
```

I built my photo class constructor to take that JSON data and convert those photos into js objects. I also gave my photo class constructor a formatter to display those profile photos.

```javascript
class Photo{
  constructor(photoData){
    this.id = photoData.id;
    this.user_id = photoData.user.id;
    this.user_email = photoData.user.email;
    this.title = photoData.title;
    this.description = photoData.description;
    this.image = photoData.image;
    this.formatted_date = photoData.formatted_date;
    this.comments = photoData.comments.map((commentData) => {
      const comment = new Comment(commentData);
      return comment;
    })
  }
  formatProfilePhoto(){
    return `<div class="box panel panel-default">
      <a href='/profiles/${this.user_id}/photos/${this.id}'>
        <img class="profile-photo" src=${this.image}></a>
      <h2><a href="/profiles/${this.user_id}/photos/{this.id}.html">${this.title}</a></h2>
      <p>${this.formatted_date}</p>
      </div>`
  }
```

I made sure to hook up an event listener to the button on the show page so that when a user clicked on that link, my fetch request would be executed. 

The method prevents the Rails default behavior of rendering another page, takes the profile_id of the user, injects and interpolates it into the URL and uses `.then` to convert the response to JSON. Then it passes the JSON data to another method `#appendPhotosandHideFeatured`, which uses that json Photo data to make javascript objects, selects an empty html DIVwith an id of "all-photos-div" on my profile show page and injects the response data into it:

```javascript
function getProfilePhotos(e){
  e.preventDefault();
  const id = e.target.dataset["id"]
  fetch(`/profiles/${id}/photos`)
    .then(response => response.json())
    .then(data => appendPhotosAndHideFeatured(data));
}


function appendPhotosAndHideFeatured(jsonPhotos){
  if ($("#all-photos-div").is(':empty')){
    $("#featured-photos").contents().hide();
    $(".js-get-photos").text("Featured Photos");
      jsonPhotos.forEach(photoData => {
        let photo = new Photo(photoData);
        $("#all-photos-div").append(photo.formatProfilePhoto());
      });
  } else {
    $("#featured-photos").contents().show();
    $(".js-get-photos").text("All Photos")
    $("#all-photos-div").html('');  
```


Full source code can be found on Github [here](https://github.com/KimGonzales/inscape). 

