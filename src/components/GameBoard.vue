<template>
  <div class="game-board">
    <div class="game-board-tiles">
      <template v-for="(tile, index) in this.allTiles" :key="index">
        <div class="game-board-tile">
          <GameTile
            v-if="tile.type === 'flip'"
            :tile="tile"
            @click="tile.flipped = true"
          ></GameTile>
          <GameAnalysisTile
            v-else-if="tile.type === 'analysis'"
            class="game-board-tile-analysis"
            :tile="tile"
          >
          </GameAnalysisTile>
          <GameCard v-else class="game-board-tile-memo"></GameCard>
        </div>
      </template>
    </div>
  </div>
  <div v-if="this.gameIsWon">
    <h1>Win!</h1>
  </div>
  <div v-else-if="this.gameIsLost">
    <h1>Lose!!</h1>
  </div>
</template>

<script>
import GameTile from "./GameTile.vue";
import GameCard from "./GameCard.vue";
import GameAnalysisTile from "./GameAnalysisTile.vue";

export default {
  name: "GameBoard",
  components: {
    GameTile,
    GameCard,
    GameAnalysisTile,
  },
  props: {
    length: {
      type: Number,
      default: 5,
    },
    value: {
      type: Number,
      default: 25,
    },
    difficulty: {
      type: Number,
      default: 1,
    },
  },
  data() {
    return {
      loading: true,
      tiles: [],
      distributedValue: 0,
    };
  },
  mounted() {
    this.resetBoard();
  },
  computed: {
    size() {
      return Math.pow(this.length, 2);
    },
    numberOfBombs() {
      if (!this.difficulty) {
        return Math.floor(this.size / 3.75);
      }
      if (this.difficulty === 1) {
        return Math.floor(this.size / 3.125);
      }
      return Math.floor(this.size / 2.5);
    },
    totalValueOfTiles() {
      return (
        this.tiles?.reduce((result, tile) => result + Number(tile.value), 0) ||
        0
      );
    },
    flipTiles() {
      if (this.loading || !this.tiles.length) {
        return [];
      }

      return this.tiles;
    },
    allTiles() {
      if (this.loading) {
        return [];
      }

      var details = this.getRowDetails();
      let count = 0;
      return this.flipTiles
        .reduce((results, tile) => {
          results ??= [];

          results.push(tile);
          count++;
          if (count === 5) {
            results.push(details[0]);
            details.shift();
            count = 0;
          }
          return results;
        }, [])
        .concat(this.getColumnDetails())
        .concat([{ type: "memo" }]);
    },
    gameIsWon() {
      if (this.loading || !this.tiles.length) {
        return false;
      }

      return !(
        this.tiles.filter((tile) => tile.value > 1 && !tile.flipped).length > 0
      );
    },
    gameIsLost() {
      if (this.loading || !this.tiles.length) {
        return false;
      }

      return (
        this.tiles.filter((tile) => tile.value === 0 && tile.flipped).length > 0
      );
    },
  },
  methods: {
    resetBoard() {
      this.loading = true;

      //reset board
      for (let i = 0; i < this.size; i++) {
        this.tiles.push({
          type: "flip",
          value: 1,
          flipped: false,
        });
      }

      //set bombs
      let placedBombs = 0;
      while (placedBombs < this.numberOfBombs) {
        const targetTile = this.tiles[this.getRandomTilePosition()];
        if (targetTile.value > 0) {
          targetTile.value = 0;
          placedBombs++;
        }
      }

      //set multipliers
      let remainingValue = this.value - this.totalValueOfTiles;
      while (remainingValue > 0) {
        const targetTile = this.tiles[this.getRandomTilePosition()];
        if (targetTile.value > 0 && targetTile.value + 1 < 4) {
          targetTile.value++;
          remainingValue--;
        }
      }

      this.loading = false;
    },
    getRandomTilePosition() {
      return this.random(0, this.size - 1);
    },
    random(min, max) {
      return Math.floor(Math.random() * (max - min + 1) + min);
    },
    getRowDetails() {
      if (!this.flipTiles.length) {
        return [];
      }
      var details = [];
      for (let i = 0; i < this.length; i++) {
        details.push(this.analyze(this.getRow(i)));
      }
      return details;
    },
    getColumnDetails() {
      if (!this.flipTiles.length) {
        return [];
      }
      var details = [];
      for (let i = 0; i < this.length; i++) {
        details.push(this.analyze(this.getColumn(i)));
      }
      return details;
    },
    getRow(index) {
      const start = index * this.length;
      const end = start + this.length;
      return this.flipTiles.slice(start, end);
    },
    getColumn(index) {
      if (!this.flipTiles.length) {
        return [];
      }

      return this.flipTiles
        .slice(index)
        .filter((e, i) => i % this.length === 0);
    },
    analyze(tiles) {
      return tiles.reduce(
        (result, tile) => {
          result.value += tile?.value;
          if (!tile?.value) {
            result.bombs++;
          }

          return result;
        },
        {
          type: "analysis",
          value: 0,
          bombs: 0,
        }
      );
    },
  },
};
</script>

<style scoped>
.game-board {
  width: 100%;
  display: flex;
  flex-wrap: wrap;
  justify-content: space-between;
}

.game-board-tiles {
  width: 100%;
  height: 100%;
  display: flex;
  flex-wrap: wrap;
  align-items: flex-start;
}

.game-board-tile {
  width: 16.5%;
  height: 16.5%;
  display: flex;
  justify-content: space-around;
}

.game-board-tile-analysis {
  width: 90%;
  height: 90%;
}

.game-board-tile-memo {
  width: 90%;
  height: 90%;
}

.game-board-tile-memo {
  background-color: var(--theme-colour-lightest);
}
</style>
