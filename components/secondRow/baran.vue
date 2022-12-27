<template>
    <div class="flex" v-for="coffee in coffees" :key="coffee.id">
      <CardComponent @show-modal="showCardModal = !showCardModal">
        <template v-slot:coffee-image>
          <img class="rounded-t-xl" :src="coffee.irish.coffeeImg" />
        </template>
  
        <template v-slot:coffee-name>
          <h1>
            {{ coffee.irish.coffeeTitle }}
          </h1>
        </template>
  
        <template v-slot:coffee-desc>
          <p class="">
            {{ coffee.irish.coffeeDesc }}
          </p>
        </template>
  
        <template v-slot:card-modal>
          <ClientOnly>
            <Teleport to="#teleported">
              <CardModal :show="showCardModal" @close="showCardModal = false">
                <template v-slot:modal-title>
                  {{ coffee.irish.coffeeTitle }}
                </template>
                <!-- ? ingredient list render -->
                <template v-slot:modal-ingredients>
                  <p
                    v-for="ingredient in coffeeIngredients.irish"
                    :key="ingredient.id"
                  >
                    {{ ingredient }}
                  </p>
                  <br>
                        <p>
                          Возраст: 5 лет (молодой)
                        </p>
                </template>
                <!-- ? guide list render -->
                <template v-slot:modal-steps-guide>
                  <li
                    class="mb-4"
                    v-for="guide in coffeeIngredients.irishGuide"
                    :key="guide.id"
                  >
                    {{ guide }}
                  </li>
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
      irish: {
        coffeeImg: "/img/baran.jpg",
        coffeeTitle: "Баран",
        coffeeDesc:
          "Бараны достигают длины от 1,4 до 1,8 м, хвост длиной от 7 до 15 см. Высота в плечах от 65 до 125 см, вес — от 20 до 200 кг, причём самцы всегда значительно массивнее самок.",
      },
    },
  ];
  
  let coffeeIngredients = {
    irish: [
      "Бараны ведут дневной образ жизни, однако в особо жаркие дни удаляются на отдых в тенистые места и переносят поиск пищи на вечернее или ночное время. Самки и молодняк образуют небольшие стада, которые иногда объединяются в более крупные. Самцы большинство времени живут отдельно от самок, ведя либо одиночный образ жизни, либо являясь частью исключительно мужской группы. Внутри такой группы существует строгая иерархия, устанавливаемая в зависимости от величины рогов либо в прямых поединках. Бараны — растительноядные животные и питаются главным образом травами. "
    ],
  };
  </script>