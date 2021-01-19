[![Latest Stable Version](https://poser.pugx.org/codeq/neos-link/v/stable)](https://packagist.org/packages/codeq/neos-link)
[![License](https://poser.pugx.org/codeq/neos-link/license)](LICENSE)

# CodeQ.Link

# WIP: This code needs to be cleaned up and tested.

## Link helper for Neos - with Atomic.Fusion & Monocle in mind

[Carbon.Link](https://github.com/CarbonPackages/Carbon.Link) is great for rendering links with just 
`<Carbon.Link:Link node={props.node}>Read more</Carbon.Link:Link>`, but does not work well with 
[Sitegeist.Monocle](https://github.com/sitegeist/Sitegeist.Monocle).

By providing a transfer object instead, we implement Carbon.Link functionality with Monocle in mind. What does such 
a transfer object consist of:

```
Neos.Fusion:DataStructure {
    link = '/'
    label = 'Home'
    rel = false
    target = '_blank'
}
```

By separating the aspects of link types and rendering we enable the separation of those aspects into different 
fusion-components.

## Installation

CodeQ.Link is available via packagist run `composer require codeq/link`.
We use semantic versioning so every breaking change will increase the major-version number.

## Usage

#### Rendering one link

#### For an individual link we provide these mappers:

- `CodeQ.Link:DummyLink`
- ```
  CodeQ.Link:NodeLink {
    node = ${node}
    backendLink = false
  }
  ```
- `CodeQ.Link:StringLink { link = 'asset://XXX' }`

#### Usage:

```
link = CodeQ.Link:DummyLink

renderer = afx`
    <CodeQ.Link:Tag link={props.link} attributes.class="my-class">Read more</CodeQ.Link:Tag>
    <CodeQ.Link:Tag link={props.link} />
    <CodeQ.Link:Tag link={props.link} renderDefaultTagIfNoLink={true} defaultTagName="span">Link or Span</CodeQ.Link:Tag>
```


#### Rendering one link structures (WIP: Not fully consistent with above api yet)

#### For menus you typically want to render a list or tree of nodes, for this we provide the following usefull mappers

 - `CodeQ.Link:DummyMenuItems`
 - ```
   CodeQ.Link:NeosMenuItems {
     startingPoint = ${site}
     maximumLevels = 2
   }
   ```
- `CodeQ.Link:DummyReferences`
- `CodeQ.Link:NodeReferences { nodes = ${q(site).property('nodes')} }`

#### Usage:

```
menuItems = CodeQ.Link:DummyMenuItems

renderer = afx`
    <ul class="menu">
        <Neos.Fusion:Loop items={props.menuItems} itemName="menuItem" @children="itemRenderer">
            <li class={'navigation-item ' + (menuItem.state ? 'navigation-item--state-' + menuItem.state : '') }>
                <CodeQ.Link:Tag link={menuItem} />
            </li>
        </Neos.Fusion:Loop>
    </ul>
`
```


## License

Licensed under MIT, see [LICENSE](LICENSE)

## Sponsors & Contribution

The development of this plugin was kindly sponsored by [Code Q](http://codeq.at/).

We will gladly accept contributions. Please send us pull requests.
