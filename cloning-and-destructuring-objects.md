# Cloning and Destructuring

Say we have an object with deeply nested data, and we want to make a copy that only changes one of the deeply nested properties.
```js
const data = {
    page: {
      card: {
        cardType: {
          typeA: {
            cardTypeAData: {
              name: "Card Type A",
              id: 1,
              color: "blue", // we want to change this to "red"
             }
           }
         }
      }
   }
}

```

Use spread operator to destructure each property all the way down:
```js
 const copy = {
    ...data,
    page: {
        ...data.page,
        card: {
            ...data.page.card,
            cardType: {
                ...data.page.card.cardType,
                typeA: {
                    ...data.page.card.cardType.typeA,
                    cardTypeAData: {
                        ...data.page.card.cardType.typeA.cardTypeAData,
                        color: "red",
                    }
                }
            }
        }
    }
}
