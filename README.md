## Welcome to Game Booster Docs

**Game Booster** is a set of scripts to create your game. It has a lot of daily common logic to accelerate your development. There is components to deal with movement, instantiation, destruction, input, score, and lot more.

The main principle of **Game Booster** is reusability. To achieve this, each component do simple things, and can be connected with others components (even your scripts) to achieve more complex behaviours. Many scripts has UnityEvent fields, which allows you to connect some event with other object’s methods and attributes on your scene.

The components are splitted in several categories: Basics, Movement, Physics, Collision Detection, Input, Time, Vars, Score, Mechanics and Audio.

## Basics components

Basics components deal with fundamental logic in Game Booster

### BehaviourEvents

Creates events for each MonoBehaviour events like Awake, Start, Update, OnEnable, etc. This component helps you to put simple logic in some MonoBehaviour event without creating a new script to it.

### Creator

Creates instance of prefabs. Randomically choose one prefab from the list to be instantiated at some spawn point. The own creator object can be used as spawn point, or a list of transforms. The spawn point rotation can be applied to the instantiated object. The created objects can be put inside some object hierarchy, to keep your scene organized. There are also options to make de creator auto instantiate object over time.

### Destroyer

This component has a few ways to destroy the object it is attached to. You can set a self-destruction time and a time to wait before destroy the object. An explosion prefab can be set to be instantiated when the object is destroied.

### ObjectSelector

Selects one object of a list, activating it, and deactivating the others of the list. Can be used to switch between weapons, costumes, screens, etc. There are methods to select one of the objects and to advance to next or previous object in the list.

### SceneMethods

Gives access to static methods relative to the scene, like load another scene, or reload the current one, quit application, and control timeScale to pause the game. This component don’t add features, just gives access point to static methods and properties to be called via events by other components.

### TransformMethods

Allows set individual axis of its transform position, scale and angle. Can, also, copy transform properties from another transform.

## Movement components
## Physics components
## Collision Detection components
## Input components
## Time components
## Vars components
## Score components
## Mechanics components
## Audio components



You can use the [editor on GitHub](https://github.com/raphaelmarques2/GameBoosterDocs/edit/master/README.md) to maintain and preview the content for your website in Markdown files.

Whenever you commit to this repository, GitHub Pages will run [Jekyll](https://jekyllrb.com/) to rebuild the pages in your site, from the content in your Markdown files.

### Markdown

Markdown is a lightweight and easy-to-use syntax for styling your writing. It includes conventions for

```markdown
Syntax highlighted code block

# Header 1
## Header 2
### Header 3

- Bulleted
- List

1. Numbered
2. List

**Bold** and _Italic_ and `Code` text

[Link](url) and ![Image](src)
```

For more details see [GitHub Flavored Markdown](https://guides.github.com/features/mastering-markdown/).

### Jekyll Themes

Your Pages site will use the layout and styles from the Jekyll theme you have selected in your [repository settings](https://github.com/raphaelmarques2/GameBoosterDocs/settings). The name of this theme is saved in the Jekyll `_config.yml` configuration file.

### Support or Contact

Having trouble with Pages? Check out our [documentation](https://help.github.com/categories/github-pages-basics/) or [contact support](https://github.com/contact) and we’ll help you sort it out.
