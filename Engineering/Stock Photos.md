# Photos

## Finding

We've had the best luck finding photos on [Flickr](https://www.flickr.com/search/?license=4%2C5%2C6%2C9%2C10&advanced=1&text=san%20francisco%20golden%20gate%20park). Be sure to enable the **commercial use allowed** flag when searching.

The [awesome-stock-resources](https://github.com/neutraltone/awesome-stock-resources#photography) github repo has a big list of public-domain photo sites.

## Using

Save the photo in `assets/images/heros`. If it's huge, crop it down to a reasonable size. Dimensions don't need to be exact, as the CSS will zoom the image to fit: just think "banner".

Add a CSS style for your photo, scoping it by the DOM id of the page you're adding it to.

The background color behind the image is black. Set the `opacity` of the background image to a value between 0 and 1 to get the darkness right. Usually `0.5` is good.


```css
#users-new .hero-background {
  opacity: 0.5;
  background-image: image-url("pages/signup/header-background.jpg");
}
```

Use the following in your view to render a header.

```erb
<%= content_for :hero do %>
  <h1>Yada Yada Goes Here</h1>
<% end %>

<%= content_for :hero_photo_credit do %>
  <a href="https://www.flickr.com/photos/padday/3598890102">Paul Adams</a>
<% end %>
```
