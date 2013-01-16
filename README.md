# Test application to debug white listing 

I'm having a problem with `config.wymeditor_whitelist_tags`.  I'm either
using the wrong syntax or there is a bug.  

## Scenario

My client needs to enter a sublime video tags/markup in the content
editor (WYMeditor).  

    <video class="sublime" width="640" height="360" poster="video-poster.jpg" data-uid="my-video-1" data-name="My Video #1" preload="none">
      <source src="http://yoursite.com/video.mp4" />
      <source src="http://yoursite.com/video-mobile.mp4" />
      <source src="http://yoursite.com/video.webm" />
    </video>

The problem is after saving hitting the "Save and continue editing"
button, it immediately sanitizes the html and leaves me with this:

    <video class="sublime" data-uid="my-video-1" data-name="My Video #1">
      <source>
      <source>

I've tried to edit the `config.wymeditor.whitelis.tags` option
several different ways with no luck:

    # Add extra tags to the wymeditor whitelist e.g. = {'tag' => {'attributes' => {'1' => 'href'}}} or just {'tag' => {}}
    config.wymeditor_whitelist_tags = {'source' => {}}
    config.wymeditor_whitelist_tags = {'<source>' => {}}
    config.wymeditor_whitelist_tags = {'source' => {'attributes' => {'1' => 'src'}}}
    config.wymeditor_whitelist_tags = {'<source>' => {'attributes' => {'1' => 'src'}}}

But I get the same result either way.

I also tried adding a custom tag, just to see if it was a problem with
the source tag:

    config.wymeditor_whitelist_tags = {'jess' => {}}

and it would not allow me to use the `<jess>` tag either.

I of course restarted the server each time I made a change.
