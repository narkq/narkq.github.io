---
layout: post
title:  "Silence is evil"
date:   2015-06-17 23:00:07 +0300
---
Quick reminder to myself: if a [fluxible](http://fluxible.io/) store does not dehydrates on the server,
chances are that you forgot to call `emitChange` in a dispatcher callback.

For example, say, you've got a store:

{% highlight javascript linenos %}
export default createStore({
    storeName: 'AwesomeStore',
    handlers: {
        'RECEIVE_DATA': 'handleData'
    },
    handleData(data) {
        this.data = data;
        this.emitChange();
    },
    dehydrate() {
        return this.data;
    },
    rehydrate(state) {
        this.data = state;
    }
});
{% endhighlight %}

Then, if you forget a call at line 8, then on the server that store won't be dehydrated at all.

Silently.
