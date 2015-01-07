No wall of text, let's cut to the chase.

Dynamic filtering pane:

![figure 1](https://raw.githubusercontent.com/gorhill/uBlock/master/doc/img/df-qg-01.png)

First column: what is to be dynamically filtered:

![figure 2](https://raw.githubusercontent.com/gorhill/uBlock/master/doc/img/df-qg-02.png)

As you can see, you can create dynamic filtering rules for object types, or hostnames according to their origin.

Second column: global dynamic filtering rules, i.e. whatever rule appears in this column applies everywhere, on all sites:

![figure 3](https://raw.githubusercontent.com/gorhill/uBlock/master/doc/img/df-qg-03.png)

Third column: local dynamic filtering rules, i.e. whatever rule appears in this column applies to the current site only:

![figure 4](https://raw.githubusercontent.com/gorhill/uBlock/master/doc/img/df-qg-04.png)

So there are **global** dynamic filtering rules, and **local** dynamic filtering rules.

Sensible security- and privacy-wise: blocking all 3rd-party frames by default everywhere: 

![figure 5](https://raw.githubusercontent.com/gorhill/uBlock/master/doc/img/df-qg-05.png)

All embedded 3rd-party frames were blocked on the page. Good. However it appears there was an embedded Youtube video in the article:

![figure 6](https://raw.githubusercontent.com/gorhill/uBlock/master/doc/img/df-qg-06.png)

If you want to block all 3rd-party frames by default, except for the embedded video on that particular site, two solutions:

![figure 7](https://raw.githubusercontent.com/gorhill/uBlock/master/doc/img/df-qg-07.png)

Create a local  _noop_ rule for 3rd-party frames:

![figure 8](https://raw.githubusercontent.com/gorhill/uBlock/master/doc/img/df-qg-08.png)

However the above rule would result in all 3rd-party frames to be unblocked.

The other better solution: create a local _noop_ rule for `youtube.com`: This will prevent dynamic filtering rules to apply to anything from `youtube.com`.

**Important:** take note that _noop_ rules by pass **only** broader dynamic filtering rules, static filtering is left completely intact, which means you won't see ads in the embedded Youtube videos.