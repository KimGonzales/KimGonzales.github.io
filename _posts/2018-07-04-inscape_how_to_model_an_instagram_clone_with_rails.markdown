---
layout: post
title:      "Inscape: How to Model an Instagram Clone with Rails"
date:       2018-07-04 11:36:22 +0000
permalink:  inscape_how_to_model_an_instagram_clone_with_rails
---

### The App!

Inscape is a social networking application built with the MVC Ruby on Rails framework. It was designed to allow Users to sign in, upload and share their favorite images. 


![Imgur](https://i.imgur.com/SCurCn9l.png)

### The Model Associations

I decided to use four models in this application.

1. User 
```
has_many :photos
has_one :profile
has_many comments
```
2. Profile
```
belongs_to :user
has_many :photos, through: :user
```
3. Photo
```
belongs_to :user
has_many :comments
```
4. Comments
```
belongs_to photo
has_many comments
```

### Authentication

In order for users to make an account and sign in, I decided to use the Devise Gem in conjunction with Ominauth Facebook. I followed [this helpful blogpost](https://www.adrianprieto.com/how-to-setup-devise-and-omniauth-for-your-rails-application/) to implement the two together.

### The Photo Model and Uploading Images

In order to let users upload photos to this Rails app, I decided to use the Paperclip Gem. 

The [Paperclip Gem](https://github.com/thoughtbot/paperclip) is a file attachment management libary for ActiveRecord. One of the Class Methods that Paperclip adds is `has_attached_file`.

`#has_attached_file` gives the class it is called on an attribute that maps to a file. 

It takes 2 arguments - a name and an options hash- and returns a Paperclip::Attachment Object which handles the management of that file. 

`hast_attached_file(name, options ={}) => Object`

In order to use it with this project, I dropped `#has_attached_file` in the Photo model and added a Migration to allow users to attach one image file to each Photo instance, like so.

```
#in Photo.rb

class Photo < ApplicationRecord

  has_attached_file :image, styles: { medium: "300x300>", thumb: "100x100>" }, default_url: "/images/:style/missing.png"
  validates_attachment_content_type :image, content_type: /\Aimage\/.*\z/
  validates :image, :title, :description, presence: true
	end

```

Migration to photos table

```
class AddAttachmentImageToPhotos < ActiveRecord::Migration[5.2]
  def self.up
    change_table :photos do |t|
      t.attachment :image
    end
  end

  def self.down
    remove_attachment :photos, :image
  end
end

```

How to upload images in the Photo form in the view using the [Simple Form Gem](https://github.com/plataformatec/simple_form):

```
<%= simple_form for @photo do |f| %>
  <%= f.input :image, as: :file %>
	<%= f.input :title %>
	<%= f.input :description %>
	<%= f.submit %>
	<% end %>

```

![Imgur](https://i.imgur.com/TOZ8nM9l.png)



Now can I use image_tag helpers in my views to render each photo instance image like so!
` image_tag(@photo.image.url)`

![Imgur](https://i.imgur.com/EPNLPHwl.png)


The full application can be found on my [Github](https://github.com/KimGonzales/inscape).






