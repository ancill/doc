# Next.js

## Преимущества

- SSG, SSR и инкрементальная статическая генерация
- Оптимизация изображений
- Роутинг + интернализация
- Code-splitting
- Поддержка TS
- CSS modules and SASS
- Fast refresh for development


## Typescript

### Зачем нужны интерфейсы?

- Можно экстендить интерфейс
- Лучше всегда использовать интерфейс, типы только по необходимости когда есть разные типы `type stringOrNumber = string | number;`

```ts
type Point = {
	x:number,
	y:number
}
type D3Point = Point & {
	z: number;
}

interface IPoint {
	x:number,
	y:number
}

interface I3DPoint extends IPoint {
	z: number;
}

type stringOrNumber = string | number;

function print(coord: I3DPoint) {

}

```


### Commands
create next app

`npx create-next-app [project name] --use-npm`

add types to it

`npm i -D typescript @types/react @types/node`

additional eslint types
`npm i -D eslint @typescript-eslint/parser @typescript-eslint/eslint-plugin`

`npm i -D stylelint stylelint-config-standard stylelint-order stylelint-order-config-standard`


### React
![](2022-04-13-15-41-00.png)
