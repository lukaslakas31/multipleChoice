# MultipleChoice

Last but not least is an all-time favorite eLearning game format used by many, which is Multiple Choice. Here, learners will choose the right answer among options that are in text format. Depending on the template you’re using, there can be multiple correct answers. As it encourages learners to think critically to not be tricked by the other choices, it’s effective for active reinforcement.

# Build Setup
To set up this game, follow the steps below:
```nuxt.js
# install dependencies
$ npm  install

# serve with hot reload at localhost:3000
$ npm  run  dev

# build for production and launch server

$ npm  run  build
$ npm  run  start
```

# Game Setup

To use the Multiple Choice component in your index.vue file, pass the "questions" props to the component, as shown below:

```html
	<multipleChoice :questions="questions"/>
```

Here's an example of how to define the "questions" data object in your script section:

```js
	export default {
	data () {
	return {
		questions: [
		{
			questions: "Your Question Here", 
			answers: [
				{text: "choice #1" , correct: true},  // set if it is the right answer by 
				{text: "choice #2" , correct: false}, // setting the boolean correct to:
				{text: "choice #3" , correct: false}, // true or false
				]
			},
			//add more questions here
			]
		}
	}
}
```
you can now play the multipleChoice game! enjoy!

# Updates

this game will be updated in the future for OJT purposes. 


# Dev Team!
* [Luke Galicia -  CCCI Intern](https://github.com/lukaslakas31)
*  [Angelo Edrosa - CCCI Intern](https://github.com/AngeloEdrosa)
*   [Mary Antonette Ubiña - CCCI Intern](https://github.com/Antonette08)