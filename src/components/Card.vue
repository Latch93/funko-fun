<template>
  <div id="funkoCards">
    <div>
      <h1>{{ title }}</h1>
    </div>
    <div class="flip-card">
      <div class="flip-card-inner">
        <div class="flip-card-front">
          <img
            class="funko-image"
            :alt="funkoData[index].altText"
            v-bind:src="'/' + funkoData[index].img"
          />
        </div>
        <div class="flip-card-back">
          <h1 class="cardHeading">
            <b>{{ funkoData[index].text }}</b>
          </h1>
          <p class="cardDescription">{{ funkoData[index].description }}</p>
          <p class="cardReleaseYear">
            Year of Character's first appearance:
            {{ funkoData[index].releaseYear }}
          </p>
          <p class="cardCategory">Category: {{ funkoData[index].category }}</p>
          <!-- <p>Number of Likes {{getFunkoLikeCounter(index)}}</p> -->
        </div>
      </div>
    </div>

    <div class="col-sm-5 d-inline-flex mt-3">
      <div class="col-sm-4">
        <button @click="decrementCounter">
          <img
            class="navButtonImg"
            :title="leftArrow.title"
            :alt="leftArrow.altText"
            v-bind:src="'/' + leftArrow.img"
          />
        </button>
      </div>
      <div class="col-sm-4">
        <p>Pop Count: {{ index + 1 }} / {{ getFunkoDataLength() }}</p>
        <button
          v-if="funkoData[index].isLiked"
          @click="toggleLikeFunkoPop(index)"
        >
          <img
            class="navButtonImg"
            :title="redHeart.title"
            :alt="redHeart.altText"
            v-bind:src="'/' + redHeart.img"
          />
        </button>
        <button v-else @click="toggleLikeFunkoPop(index)">
          <img
            class="navButtonImg"
            :title="grayHeart.title"
            :alt="grayHeart.altText"
            v-bind:src="'/' + grayHeart.img"
          />
        </button>
      </div>
      <div class="col-sm-4">
        <button class="navButton" @click="incrementCounter">
          <img
            class="navButtonImg"
            :title="rightArrow.title"
            :alt="rightArrow.altText"
            v-bind:src="'/' + rightArrow.img"
          />
        </button>
      </div>
    </div>
  </div>
  <div class="col-sm-4 text-center mx-auto mt-3">
    <h3>Browse the Funko Pops and hover over each card to reveal information on the character.</h3>
    <h3> You can like your favorite Funko Pops by clicking the heart icon.</h3>
  </div>
</template>

<script>
export default {
  name: "Card",
  data() {
    return {
      title: "Funko Fan!",
      index: 0,
      publicPath: process.env.BASE_URL,
      funkoData: [
        {
          text: "PHILHARMAGIC MICKEY MOUSE",
          description:
            "Commemorate 50 years of magic at Walt Disney World Resort with Mickey Mouse and other classic Disney characters as Pops! Mickey is ready to conduct the Philharmagic orchestra as this Pop! collectible. Bring Walt Disney World home with the new Walt Disney World Resort 50th Anniversary collection!",
          category: "Disney",
          altText: "Mickey Mouse with Philharmagic clothing Funko Pop",
          img: "./mickey-philharmagic-funko-pop.jpg",
          releaseYear: "1928",
          isLiked: false,
        },
        {
          text: "Sora",
          description:
            "Sora from Disney's Kingdom Hearts is given a fun, and funky, stylized look as an adorable collectible Pop! vinyl figure from Funko!",
          category: "Kingdom Hearts",
          altText: "Sora Funko Pop",
          img: "./sora-funko-pop.jpg",
          releaseYear: "2002",
          isLiked: false,
        },
        {
          text: "Figment",
          description:
            'Figment, a small purple dragon, occasionally seen sporting a yellow sweater, is the mascot of the "Imagination!" pavilion at the Epcot theme park at Walt Disney World Resort. He is extensively seen in Epcot merchandise.',
          category: "Disney",
          altText: "Chef Figment Funko Pop",
          img: "./figment-funko-pop.jpg",
          releaseYear: "1983",
          isLiked: false,
        },
        {
          text: "Sulley with Boo",
          description:
            "Celebrate the 20th Anniversary of Disney Pixar's Monster's Inc. with a Pop! The original mission was to scare until Mike and Sulley got a scare of their own. Bring home Pop! Sulley holding Boo in a cardboard box to complete your collection of Monster's Inc. and celebrate the 20th Anniversary of the movie's release!",
          category: "Monster's Inc",
          altText: "Sulley with Boo Funko Pop",
          img: "./sulley-with-boo-funko-pop.jpg",
          releaseYear: "2001",
          isLiked: false,
        },
        {
          text: "Gingerbread Thanos",
          description:
            "Will your Marvel Holiday collection crumble when the Funko exclusive Pop! Gingerbread Thanos steps into the sweet superhero setup?",
          category: "Marvel",
          altText: "Gingerbread Thanos Funko Pop",
          img: "./gingerbread-thanos-funko-pop.png",
          releaseYear: "1973",
          isLiked: false,
        },
        {
          text: "Dobby",
          description:
            "He's finally free! Welcome home one of the most well-known and lovable house elves of the Wizarding World with this Pop!",
          category: "Harry Potter",
          altText: "Dobby Funko Pop",
          img: "./dobby-funko-pop.jpg",
          releaseYear: "1998",
          isLiked: false,
        },
      ],
      leftArrow: {
        title: "Previous Pop",
        img: "./left-arrow.png",
        altText: "Left facing arrow",
      },
      rightArrow: {
        title: "Next Pop",
        img: "./right-arrow.png",
        altText: "Right facing arrow",
      },
      redHeart: {
        title: "Unlike Funko Pop",
        img: "./red-heart.png",
        altText: "Red heart icon",
      },
      grayHeart: {
        title: "Like Funko Pop",
        img: "./gray-heart.png",
        altText: "Grey heart icon",
      },
    };
  },
  methods: {
    // Increments page counter when the index is less than the length of cards - 1
    incrementCounter: function () {
      if (this.index != this.getFunkoDataLength() - 1) {
        this.index += 1;
      }
    },
    // Decrements page counter when the index is greater than 0
    decrementCounter: function () {
      if (this.index != 0) {
        this.index -= 1;
      }
    },
    // Gets length of cards in data set
    getFunkoDataLength: function () {
      return this.funkoData.length;
    },
    // Gets current index of card
    getCurrentIndex: function () {
      return this.index;
    },
    // Keeps status of isLiked and toggles boolean
    toggleLikeFunkoPop: function (index) {
      if (this.funkoData[index].isLiked == true) {
        this.funkoData[index].isLiked = false;
      } else {
        this.funkoData[index].isLiked = true;
      }
    },
  },
};
</script>
