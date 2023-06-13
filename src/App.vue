<template>
  <div class="ctr">
    <questions 
      v-if="questionsAnswered < questions.length" 
      :questions="questions" 
      :questionsAnswered="questionsAnswered"
      @question-answered="questionAnswered"
      >
    </questions>
    <results 
      v-else
      :results="results"
      :totalCorrect="totalCorrect"
    >
    </results>
    <button type="button" class="reset-btn" @click.prevent="reset" v-if="this.questionsAnswered === questions.length">Reset</button>
  </div>
</template>

<script>
import Questions from './components/Questions.vue';
import Results from './components/Results.vue';

export default {
  name: 'App',
  components: {
    Questions,
    Results
},
  data() {
    return {
      questionsAnswered: 0,
      totalCorrect: 0,
      questions: [
        {
          q: 'Who has the cutest nose in the world?',
          answers: [
            {
              text: 'Misa',
              is_correct: true
            },
            {
              text: 'Will',
              is_correct: false
            },
            {
              text: 'Cindy Lou Who',
              is_correct: false
            },
            {
              text: 'Bob Jones',
              is_correct: false
            }
          ]
        },
        {
          q: 'Who is the spiciest of them all?',
          answers: [
            {
              text: 'A habenero pepper',
              is_correct: false
            },
            {
              text: 'Chili flakes',
              is_correct: false
            },
            {
              text: 'Misa',
              is_correct: true
            },
            {
              text: 'The actual Sun',
              is_correct: false
            }
          ]
        },
        {
          q: 'Who is Misas favorite strange creature',
          answers: [
            {
              text: 'Yoda',
              is_correct: false
            },
            {
              text: 'Samson',
              is_correct: true
            },
            {
              text: 'Mace Windu',
              is_correct: false
            },
            {
              text: 'Obi-Wan-Kenobi',
              is_correct: false
            }
          ]
        },
        {
          q: 'What is Misas favorite color?',
          answers: [
            {
              text: 'Pink',
              is_correct: false
            },
            {
              text: 'Purple',
              is_correct: false
            },
            {
              text: 'Blue',
              is_correct: true
            },
            {
              text: 'Poop color',
              is_correct: false
            }
          ]
        },
        {
          q: 'Who has the roundest booty in all the lands, definitely meant for squeezes?',
          answers: [
            {
              text: 'Dwayne Johnson',
              is_correct: false
            },
            {
              text: 'Garfield',
              is_correct: false
            },
            {
              text: 'Misa',
              is_correct: true
            },
            {
              text: 'Stan Marsh',
              is_correct: false
            }
          ]
        },
        {
          q: 'What is the best condiment to use on a burger? (or on anything)',
          answers: [
            {
              text: 'Mustard',
              is_correct: false
            },
            {
              text: 'Micro-Greens',
              is_correct: false
            },
            {
              text: 'Horseradish',
              is_correct: false
            },
            {
              text: '2-3 gallons of ketchup',
              is_correct: true
            }
          ]
        },
        {
          q: 'Who has the sweetest laugh in this sector of the state of Wisconsin?',
          answers: [
            {
              text: 'Misa',
              is_correct: true
            },
            {
              text: 'Bob Dole',
              is_correct: false
            },
            {
              text: 'The Koolaid man',
              is_correct: false
            },
            {
              text: 'Betty Crocker',
              is_correct: false
            }
          ]
        },
        {
          q: 'What is Misas favorite flavor of ice cream?',
          answers: [
            {
              text: 'Strawberry',
              is_correct: false
            },
            {
              text: 'Cookie Dough',
              is_correct: true
            },
            {
              text: 'Mint Chocolate Chip',
              is_correct: false
            },
            {
              text: 'Bana Creme Fudge Detonation',
              is_correct: false
            }
          ]
        },
        {
          q: 'Who is Misas favorite person to interlock toes with?',
          answers: [
            {
              text: 'Sam',
              is_correct: true
            },
            {
              text: 'Herself. Her own toes',
              is_correct: false
            },
            {
              text: 'Joe Biden',
              is_correct: false
            },
            {
              text: 'Alec Baldwin',
              is_correct: false
            }
          ]
        },
        {
          q: 'Who always smells amazing?',
          answers: [
            {
              text: 'Unicorn Rainbow Man',
              is_correct: false
            },
            {
              text: 'Tulips',
              is_correct: false
            },
            {
              text: 'Misa',
              is_correct: true
            },
            {
              text: 'A dresser',
              is_correct: false
            }
          ]
        },
        {
          q: 'Who is the best person to snuggle with ever?',
          answers: [
            {
              text: 'Pillows',
              is_correct: false
            },
            {
              text: 'Misa',
              is_correct: true
            },
            {
              text: '25lb Block of cheese',
              is_correct: false
            },
            {
              text: '40000 Pounds of ammonium nitrate',
              is_correct: false
            }
          ]
        },
        {
          q: 'Who is Sams favorite golden haired girl?',
          answers: [
            {
              text: 'Margerine',
              is_correct: false
            },
            {
              text: 'Sarah',
              is_correct: false
            },
            {
              text: 'Penelope',
              is_correct: false
            },
            {
              text: 'Misa :)',
              is_correct: true
            }
          ]
        }
        //12
        // {
        //   q: '',
        //   answers: [
        //     {
        //       text: '',
        //       is_correct:
        //     },
        //     {
        //       text: '',
        //       is_correct:
        //     },
        //     {
        //       text: '',
        //       is_correct:
        //     },
        //     {
        //       text: '',
        //       is_correct:
        //     }
        //   ]
        // }
      ],
      results: [
        {
          min: 0,
          max: 11,
          title: "Try again!",
          desc: "Wow. You clearly don't even know that Misa is literally the bestest of all. Please take this quiz again until you realize the errors of your ignorance."
        },
        {
          min: 12,
          max: 12,
          title: "Wow, you're a genius!",
          desc: "Yay Misa is the sweetest she won the game by getting all the questions right :)!"
        }
      ]
    }
  },
  methods: {
    questionAnswered(is_correct) {
      if(is_correct) {
        this.totalCorrect++;
      }

      this.questionsAnswered++;
    },
    reset() {
      this.questionsAnswered = 0;
      this.totalCorrect = 0;
    }
  }
}
</script>

<style></style>
