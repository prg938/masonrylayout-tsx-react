## About
**masonrylayout-tsx-react** exports MasonryLayout component from *index.tsx*

![GitHub package.json version](https://img.shields.io/github/package-json/v/prg938/masonrylayout-tsx-react)

![images](https://github.com/prg938/masonrylayout-tsx-react/assets/7237762/2b435ea0-63e1-456b-affe-9c6ba3f169e9)


It allows to create grid layout based on columns with auto-placement and optimized usage of Y-space by reducing unnecessary gaps

## NPM
```npm i masonrylayout-tsx-react```

## Requirements

| install | version |
| --- | --- |
| React | >=16.8.0 |
| TypeScript | - |

## flex-wrap vs Masonry Layout

![243689597-fe4dc183-45cf-4fd0-a60f-58f3be590ec0](https://github.com/prg938/masonrylayout-tsx-react/assets/7237762/380fd1a3-67e5-46b8-8d09-88c9631b283f)

## Demo & Usage
#### Demo: http://prg938.vercel.app/masonry
#### Usage: (full code for demo above)
```js
import {FunctionComponent, ReactEventHandler, useRef, useState} from "react"
import MasonryLayout from "masonrylayout-tsx-react"
import type {MasonryLayoutRefType} from "masonrylayout-tsx-react"

/* For Next.js
1. Use dynamic import:
   import dynamic from "next/dynamic"
   const MasonryLayout = dynamic(import('masonrylayout-tsx-react'), {ssr: false})

2. Add to next.config.js
   module.exports = {transpilePackages: ['masonrylayout-tsx-react']}
   https://nextjs.org/docs/architecture/nextjs-compiler#module-transpilation
*/
   

const [box, center, button, fw] = [
  {
    width: '300px',
    padding: '10px',
    border: '1px solid grey'
  },
  {
    display: 'flex',
    justifyContent: 'center',
    alignItems: 'center',
  },
  {
    padding: '10px',
    backgroundColor: 'rebeccapurple',
    color: 'white',
    cursor: 'pointer',
    border: '1px solid transparent',
    margin: '20px 5px'
  },
  {width: '100%'}
]

const key = () => String(Math.random()).split('.')[1]

const initialElements = (updateLayout: ReactEventHandler<any>) => [
  <div key={key()} style={box}>
    <h2>masonrylayout-tsx-react</h2>
    <img onLoad={updateLayout} style={fw} src="https://user-images.githubusercontent.com/7237762/243566394-47b9d96b-cb31-46c8-a9aa-2b9251394d28.jpg" />
    <div>MasonryLayout component for React. Allows to create grid layout based on columns with auto-placement and optimized usage of Y-space by reducing unnecessary gaps</div>
  </div>,
  <div key={key()} style={box}>
    <video onLoadedMetadata={updateLayout} controls={true} autoPlay={true} loop={true} muted style={fw}>
      <source src="https://i.imgur.com/m884zzP.mp4" type="video/mp4" />
    </video>
  </div>,
  <div key={key()} style={box}>
    <h2>Publishing and graphic design</h2>
    <div>In publishing and graphic design, Lorem ipsum is a placeholder text commonly used to demonstrate the visual form of a document or a typeface without relying on meaningful content. Lorem ipsum may be used as a placeholder before final copy is available. It is also used to temporarily replace text in a process called greeking, which allows designers to consider the form of a webpage or publication, without the meaning of the text influencing the design</div>
  </div>,
  <div key={key()} style={box}>
    <h1>Mario game 🎮</h1>
    <b>Mario game using HTML5 Canvas</b>. Still under development. But first 2 levels available!
    <h2>Play <a href='https://prg938.github.io/mariogame' target='_blank'>HERE</a></h2>
  </div>,
  <div key={key()} style={box}>
    <h1>Great image</h1>
    <img onLoad={updateLayout} style={fw} src="https://plus.unsplash.com/premium_photo-1683309568218-bf32f6d904f0?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxlZGl0b3JpYWwtZmVlZHwyNHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=700&q=60" />
    <div>Lorem ipsum is typically a corrupted version of De finibus bonorum et malorum, a 1st-century BC text by the Roman statesman and philosopher Cicero, with words altered, added, and removed to make it nonsensical and improper Latin. The first two words themselves are a truncation of 'dolorem ipsum' ('pain itself')</div>
  </div>,
  <div key={key()} style={box}>
    <a href="https://imgur.com/gvZsB1J">
      <img onLoad={updateLayout} style={fw} src="https://i.imgur.com/gvZsB1J.png" />
    </a>
  </div>,
  <div key={key()} style={box}>
    <h1>😎 Hi</h1>
  </div>
]

const MasonryPage: FunctionComponent<{}> = () => {
  const MasonryLayoutRef = useRef<MasonryLayoutRefType>(null)
  const updateLayout = () => {
    MasonryLayoutRef.current?.layout()
  }
  const [elements, setElements] = useState<JSX.Element[]>(initialElements(updateLayout))
  const add = () => {
    setElements(elements => [<div key={key()} style={box}>🙂</div>, ...elements])
  }
  const remove = () => {
    const newElements = [...elements]
    newElements.shift()
    setElements(elements => newElements)
  }
  const change = () => {
    const newElements = [...elements]
    const newElement = <div key={key()} style={{...box}}>In publishing and graphic design, Lorem ipsum is a placeholder text</div>
    newElements[0] = newElement
    setElements(elements => newElements)
  }
  return <>
    <div style={center}>
      <button style={button} onClick={add}>ADD</button>
      <button style={button} onClick={remove}>REMOVE FIRST</button>
      <button style={button} onClick={change}>CHANGE FIRST</button>
    </div>
    <MasonryLayout forwardedRef={MasonryLayoutRef} animate=".4s ease" justifyContainer="center" gap={10} layoutThrottle={200}>
      {elements}
    </MasonryLayout>
  </>
}
```
## component
```js
<MasonryLayout forwardedRef={MasonryLayoutRef} animate=".4s ease" justifyContainer="center" gap={10} layoutThrottle={200}>
  {elements}
</MasonryLayout>
```
## properties:

| property | type | default | description |
| --- | --- | --- | --- |
| `forwardedRef` | RefObject\<MasonryLayoutRefType\> | none | Provides **layout()** function. Used to layout elements again when the asset is loaded (image/video). This is needed to prevent overlay of the elements when the asset is loaded and the height of its block is changed) |
| `animate` | string | none | To animate elements using CSS-transition. Example: **.4s ease** |
| `justifyContainer` | 'flex-start' \| 'center' \| 'flex-end' | 'flex-start' | Specifies how to place container (in which all elements are nested) |
| `gap` | number | 10 | To create a gap for the elements |
| `layoutThrottle` | number | 250 | Delay after which the **layout()** function is called to layout elements again (when browser's window is resized) | 
