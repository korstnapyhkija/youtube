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
          <v-btn outlined color="primary"><v-icon size="25">mdi-account</v-icon>
            SIGN IN
          </v-btn>
        </template>

      </v-menu>
    </v-app-bar>

    <div class="chips">
          <v-chip outlined color="white">All</v-chip>
          <v-chip outlined color="white">Live</v-chip>
          <v-chip outlined color="white">Blues rock music</v-chip>
          <v-chip outlined color="white">Deep House</v-chip>
          <v-chip outlined color="white">Chill-out music</v-chip>
          <v-chip outlined color="white">Christmas music</v-chip>
          <v-chip outlined color="white">Kygo</v-chip>
          <v-chip outlined color="white">Music</v-chip>
          <v-chip outlined color="white">Russian chanson music</v-chip>
          <v-chip outlined color="white">Techno</v-chip>
          <v-chip outlined color="white">Tourism</v-chip>
          <v-chip outlined color="white">Orchestra</v-chip>
          <v-chip outlined color="white">Melodramas</v-chip>
          <v-chip outlined color="white">Game shows</v-chip>
          <v-chip outlined color="white">Tools</v-chip>
          <v-chip outlined color="white">Nature</v-chip>
          <v-chip outlined color="white">Snow</v-chip>
          </div>

    <div class="content">
        <div class="vid">
            <div class="preview">
                <img src="../assets/minecraft.jpg" alt=""> 
                <div class="time">1:50</div>
                <div class="hovicons">
                  <v-icon>mdi-clock-outline</v-icon>
                  <v-icon>mdi-menu</v-icon>
                </div>
            </div>
            <div class="idk">
                <div class="left">
                <img class="profile" src="https://picsum.photos/201">
                <div class="below">
                    <h2>Minecraft Caves & Cliffs Update: Part II - Official Trailer</h2>
                    <p class="username">Minecraft</p>
                    <p>1.4M views &bull; 1 day ago</p>

                    </div>
                </div>
              </div>
            </div>
          </div>

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
  .chips {
    display:inline-block;
    vertical-align: top;
    margin-left:30px;
  }
  .yt {
    color:red;
  }
  img{
    width: 100%;
    height:100%;
  }

.left, .middle, .right {
    display: flex;
    flex-direction: row;
    align-items: center;
}

.left {
    width: 160px;
}
.left i{
    margin-right: 20px;
}

.middle .search input{
    background-color: var(--bg-main);
    border: 1px solid var(--light-gray);
    padding: 7px;
    width: 500px;
    font-size: 1.2em;
    color: lightgray;

    border-collapse: collapse;
}

.middle .search input:focus{
    border: 2px solid rgb(255, 0, 0);
}

.search{
    display: flex;
    flex-direction: row;
}

.middle .search .searchbtn {
    height: 2em;
    width: 80px;
    font-size: 1.2em;
    color: rgb(122, 122, 122);
    background-color: var(--light-gray);
    display: grid;
    text-align: center;
    align-items: center;
    cursor: pointer;
    border-radius: 0 5px 5px 0;
}
.searchbtn i {
    color: white;
    opacity: .4;
}
.searchbtn:hover i {
    opacity: .8;
}

.topbar .middle .fa-microphone {
    margin-left: 20px;
}

.right {
    width: 300px;
    justify-content: space-evenly;
}
.right .icons {
    display: flex;
    justify-content: space-between;
    width: 130px;
}

img.profile {
    height: 2.2em;
    border-radius: 50%;
}

.content {
    margin-top: 60px;
    margin-left: 230px;
    height: 120vh;
    padding: 3%;
    font-family: sans-serif;
    display: flex;
    flex-wrap: wrap;
}

.vid {
    margin: 10px 10px 10px 10px;
    display: flex;
    flex-direction: column;
    width: fit-content;
    cursor: pointer;
}

.vid .idk {
    display: flex;
    flex-direction: row;
    justify-content: space-between;
}

.below {
    display: inline;
    width: 96px;
    margin-left: 8px;
}

.vid .idk h2, .vid .idk p{
    margin: 0;
    padding: 0;
    white-space: nowrap;
}
.idk h2 {
    font-size: 16px;
    color: white;
    cursor: pointer;
}
.idk p{
    color: #aaaaaa;
}

p.username:hover{
    color: white;
}

.idk i {
    margin-top: 5px;
    color: #aaaaaa;
}

.preview .time {
    font-size: .8em;
    position: absolute;
    transform: translate(300px, -30px);
    padding: 3px;
    padding-right: 5px;
    border-radius: 3px;
    color: white;
    background-color: rgba(0, 0, 0, 0.733);
}
.hovicons {
    position: absolute;
    display: flex;
    flex-direction: column;
    transform: translate(310px, -190px);
    opacity: 0;
}

.vid:hover .hovicons {
    opacity: 1;
}

.hovicons i{
    color: white;
    background-color: rgba(0, 0, 0, 0.733);
    margin-bottom: 5px;
    padding: 4px 4px 4px 4px;
    border-radius: 3px;
}

}
</style>