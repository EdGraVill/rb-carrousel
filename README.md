# Carrousel - React Basics

A React Basics Carrousel component. Stateless, fully optimized with css animations, highly customizable and Mobile support.

## Installation

Into your project's root directory run the following command:


**npm**
```console
npm i -P rb-carrousel
```

**Yarn**
```console
yarn add rb-carrousel
```

This package only has 2 dependencies:

- `react@16.3.0`
- `hammerjs@2.0.8`

## Example

Carrousel is one of the components inside React Basics, so if you want test it, go https://edgravill.github.io/react-basics and see it working.

> The website is under construction

## Usage

Component is stateless, so if you want change carrousel position, the parent component must be able to pass position in Carrousel's prop.

```javascript
import React, { Component } from 'react';
import Carrousel from 'rb-carrousel';
import Button from 'rb-buttons' // <- Good package ;)

class Pictures extends Component {
  state = {
    position: 0,
  };

  data = [{
    alt: 'All the family',
    src: '/img/family.jpg',
  }, {
    alt: 'My girl\'s paint',
    src: '/img/paint.png',
  }, {
    alt: 'Jumping!',
    src: '/img/jumping.gif',
  }, {
    alt: 'Drinking something',
    src: '/img/drinks.jpg',
  }, {
    alt: 'Himalayas right back',
    src: '/img/myFace.jpg',
    onClick() {
      alert('Don\'t click my face :)');
    }
  }];

  goTo(position) {
    this.setState({ position });
  }

  render() {
    return (
      <h1>My vacation pictures</h2>
      <Carrousel
        data={this.data}
        indicator
        indicatorOnClick={position => this.goTo(position)}
        onSwipe={position => this.goTo(position)}
        position={this.state.position}
        style={{
          border: '1px solid #000',
          height: '300px',
          margin: '0 auto',
          width: '90%',
        }}
      />
      <div className="buttons">
        <Button
          onClick={() => goTo(this.state.position - 1)}
          text="Previous"
        />
        <Button
          onClick={() => goTo(this.state.position + 1)}
          text="Next"
        />
      </div>
    );
  }
}
```

The example above includes two particular props: `indicatorOnClick` and `onSwipe`. This props helps to change the position, this doesn't means the component has its state, component still is stateless but has its own methods to calculate next position by gived position and data lenght.

Also `onSwipe` prop means thay Carrousel can handle swipe interactions.

### Thumbnails

Carrousel component accept a children who can be a layer over the images if you put a div with position absolute. Also the package includes its own Thumbnails package. Example below.

```javascript
import React, { Component } from 'react';
import Carrousel, { Thumbnails } from 'rb-carrousel';
import Button from 'rb-buttons' // <- Good package ;)

class Pictures extends Component {
  state = {
    position: 0,
  };

  data = [{
    alt: 'All the family',
    src: '/img/family.jpg',
  }, {
    alt: 'My girl\'s paint',
    src: '/img/paint.png',
  }, {
    alt: 'Jumping!',
    src: '/img/jumping.gif',
  }, {
    alt: 'Drinking something',
    src: '/img/drinks.jpg',
  }, {
    alt: 'Himalayas right back',
    src: '/img/myFace.jpg',
    onClick() {
      alert('Don\'t click my face :)');
    }
  }];

  goTo(position) {
    this.setState({ position });
  }

  render() {
    return (
      <h1>My vacation pictures</h2>
      <Carrousel
        data={this.data}
        indicator
        indicatorOnClick={this.goTo}
        onSwipe={this.goTo}
        position={this.state.position}
        style={{
          border: '1px solid #000',
          height: '300px',
          margin: '0 auto',
          width: '90%',
        }}
      >
        <Thumbnails onClick={this.goTo} />
      </Carrousel>
      <div className="buttons">
        <Button
          onClick={() => this.goTo(this.state.position - 1)}
          text="Previous"
        />
        <Button
          onClick={() => this.goTo(this.state.position + 1)}
          text="Next"
        />
      </div>
    );
  }
}
```

`onClick` prop catch the click in one thumbnail and return its index position.

## API

|Prop|Required|Type|Default|Description|
|----|--------|----|-------|-----------|
|children|`false`|`React$Element<'div'>`|`null`|Layer over images carrousel.|
|data|`true`|`Array<Object>`|`undefined`|Array of the images object. See [Object definition](#data) below.|
|indicator|`false`|`boolean`|`false`|Option to show dots indicator.|
|indicatorOnClick|`false`|`Function`|`undefined`|Function on click a dot. It returns by parameter the index of the dot.|
|onSwipe|`false`|`Function`|`undefined`|Function on swipe the carrousel. It returns by parameter the next position depending the swipe direction.|
|position|`true`|`number`|`0`|Position of the index to show the image.|
|style|`false`|`Object`|`{}`|Style object.|

### data

It takes image object:

|Key|Required|Type|Default|Description|
|---|--------|----|-------|-----------|
|alt|`true`|`string`|`undefined`|Alternative text to img.|
|src|`true`|`string`|`undefined`|Source to img, can be relative to root path, url or base64 encode.|
|onClick|`false`|`Function`|`undefined`|Function to call on image click.|

## Build your own Thumbnails

Your own Thumbnails need support at least 2 props:

|Prop|Required|Type|Default|Description|
|----|--------|----|-------|-----------|
|data|`true`|`Array<Object>`|`undefined`|Array of the images object. See [Object definition](#data) above.|
|position|`true`|`number`|`0`|Position of the index to show the image.|

This props are fed by the Carrousel component so you don't have pass it again.

## Goals

- [x] Support asyn image add.
- [x] Swipe to interact with position.
- [x] Thumbnails component with pan detection.
- [ ] Thumbnails colitions (Under develop).
- [ ] Lazy loading (Under develop).
- [ ] Sopport for div instead of images, this enables videos, other components, etc.

> looking for more? - Do a pull request with your proposals ;)

## Collaborators

- Eduardo Grajales Villanueva @EdGraVill

> If you want to collaborate with this or another exist or new component inside React Basics, first do a pull request and then email me: edgravill@gmail.com

If you want pull request some changes, don't forget build it firt with the following command:

**npm**
```console
npm run build
```

**Yarn**
```console
yarn build
```

Once you're a collaborator don't forget 3 rules:

1. Version are `Mayor` (If APIs are deleted or create new one) `.` `Medium` (If APIs changes without changing name) `.` `Minimum` (If do some hotfix, change Documentation or develop configurations). This is because all 1.x.x are compatible, but are incompatible with 2.x.x
2. Build a great components and do the best documentation as you can.
3. Share with your developer friends. It would be useful for them.

Don't forget [join discussion on Slack](https://join.slack.com/t/react-basics/shared_invite/enQtMzM4MDMyNzM5NjgxLTMxYzcwMDMwYmNkZGIxNWFkZGZhMDVmNWU3OTQ3ZDhlYmZhOWU0NTkwMTdkNzg5ZTJhNWE3MDJlNTc3OGU4YjA)

## License

MIT License

Copyright (c) 2018 Eduardo Grajales Villanueva

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
