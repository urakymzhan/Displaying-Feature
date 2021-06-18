---

Displaying Features - details page

---

## Displaying Features - Detail page

Each of the places has a list of features. The features describe the location as indoors or outdoors, whether there is coffee, art, or a bathroom available.

We could display these as text but it might be more fun and easier for people to understand if we displayed them with icons or emojis.

We have two choices to work with

- Emoji
- Images

Emojis are built in and require no extra libraries or files. They are also fairly compatible across systems today.

Images represent a lot of things, but using images would require more files, and more work on our part but possible be more compatible. Font Awesome would be a good choice here.

Let's give emoji a try.

## Convert words to emoji

Looking through the base data there are five features:

- outdoors
- coffee
- art
- toilet
- power

We need an emoji for each of these.

- 🌲 - outdoors
- ☕️ - coffee
- 🖼 - art
- 🚽 - toilet
- 🔌 - power

Now we need to convert an array of words to an array of emoji. Array.map is the tool for the job. Map is meant for transforming an array of one type into an array of another type. Here you'd be converting an array of text strings into an array of emoji strings.

Make a component that displays the emoji!

> [action]
>
> Make a folder: `PLACESFeatures`
>
> Inside that folder make a new file: `PLACESFeature.js`.
>
> Define a component:
>
```JS
import './PLACESFeature.css'

function getFeature(str) {
    switch(str) {
        case 'outdoors':
            return '🌲'
        case 'coffee':
            return '☕️'
        case 'art':
            return '🖼'
        case 'toilet':
            return '🚽'
        case 'power':
            return '🔌'
        default:
            return '？'
    }
}
function PLACESFeature(props) {
    const emoji = getFeature(props.name)
    return <div className="PLACESFeature">{emoji}</div>
}
export default PLACESFeature
```

This component will require a prop: name. You might create a instance like this:

```JS
<PLACESFeature name="coffee" />
```

Internally the component translates the word to an emoji using the `getFeature(str)` function.

The `switch` block is like an if else block. The switch tries to match the supplied value agains one of it's cases. If `str` matches the function returns an emoji string.

Add a stylessheet.

> [action]
>
> Inside `PLACESFeatures` folder create a new file: `PLACESFeature.css`
>
> Import this new stylesheet at the top `PLACESFeature.js`
>
```JS
import './PLACESFeature.css'
```
>
> Add the follow code at the top `PLACESFeature.css`:
>
```CSS
.PLACESFeature {
    font-size: 2em;
    padding: 0.25em;
    margin: 0.125em;
    border-radius: 0.25em;
    background-color: #eee;
}
```

This sets the font size, adds some padding and marging, sets the border radius, and sets a background color.

## Feature list

The Places data provides a list of 0 or more strings of features. This means we need to display a list of these `PLACESFeature` components.

Time to make a component! This new component will take an array of strings and return an array of `PLACESFeature` components.

> [action]
>
> Inside `PLACESFeatures` folder create a new file: `PLACESFeatureList`.
>
> Add the following code here to define the new component.
>
```JS
import PLACESFeature from './PLACESFeature'
import './PLACESFeatureList.css'

function PLACESFeatureList(props) {
    const icons = props.features.map((feature) => {
    return <PLACESFeature key={feature} name={feature} />
  })
    return <div className="PLACESFeatureList">{icons}</div>
}

export default PLACESFeatureList
```


This component imports the `PLACESFeature` component.

This component expects an array of strings named features. We get the array on props as: `props.features`.

The component maps the array of strings into an array `PLACESFeature` components setting the name of each to a feature string from the array.

Add a style sheet.

> [action]
>
> Inside `PLACESFeatures` folder add a new file: `PLACESFeatureList.css`.
>
> Import your styles in `PLACESFeatureList.js`:
>
```JS
import './PLACESFeatureList.css'
```
>
> Then add some styles.
>
```CSS
.PLACESFeatureList {
    display: flex;
}
```


The only style here is flex which should line up all of the elements in a row.

You could add more styles if you like.

## Use the PLACESFeatureList

Use the feature list and feature components.

To use the `PLACESFeature` component you make an instance and set the name prop, fro example:

```JS
<PLACESFeature name="art" />
```

To use the PLACESFeatureList component you need to include an array of strings as the features prop, for example:

```JS
<PLACESFeatureList features={['coffee', 'art']} />
```

Put this to work in the details page.

> [action]
>
> Edit `PLACESDetails.js`
>
```JS
...
import PLACESFeatureList from '../PLACESFeatures/PLACESFeatureList'
>
function PLACESDetails(props) {
    ...
  return (
    <div className="PLACESDetails">
      ...
      <div className="PLACESDetails-info">
        ...
        <PLACESFeatureList features={features}/>
        <p className="PLACESDetails-geo">{ geo.lat } { geo.lon }</p>
      </div>
    </div>
  )
}
```
>
> Be sure to adjust the path to your `PLACESFeatureList` component, it may be in a different location than where I placed mine!
>
> Be sure to remove the previous tag that displayed the features.
```HTML 
{/* <p className="PLACESDetails-features">{ features }</p> */}
```

What happened here? First we imported the PLACESFeatureList component.

Next, make an instance of `PLACESFeatureList` and set the feature proper to the array of feature strings that came from the data source.

Now experiment adding more data to `places-data.json` and adding features.

# Now Commit

> [action]

```bash
$ git add .
$ git commit -m 'displaying features'
$ git push
```
