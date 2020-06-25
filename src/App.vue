<template>
  <div id="app">
    <div id="app">
      <header>My Listening List</header>
      <main>
        <section class="player">
          <h2 class="book-title">
            {{ current.title }} - <span>{{ current.author }}</span>
          </h2>
          <div class="controls">
            <button class="prev" @click="prev">Prev</button>
            <button class="play" v-if="!isPlaying" @click="play">Play</button>
            <button class="pause" v-else @click="pause">Pause</button>
            <button class="next" @click="next">Next</button>
          </div>
        </section>
        <section class="playlist">
          <h3>The Playlist</h3>
          <button
            class="book"
            v-for="book in books"
            :key="book.src"
            @click="play(book)"
            :class="book.src == current.src ? 'playing' : 'book'"
          >
            {{ book.title }} -{{ book.author }}
          </button>
        </section>
      </main>
    </div>
  </div>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      current: {},
      index: 0,
      isPlaying: false,
      books: [
        {
          title: "Educational Vibe",
          author: "Liam & Vance",
          src: require("./assets/audio/audio1.mp3"),
        },
        {
          title: "Inspiring and Motivating",
          author: "Twisterium",
          src: require("./assets/audio/audio2.mp3"),
        },
        {
          title: "Stop Motion Town",
          author: "Basspartout",
          src: require("./assets/audio/audio3.mp3"),
        },
      ],
      player: new Audio(),
    };
  },
  methods: {
    play(book) {
      if (typeof book.src != "undefined") {
        this.current = book;
        this.player.src = this.current.src;
      }
      this.player.play();
      this.player.addEventListener[
        ("ended",
        function() {
          this.index++;
          if (this.index > this.books.length - 1) {
            this.index = 0;
          }
        }.bind(this))
      ];
      this.isPlaying = true;
    },
    pause() {
      this.player.pause();
      this.isPlaying = false;
    },
    next() {
      this.index++;
      if (this.index > this.books.length - 1) {
        this.index = 0;
      }

      this.current = this.books[this.index];
      this.play(this.current);
    },
    prev() {
      this.index--;
      if (this.index < 0) {
        this.index = this.books.length - 1;
      }

      this.current = this.books[this.index];
      this.play(this.current);
    },
  },
  created() {
    this.current = this.books[this.index];
    this.player.src = this.current.src;
    // this.player.play();
  },
};
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  font-family: sans-serif;
}

header {
  display: flex;
  justify-content: center;
  align-items: center;
  padding: 15px;
  background-color: #212121;
  color: #fff;
}

main {
  width: 100%;
  max-width: 768px;
  margin: 0 auto;
  padding: 25px;
}

.book-title {
  color: #53563a;
  font-size: 32px;
  font-weight: 700;
  text-transform: uppercase;
  text-align: center;
}

.book-title span {
  font-weight: 400;
  font-style: italic;
}

.controls {
  display: flex;
  justify-content: center;
  align-items: center;
  padding: 30px 15px;
}
button {
  appearance: none;
  background: none;
  border: none;
  outline: none;
  cursor: pointer;
}
button:hover {
  opacity: 0.8;
}
.play,
.pause {
  font-size: 20px;
  font-weight: 700px;
  padding: 15px 25px;
  margin: 0px 15px;
  border-radius: 8px;
  color: #fff;
  background-color: #cc2e50;
}
.next,
.prev {
  font-size: 16px;
  font-weight: 700px;
  padding: 10px 20px;
  margin: 0px 15px;
  border-radius: 6px;
  color: #fff;
  background-color: #ff5858;
}
.playlist {
  padding: 0px 30px;
}
.playlist h3 {
  color: #212121;
  font-size: 20px;
  font-weight: 400;
  margin-bottom: 20px;
  text-align: center;
}
.playlist .book {
  display: block;
  width: 100%;
  padding: 15px;
  font-size: 20px;
  font-weight: 700;
  cursor: pointer;
}
.playlist .book:hover {
  color: #ff5858;
}
.playlist .book.playing {
  color: #fff;
  background-image: linear-gradient(to right, #cc2e5d, #ff5858);
}
</style>
