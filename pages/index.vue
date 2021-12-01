<template>
  <nav id="navbar">
    <v-app-bar class="white" flat app clipped-left>
      <v-app-bar-nav-icon @click.stop="drawer = !drawer"></v-app-bar-nav-icon>
      <v-toolbar-title class="font-weight-bold"
        ><router-link to="/" class="black--text" style="text-decoration: none"
          ><v-icon sixe="25" class="yt">mdi-youtube</v-icon>YouTube</router-link
        ></v-toolbar-title
      >
      <v-spacer></v-spacer>
      <v-text-field
        flat
        hide-details
        append-icon="mdi-magnify"
        placeholder="Search"
        outlined
        dense
        v-model="searchText"
        @click:append="search"
        class="hidden-sm-and-down"
      ></v-text-field>
      </v-tooltip>
      <v-tooltip bottom>
        <template v-slot:activator="{ on }">
          <v-btn icon v-on="on" class="mr-7">
            <v-icon size="25">mdi-microphone</v-icon></v-btn
          >
        </template>
        <span>Search with your voice</span>
      </v-tooltip>

      <v-spacer></v-spacer>
      <v-menu offsetY>
        
        <v-list>
          <v-list-item router to="/studio">
            <v-list-item-icon class="mr-3"
              ><v-icon>mdi-play-box-outline</v-icon></v-list-item-icon
            >
            <v-list-item-title>Upload video</v-list-item-title>
          </v-list-item>
          <v-list-item>
            <v-list-item-icon class="mr-3"
              ><v-icon>mdi-access-point</v-icon></v-list-item-icon
            >
            <v-list-item-title>Go live</v-list-item-title>
          </v-list-item>
        </v-list>
      </v-menu>

      <v-tooltip bottom>
        <template v-slot:activator="{ on }">
          <v-btn icon v-on="on"> <v-icon size="25">mdi-apps</v-icon></v-btn>
        </template>
        <span>YouTube apps</span>
      </v-tooltip>
      <v-tooltip bottom>
        <template v-slot:activator="{ on }">
          <v-btn icon v-on="on" class="mr-7">
            <v-icon size="25">mdi-dots-vertical</v-icon></v-btn
          >
        </template>
        <span>Settings</span>
      </v-tooltip>

      <v-menu offset-y left>
        <template v-slot:activator="{ on }">
          <v-btn outlined><v-icon size="25">mdi-account</v-icon>
            SIGN IN
          </v-btn>
        </template>

      </v-menu>
    </v-app-bar>
    <div class="chip">
          <v-chip
            outlined
          >All</v-chip>
      </div>
        <div class="chip">
          <v-chip
            outlined
          >Live</v-chip>
      </div>
      <div class="chip">
          <v-chip
            outlined
          >Blues rock music</v-chip>
      </div>
      <div class="chip">
          <v-chip
            outlined
          >Deep House</v-chip>
      </div>
      <div class="chip">
          <v-chip
            outlined
          >Chill-out music</v-chip>
      </div>
      <div class="chip">
          <v-chip
            outlined
          >Christmas music</v-chip>
      </div>
      <div class="chip">
          <v-chip
            outlined
          >Kygo</v-chip>
      </div>
      <div class="chip">
          <v-chip
            outlined
          >Music</v-chip>
      </div>
      <div class="chip">
          <v-chip
            outlined
          >Russian chanson music</v-chip>
      </div>
      <div class="chip">
          <v-chip
            outlined
          >Techno</v-chip>
      </div>
      <div class="chip">
          <v-chip
            outlined
          >Tourism</v-chip>
      </div>
      <div class="chip">
          <v-chip
            outlined
          >Orchestra</v-chip>
      </div>
      <div class="chip">
          <v-chip
            outlined
          >Melodramas</v-chip>
      </div>
      <div class="chip">
          <v-chip
            outlined
          >Albums</v-chip>
      </div>

    <img src="../assets/youtube.png"></img>

    <v-navigation-drawer
      v-model="drawer"
      app
      :clipped="$route.name !== 'Watch'"
      :temporary="$route.name === 'Watch'"
      id="nav"
    >
      <div tag="div" class="v-navigation-drawer__content" v-bar>
        <v-list dense nav class="py-0" tag="div">
          <v-list-item
            :class="{
              'hidden-lg-and-up': $route.name === 'Watch' ? false : true
            }"
          >
            <v-app-bar-nav-icon
              @click="drawer = !drawer"
              class="mr-5"
            ></v-app-bar-nav-icon>
            <v-toolbar-title class="font-weight-bold">Youtube</v-toolbar-title>
          </v-list-item>
          <v-divider class="hidden-lg-and-up"></v-divider>
          <div v-for="parentItem in items" :key="parentItem.header">
            <v-subheader
              v-if="parentItem.header"
              class="pl-3 py-4 subtitle-1 font-weight-bold text-uppercase"
              >{{ parentItem.header }}</v-subheader
            >
            <v-list-item
              v-for="(item, i) in parentItem.pages"
              :key="item.title"
              link
              class="mb-0"
              router
              :to="item.link"
              exact
              active-class="active-item"
            >
              <v-list-item-icon v-if="parentItem.header !== 'Subscriptions'">
                <v-icon>{{ item.icon }}</v-icon>
              </v-list-item-icon>
              <v-list-item-avatar v-else class="mr-5">
                <img
                  :src="`https://randomuser.me/api/portraits/men/${i}.jpg`"
                />
              </v-list-item-avatar>
              <v-list-item-content>
                <v-list-item-title class=" font-weight-medium subtitle-2">{{
                  item.title
                }}</v-list-item-title>
              </v-list-item-content>
            </v-list-item>
            <v-divider class="mt-2 mb-2"></v-divider>
          </div>

          <span v-for="link in links" :key="link.text">
            <span v-if="link.text === 'Terms'" class="mb-2 d-block"> </span>
            <v-btn
              href
              router
              :to="link.link"
              text
              class="text-capitalize px-1"
              small
              >{{ link.text }}</v-btn
            >
          </span>
        </v-list>
      </div>
    </v-navigation-drawer>
  </nav>
</template>

<script>
export default {
  
  data: () => ({
    
    drawer: false,
    items: [
      
      {
        header: null,
        pages: [
          { title: 'Home', link: '/', icon: 'mdi-home' },
          { title: 'Explore', link: '/explore', icon: 'mdi-compass' },
          {
            title: 'Subscriptions',
            link: '#s',
            icon: 'mdi-youtube-subscription'
          }
        ]
      },
      {
        header: null,
        pages: [
          {
            title: 'Library',
            link: '#l',
            icon: 'mdi-play-box-multiple'
          },
          {
            title: 'History',
            link: '/history',
            icon: 'mdi-history'
          }
        ]
      },
      {
      header: null,
        pages: [
          {
            title: 'SIGN IN',
            link: '#l',
            icon: 'mdi-account'
          },
        ]
   },
   {
        header: 'BEST OF YOUTUBE',
        pages: [
          {
            title: 'Music',
            link: '#vp',
            icon: 'mdi-music'
          },
          {
            title: 'Sports',
            link: '#g',
            icon: 'mdi-trophy-variant'
          },
          {
            title: 'Gaming',
            link: '#li',
            icon: 'mdi-youtube-gaming'
          },
          {
            title: 'News',
            link: '#g',
            icon: 'mdi-newspaper-variant'
          },
          {
            title: 'Live',
            link: '#g',
            icon: 'mdi-access-point'
          },
          {
            title: '360° Video',
            link: '#g',
            icon: 'mdi-domino-mask'
          },
          {
            title: 'Browse channels',
            link: '#g',
            icon: 'mdi-plus-circle'
          }
          
        ]
      },
   {
        header: 'MORE FROM YOUTUBE',
        pages: [
          {
            title: 'YouTube Premium',
            link: '#vp',
            icon: 'mdi-youtube'
          },
          {
            title: 'Live',
            link: '#li',
            icon: 'mdi-access-point'
          }
        ]
      },
      {
        header: null,
        pages: [
          {
            title: 'Setting',
            link: '#sg',
            icon: 'mdi-cog'
          },
          {
            title: 'Report history',
            link: '#rh',
            icon: 'mdi-flag'
          },
          {
            title: 'Help',
            link: '#hp',
            icon: 'mdi-help-circle'
          },
          {
            title: 'Send feedback',
            link: '#f',
            icon: 'mdi-message-alert'
          }
        ]
      }
    ],
    links: [
      { text: 'About', link: '#' },
      { text: 'Press', link: '#' },
      { text: 'Copyrignt', link: '#' },
      { text: 'Contact us', link: '#' },
      { text: 'Creators', link: '#' },
      { text: 'Advertise', link: '#' },
      { text: 'Developers', link: '#' },
      { text: 'Terms', link: '#' },
      { text: 'Privacy', link: '#' },
      { text: 'Policy & Safety', link: '#' },
      { text: 'Test new features', link: '#' }
    ],
    searchText: ''
  }),
  methods: {
    search() {
      if (!this.searchText) return
      this.$router.push({
        name: 'Search',
        query: { 'search-query': this.searchText }
      })
    }
  },
  mounted() {
    this.drawer = this.$vuetify.breakpoint.mdAndDown ? false : true
    this.drawer = this.$route.name === 'Watch' ? false : this.drawer
  }
}
</script>

<style lang="scss">
#navbar {
  .active-item {
    .v-list-item__icon {
      color: red !important;
    }
  }
  .v-navigation-drawer__border {
    width: 0 !important;
  }

  .vuebar-element {
    height: 250px;
    width: 100%;
    max-width: 500px;
    background: #dfe9fe;
  }

  .vb > .vb-dragger {
    z-index: 5;
    width: 10px;
    right: 0;
  }

  .vb > .vb-dragger > .vb-dragger-styler {
    -webkit-backface-visibility: hidden;
    backface-visibility: hidden;
    -webkit-transform: rotate3d(0, 0, 0, 0);
    transform: rotate3d(0, 0, 0, 0);
    -webkit-transition: background-color 100ms ease-out, margin 100ms ease-out,
      height 100ms ease-out;
    transition: background-color 100ms ease-out, margin 100ms ease-out,
      height 100ms ease-out;

    margin: 5px 5px 5px 0;
    border-radius: 20px;
    height: calc(100% - 10px);
    display: block;
  }

  .v-navigation-drawer__content:hover .vb > .vb-dragger > .vb-dragger-styler {
    width: 10px;
    background-color: #e0e0e0;
  }

  .vb.vb-scrolling-phantom > .vb-dragger > .vb-dragger-styler {
    background-color: rgba(48, 121, 244, 0.3);
    background-color: rgba(255, 255, 255, 0.3);
  }

  .vb > .vb-dragger:hover > .vb-dragger-styler {
    margin: 0px;
    width: 10px;
  }

  .vb.vb-dragging > .vb-dragger > .vb-dragger-styler {
    background-color: rgba(48, 121, 244, 0.5);
    margin: 0px;
    height: 100%;
  }

  .vb.vb-dragging-phantom > .vb-dragger > .vb-dragger-styler {
    background-color: rgba(48, 121, 244, 0.5);
  }
  .chip {
    display:inline-block;
    vertical-align: top;
    margin-left:20px;
  }
  .yt {
    color:red;
  }
  img{
    width: 100%;
    height:100%;
  }
}
</style>