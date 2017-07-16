# React Simple Chatbot

<a href="https://travis-ci.org/LucasBassetti/react-simple-chatbot"><img src="https://travis-ci.org/LucasBassetti/react-simple-chatbot.svg?branch=master" alt="Travis CI" /></a> <a href="https://badge.fury.io/js/react-simple-chatbot"><img src="https://badge.fury.io/js/react-simple-chatbot.svg" alt="npm version"></a>
  <img src="https://codecov.io/gh/LucasBassetti/react-simple-chatbot/branch/master/graph/badge.svg" alt="Codecov" />
</a>

A simple chatbot component to create conversation chats

<img src="https://cloud.githubusercontent.com/assets/1014326/25716667/2d4bb4c4-30d6-11e7-996e-30c8fb316361.gif" height="400" />

## Contents
- [Getting Started](#getting-started)
- [Usage](#usage)
- [Documentation](#documentation)
  - [Properties](#properties)
  - [Steps](#steps)
  - [Custom Component](#custom-component)
- [How to Contribute](#how-to-contribute)

## Getting Start

```bash
npm install react-simple-chatbot --save
```

## Usage

There are several examples on the [website](http://lucasbassetti.com.br/react-simple-chatbot). Here is the first one to get you started:

``` javascript
import ChatBot from 'react-simple-chatbot';

const steps = [
  {
    id: '0',
    message: 'Welcome to react chatbot!',
    trigger: '1',
  },
  {
    id: '1',
    message: 'Bye!',
    end: true,
  },
];

ReactDOM.render(
  <div>
    <ChatBot steps={steps} />
  </div>,
  document.getElementById('root')
);
```

## Build with `react-simple-chatbot`

1. [Seth Loh Website](https://github.com/lackdaz/lackdaz.github.io) - Personal website of Seth Loh ([demo](https://www.sethloh.com))

## Documentation

### Properties

| Name | Type | Default | Description |
|---|---|---|---|
| `avatarStyle` | `PropTypes.object` | | The style object to use to override the avatar element |
| `botAvatar` | `PropTypes.string` | `img` | Bot image source |
| `botBubbleColor` | `PropTypes.string` | `#6e48aa` | Color of bot bubble color |
| `botDelay` | `PropTypes.number` | `1000` | The delay time of bot messages |
| `botFontColor` | `PropTypes.string` | `#fff` | Color of bot font color |
| `bubbleStyle` | `PropTypes.object` | | The style object to use to override the bubble element |
| `className` | `PropTypes.string` | | Add a class name to root element |
| `contentStyle` | `PropTypes.object` | | The style object to use to override the scroll element |
| `customDelay` | `PropTypes.number` | `1000` | The delay time of custom messages |
| `customStyle` | `PropTypes.object	` | | The style object to use to override the custom step element |
| `floating` | `PropTypes.bool`  | `false` | Render chatbot with a floating button |
| `footerStyle` | `PropTypes.object`  | | The style object to use to override the footer element |
| `handleEnd({ renderedSteps, steps, values })` | `PropTypes.func`  | | The callback function when chat ends |
| `headerBgColor` | `PropTypes.string`  | `#6e48aa` | Backgroud color of header element |
| `headerComponent` | `PropTypes.element`  | | Override the default header element |
| `headerFontColor` | `PropTypes.string`  | `#fff` | Font color of header element |
| `headerTitle` | `PropTypes.string`  | `Chat` | Override header title |
| `hideBotAvatar` | `PropTypes.bool`  | `false` | If true the bot avatar will be hidden in all steps |
| `hideHeader` | `PropTypes.bool`  | `false` | If true the header will be hidden |
| `hideUserAvatar` | `PropTypes.bool`  | `false` | If true the user avatar will be hidden in all steps |
| `inputStyle` | `PropTypes.object`  | | The style object to use to override the input element |
| `opened` | `PropTypes.bool`  | `undefined` | Override the default opened state. This prop can just be used if floating is true. You must use the callback prop toggleFloating to update the opened prop |
| `steps` | `PropTypes.array`  | | The chatbot steps to display |
| `style` | `PropTypes.object`  | | The style object to use to override the root element |
| `toggleFloating` | `PropTypes.func`  | `undefined` | Must be used with opened prop. You must use it to change your opened prop using your custom function like myToggleFloating({ opened }) |
| `userAvatar` | `PropTypes.string`  | `img` | User image source |
| `userBubbleColor` | `PropTypes.string`  | `#fff` | Color of user bubble color |
| `userDelay` | `PropTypes.number`  | `1000` | The delay time of user messages |
| `userFontColor` | `PropTypes.string`  | `#4a4a4a` | Color of user font color |

### Steps

#### Text Step

| Name | Type | Required | Description |
|---|---|---|---|
| `id` | `String / Number` | `true` | The step id. Required for any step |
| `message` | `String` | `true` | The text message |
| `trigger` | `String / Number` | `false` | The id of next step to be triggered |
| `avatar` | `String` | `false` | the avatar to be showed just in this step. Note: this step must be a step that avatar appears |
| `end` | `Boolean` | `false` | if true indicate that this step is the last |

Example:

``` js
{
  id: '1',
  message: 'Hello World',
  end: true,
}
```

#### User Step

| Name | Type | Required | Description |
|---|---|---|---|
| `id` | `String / Number` | `true` | The step id. Required for any step |
| `user` | `Boolean` | `true` | if true indicate that you waiting a user type action |
| `trigger` | `String / Number` | `false` | The id of next step to be triggered |
| `validator` | `String / Number` | `false` | if user attribute is true you can pass a validator function to validate the text typed by the user |
| `end` | `Boolean` | `false` | if true indicate that this step is the last |

Example:

``` js
{
  id: '1',
  user: true,
  end: true,
}
```

#### Options Step

| Name | Type | Required | Description |
|---|---|---|---|
| `id` | `String / Number` | `true` | The step id. Required for any step |
| `options` | `Array` | `true` | Array of options with { label, value, trigger } properties |
| `end` | `Boolean` | `false` | if true indicate that this step is the last |

Example:

``` js
{
  id: '1',
  options: [
    { value: 1, label: 'Number 1', trigger: '3' },
    { value: 2, label: 'Number 2', trigger: '2' },
    { value: 3, label: 'Number 3', trigger: '2' },
  ],
}
```

#### Custom Step

| Name | Type | Required | Description |
|---|---|---|---|
| `id` | `String / Number` | `true` | The step id. Required for any step |
| `component` | `Component` | `true` | Custom React Component |
| `replace` | `Boolean` | `false` | if true indicate that component will be replaced by the next step |
| `waitAction` | `Boolean` | `false` | if true indicate that you waiting some action. You must use the triggerNextStep prop in your component to execute the action |
| `asMessage` | `Boolean` | `false` | f true indicate that the component will be displayed as a text step
| `trigger` | `String / Number` | `false` | The id of next step to be triggered |
| `end` | `Boolean` | `false` | if true indicate that this step is the last |

Example:

``` js
{
  id: '1',
  component: <CustomComponent />
  trigger: '2'
}
```

#### Update Step

| Name | Type | Required | Description |
|---|---|---|---|
| `id` | `String / Number` | `true` | The step id. Required for any step |
| `update` | `String / Number` | `true` | The id of next step to be updated |
| `trigger` | `String / Number` | `false` | The id of next step to be triggered |

Example:

``` js
{
  id: '1',
  options: [
    { value: 1, label: 'Number 1', trigger: '3' },
    { value: 2, label: 'Number 2', trigger: '2' },
    { value: 3, label: 'Number 3', trigger: '2' },
  ],
}
```

#### Custom Component

When you declare a custom step, you need indicate a custom React Component to be rendered in the chat. This custom component will receive the following properties.

| Name | Type | Description |
|---|---|---|
| `previousStep` | `PropTypes.object` | Previous step rendered |
| `step` | `PropTypes.object` | Current step rendered |
| `steps` | `PropTypes.object` | All steps rendered |
| `triggerNextStep({ value, trigger })` | `PropTypes.func` | Callback function to trigger next step when user attribute is true. Optionally you can pass a object with value to be setted in the step and the next step to be triggered |

## How to Contribute

Please check the [contributing guide](https://github.com/LucasBassetti/react-simple-chatbot/blob/master/contributing.md)

## License

MIT · [Lucas Bassetti](http://lucasbassetti.com.br)
