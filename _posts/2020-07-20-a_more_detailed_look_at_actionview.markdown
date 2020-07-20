---
layout: post
title:      "A more detailed look at ActionView"
date:       2020-07-20 09:04:06 +0000
permalink:  a_more_detailed_look_at_actionview
---


Going into Rails, I had an admittedly shaky understanding of some of the concepts that were introduced in the previous section. A lot of different things clicked for me, and I was able to achieve enough of an understanding to be considered competent in Sinatra and continue, but I was left with a want to understand more about the underlying technologies at play. Thankfully, a lot of the different underlying technologies we used, such as ActiveRecord, were carried over to Rails.

The one technology I got tripped up on the most was, by far, [ActionView](https://guides.rubyonrails.org/action_view_overview.html). It uses a mix of both embedded ruby and html to present the user with what they’re supposed to see when they open a page in your Rails web app. In a standard Rails project, each controller has a views directory associated with it; for example, if you had a controller named `GuidesController`, you would also have a directory in your app/views folder called guides which would contain all of the views your guides have. In my application, this included an `index`, `show`, `new`, and `edit` form, along with a partial, `_form`.

“But wait,” I hear you ask, “what the heck is a partial?” A partial is a lot like a function in regular ruby. It acts almost just like any other ERB file, but with two twists: it can be rendered in any form, and it can include locals. Locals are just like parameters; they can store all different kinds of data / objects, which can be later used in different parts of the partial.

Partials open up several interesting possibilities in creating templates. They make it possible for us to refactor our code and make it more DRY (which stands for “Don’t Repeat Yourself”), resulting in more flexible and robust programs which can cater to a wide range of  use cases. Take, for example, a form for a guide:

```
# show.html.erb

<%= form_with model: @guide do |f| %>
   <%= f.hidden_field :user_id, value: @user.id %>
   <%= f.label :title %><br>
   <%= f.text_field :title %><br>
   <%= f.label 'Map:'%><br>
   <%= f.collection_select :map_id, Map.all, :id, :name%><br>
   <%= f.label :body%><br>
   <%= f.text_field :body %><br>
   <%= f.submit %>
<% end %>
```

In this form, we’re expecting two instance variables to be present in the controller actions: `@guide`, which would hold the guide with all the data we’re working with in the form, and `@user`, which would hold the currently logged in user. This may work for our show form, but what about our edit form? What if we want to specify another user in the hidden field than we have in our controller? What if we want to have a different guide being displayed while creating another one? All of this can be solved by moving this form to a partial and replacing the instance variables with locals:

```
#_form.html.erb

<%= form_with model: guide do |f| %>
   <%= f.hidden_field :user_id, value: user.id %>
   <%= f.label :title %><br>
   <%= f.text_field :title %><br>
   <%= f.label 'Map:'%><br>
   <%= f.collection_select :map_id, Map.all, :id, :name%><br>
   <%= f.label :body%><br>
   <%= f.text_field :body %><br>
   <%= f.submit %>
<% end %>
```

After that, we can then simply render the partial in any template we wish by writing the following:
```
#show.html.erb
<%= render partial: 'view_directory_here/form', locals: {guide: Guide.new, user: @user } %>
```
 
Note that we specify the directory explicitly, with “view_directory_here” being the view directory you put the partial in. This full directory path allows us to access the partial outside of the folder it’s in, but if we’re rendering the partial in a template within its own directory, we can access it like this:

`<%= render partial: 'form' %>`

