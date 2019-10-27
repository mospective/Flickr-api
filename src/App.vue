<template>
  <div id="app">
    <header>
      <h1>Flickr App Test</h1>
    </header>
    <main>
      <section class="container">
        <div class="grp-cards" ref="content">
          <div class="card" v-for="(item, index) in items" :key="index" data-aos="fade-up">
            <div class="img_bx">
              <img :src="item.media.m" alt="">
            </div>
            <div class="content">
              <div class="info">
                <p><a :href="item.media.m" target="_blank">{{item.title}}</a> by <a href="#" class="author">{{item.author}}</a></p>
              </div>
              <div class="desc">
                <!-- {{item.description}} -->
                <p>Content here has other elements within the description. For this reason I will not filter it for now</p>
              </div>
            </div>
          </div>
        </div>

      </section>
    </main>
  </div>
</template>

<script>
// import the packages from node modules
import jsonp from 'jsonp'
import AOS from 'aos'
import 'aos/dist/aos.css'
// 20aaabf5a874c8711424d05918250ede

export default {
  name: 'app',
  data: function () {
    return {
      items: []
    }
  },
  created () {
    // Call the api
    jsonp('https://api.flickr.com/services/feeds/photos_public.gne?format=json', { name: 'jsonFlickrFeed' }, (error, data) => {
      if (error) {
        console.log('parsing failed', error)
      } else {
        console.log('success', data)
        // Upon success store the data in `items` and initialise AOS animation
        this.items = data.items
        AOS.init()
      }
    })
  }
}
</script>
