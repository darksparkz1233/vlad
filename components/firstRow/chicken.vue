<template>
    <div class="flex" v-for="coffee in coffees" :key="coffee.id">
      <CardComponent @show-modal="showCardModal = !showCardModal">
        <template v-slot:coffee-image>
          <img class="rounded-t-xl" :src="coffee.cappuccino.coffeeImg" />
        </template>
  
        <template v-slot:coffee-name>
          <h1>
            {{ coffee.cappuccino.coffeeTitle }}
          </h1>
        </template>
  
        <template v-slot:coffee-desc>
          <p class="">
            {{ coffee.cappuccino.coffeeDesc }}
          </p>
        </template>
  
        <template v-slot:card-modal>
          <ClientOnly>
            <Teleport to="#teleported">
              <CardModal :show="showCardModal" @close="showCardModal = false">
                <template v-slot:modal-title>
                  {{ coffee.cappuccino.coffeeTitle }}
                </template>
                <!-- ? ingredient list render -->
                <template v-slot:modal-ingredients>
                  <p
                    v-for="ingredient in coffeeIngredients.cappuccino"
                    :key="ingredient.id"
                  >
                    {{ ingredient }}
                  </p>
                  <br>
                  <p>
                    Возраст: 1 год (молодая)
                  </p>
                </template>
              </CardModal>
            </Teleport>
          </ClientOnly>
        </template>
      </CardComponent>
    </div>
  </template>
  
  <script setup>
  let showCardModal = ref(false);
  
  let coffees = [
    {
      cappuccino: {
        coffeeImg: "./img/chicken.jpg",
        coffeeTitle: "Курица",
        coffeeDesc:
          "Домашняя курица - самая многочисленная и распространённая домашняя птица, а в XXI веке — самый многочисленный на Земле вид птиц. ",
      },
    },
  ];
  
  let coffeeIngredients = {
    cappuccino: [
      "В домашних хозяйствах основным кормом курам служат разные виды зерновых, из которых овёс, ячмень, гречиха и просо наиболее употребительны. Ими можно кормить кур в течение целого года без вреда для их здоровья и продуктивности. Часто куры роют землю в поисках крупных насекомых, личинок и семян. Прибавка к зерновому корму в небольшом количестве зелени и животной пищи (в прошлом, например, конины, сушёных майских жуков), когда птицы не выгуливаются и не могут отыскивать червей и клевать травы самостоятельно, полезна: она увеличивает яйценоскость."
    ],
  };
  </script>
