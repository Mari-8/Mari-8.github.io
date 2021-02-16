---
layout: post
title:      "Reading on Rails"
date:       2021-02-15 22:49:30 -0500
permalink:  reading_on_rails
---


“One learns from books and example only that certain things can be done. Actual learning requires that you do those things.”   – **Frank Herbert**

As I was approaching this project, looking over requirements, and racking My brain for the right idea I found myself going back to the same idea every time. Books! 
I find a lot of joy in books, It is one of the constants I try and keep throughout the rockiness of life. While everyone's motivation to read or to learn may be different, I know many people enjoy them as much, if not more than I do! 

## Models and relationships

I started planning My model relationships and realized I was NOT as comfortable with them as I thought. After some time, and a tinge of confusion I ended up with the following: 

* User
* Discussion
* Comment
* Review
* Bookshelf
* Book 

The relationships stayed very simple, But the requirements state that you need a few has_many, through relationships as well as a many-to-many relationship built using has_many, through. 

My many-to-many ended up being Users and Discussions joined through comments! Here's what that looks like in the app.

```
User 
has_many :entered_discussions, through: :comments, source: :discussion

Discussion 
has_many :users, through: :comments

Comments 
belongs_to :discussion
belongs_to :user
```

I also added another has_many, through to the User model to be sure I met the requirements.

```
has_many :reviewed_books, through: :reviews, source: :review
```

Now, though I would love to get down to the nitty gritty on the entire app there's way too much ground to cover.
Im going to show you around some of my favorite spots and features!

## Adding a book

My favorite part has to be My book finder. I found a gem called 'googlebooks' that acts like a middle man between BookClub and... You guessed it, Google Books! 
I made a class method for Book, called create_from_google_books which takes the user input of a book title

```
def create_from_google_books(user_input)
    results = GoogleBooks.search(user_input)
    book = results.first 
    book = Book.create(title: book.title, author_name: book.authors, image_url: book.image_link, description: book.description)
end
```

The method uses 'googlebooks' to send the query, sets the book variable to the first result, and creates a new instance of a book using that information. 
Here's a peek inside the books#create action.

```
 if params[:commit] == "Search" 
       book = Book.new.create_from_google_books(params[:book][:title])
       book.user_id = current_user.id
       book.bookshelf_id = params[:book][:bookshelf_id]
 else 
       book = Book.create(book_params)
       book.user_id = current_user.id 
       book.bookshelf_id = params[:book][:bookshelf_id]
 end 
```

When the user hits the "Create book" button on the new book form,  the first thing our create action does is check to see if the input came from the "search for a book" feature, or if the user created a new book manually. If the user searched for the book, we ask that nifty class method above to create the book. If it was a manual creation, we just use rails strong params to create the object instead. 

## Nested routes

When we learned about nested routes, I loved the idea. Seeing that it was a requirement made no difference to me, I was trying it no-matter-what!
The main nested route I ended up with, was between bookshelves and books. The main route was the new book route for a specific shelf, which ends up as: 

`/bookshelves/:id/books/new`

This goes about the process the same as adding any book, except it's building it for that specific shelf without having to manually choose the shelf to fetch the id. The nesting process is simple enough, I'll show you what it looks like using the previous bookshelf example: 

```
resources :bookshelves, only: [:show, :index] do
    resources :books, only: [:show, :index, :new]
end
```

This code gives you access to that nested "new" route, as well as a show and index route for books within shelves. It's a great, simple way to be much more specific about where your routes take you and access specific information through that nested resource. 

## Flash and authorization patterns

Instead of wrapping my fields in a "Fields-with-errors" I went with flash again, It makes it so easy to display not only errors but any message to the user. 
I split this up into two different types of flash messages, "Alert" and "Notice". I used notice for any normal information I needed the user to see. Small things, like "Bookshelf created successfully!". 
Alert was for errors or trying to access something that a user cant access, like other users accounts, bookshelves, or discussions. 
To make sure it always displayed on top of the page, I added them to the layout which is used app-wide:

```
<% if notice %>
    <%= notice %
<% end %>

<% if alert %>
    <%= alert %>
<% end %>
```

That's it! Now any time there is an alert, or notice it automatically shows on the top of the page one time, and then clears out as soon as anything else is done on the page (HTTP is stateless, so every new request is new and fresh) 
The pattern I used for authorization is the same throughout the controllers, I made some helper methods for books, shelves, reviews, discussions, basically anything a user can access and used this to check (with an if statement) if whatever the resource belongs to the user. 

```
#book_controller.rb

def edit
    @book = Book.find(params[:id])

    if !users_book(@book)
        flash[:alert] = "Cannot edit another users book"
        redirect_to user_path(current_user)
    end
end



private

def users_book(book)
    book.user_id == current_user.id
end
```

So every time a user tries to edit a book we are making sure they own it, redirecting them to their own user_path with an alert message if they don't own the book, and letting them straight through if they do. 
The structure is the same throughout all of the controllers that have to do with another user's data. 

On a side note is a great gem I tried out called 'exception_handler' that lets you easily make a custom error page. It's way better on the design, and user experience. It also allows you to redirect a user back to the homepage, or whatever options you'd like to include, instead of the app breaking when someone goes to a route that doesn't exist. 

## A new look on styling 

I love the way everything ended up looking. Beforehand I knew styling would be my weakest point, and what I need to focus on improving the most.
Don't get me wrong, I love my other creations and they have been great markers of my progression through coding... But this had the more professional, sleek look I was going for. I know there is SO much more room to improve.

I used Bulma for a majority of the styling, but for the first time, I added some custom CSS. I feel a bit late in the game for the styling, and I haven't spent as much time as I wanted practicing, but I felt pretty good with the small amount I was able to mix in with the Bulma styling. 

I managed to pull off some spacing, a few scroll-boxes, and FINALLY a background image! I've always loved a great background and I loved the look of the bookshelves and the wood in this picture. Here's some of the code from the view side of the app:

```
#In layouts/application.html.erb

<div class="hero is-fullheight has-bg-image">
    <%= yield %>
</div>
```

Here, we encapsulate the yield sign in a hero with the "has-bg-image" class, this has some CSS that sets the background image. 

```
<div class="section">
    <div class="container mx-6 py-6 has-text-centered">
        <div class="columns">
            <div class="column is-one-third"></div>
						
            <div class="column is-one-third">
                <div class="card">
                    <div class="card-content">
                        <div class="card">
                            <div class="card-content">
                            #Content goes here!
                            </div>
                         </div>
                     </div>
                </div>
            </div>
						
            <div class="column is-one-third"></div>
        </div>
    </div>
</div>
```

This is the layout for most of the views, I'm using Bulma custom classes to style the Html elements. It's setting three columns, each one-third of the page. Most of the pages make use of the center column only, so once I found this pattern it made it a much quicker process and I was able to focus on tweaking small details instead of changing around the layout of each view. 

```
.scroll-box {
background: #f4f4f4;
border: 2px solid rgba(0, 0, 0, 0.1);
height: 100px;
padding: 15px;
overflow-y: scroll;
}
```

And lastly, though simple I found the scroll box extremely useful on more than one view. I'm excited to learn more CSS and grow my skills in styling even further, but I'm very happy with how this project turned out looking and feeling in the end. 

## Summary 

It's impossible to sum up. It's a lot of work creating something of even this scale from scratch, at least until I reach a.
As the Rails portion of the curriculum comes to an end, after another wild ride full of new information, times of frustration, and of course a new skills to add to my arsenal... The cycle now restarts with Javascript. Exciting as it is nerve-racking, I'm fully ready to be baffled and confused again at first, and once more through consistency and repetition solidify my understanding of another language. 

