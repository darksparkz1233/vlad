<template>
    <div class="flex" v-for="coffee in coffees" :key="coffee.id">
      <CardComponent @show-modal="showCardModal = !showCardModal">
        <template v-slot:coffee-image>
          <img class="rounded-t-xl" :src="coffee.flatWhite.coffeeImg" />
        </template>
  
        <template v-slot:coffee-name>
          <h1>
            {{ coffee.flatWhite.coffeeTitle }}
          </h1>
        </template>
  
        <template v-slot:coffee-desc>
          <p class="">
            {{ coffee.flatWhite.coffeeDesc }}
          </p>
        </template>
  
        <template v-slot:card-modal>
          <ClientOnly>
            <Teleport to="#teleported">
              <CardModal :show="showCardModal" @close="showCardModal = false">
                <template v-slot:modal-title>
                  {{ coffee.flatWhite.coffeeTitle }}
                </template>
                <!-- ? ingredient list render -->
                <template v-slot:modal-ingredients>
                  <p
                    v-for="ingredient in coffeeIngredients.flatWhite"
                    :key="ingredient.id"
                  >
                    {{ ingredient }}
                  </p>
                  <br>
                        <p>
                          Возраст: 13 лет (старая)
                        </p>
                </template>
                <!-- ? guide list render -->
                <template v-slot:modal-steps-guide>
                  <li
                    class="mb-4"
                    v-for="guide in coffeeIngredients.flatWhiteGuide"
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
      flatWhite: {
        coffeeImg: "/img/sheep.jpg",
        coffeeTitle: "Домашняя овца",
        coffeeDesc:
          "Парнокопытное млекопитающее из рода баранов, семейства полорогих. Это животное уже в глубокой древности было одомашнено человеком, в основном из-за густой шерсти и съедобного мяса.",
      },
    },
  ];
  
  let coffeeIngredients = {
    flatWhite: [
      "Размер и вес домашних овец сильно различается в зависимости от породы. Скорость роста и масса взрослого животного во многом зависят от наследственности, и по этой причине селекционный отбор часто производится на основании этих характеристик Взрослые самки обычно весят 45—100 кг, тогда как более крупные самцы 70—160 кг. Рекордный вес барана (саффолкской породы) достигал 247,2 кг. В целом высота в холке у животных составляет 55-100 см, а длина тела — 60—110 см. Мор  да в нижней части заострённая, имеет прямой или иногда горбоносый профиль, почти полностью (за исключением губ и краёв ноздрей) покрыта тонкой шерстью. "
    ],
  
   
  };
  </script>