<template>
  <div class="flex" v-for="coffee in coffees" :key="coffee.id">
    <CardComponent @show-modal="showCardModal = !showCardModal">
      <template v-slot:coffee-image>
        <img class="h-full rounded-t-xl " :src="coffee.bicerin.coffeeImg" />
      </template>

      <template v-slot:coffee-name>
        <h1>
          {{ coffee.bicerin.coffeeTitle }}
        </h1>
      </template>

      <template v-slot:coffee-desc>
        <p class="">
          {{ coffee.bicerin.coffeeDesc }}
        </p>
      </template>

      <template v-slot:card-modal>
        <ClientOnly>
          <Teleport to="#teleported">
            <CardModal :show="showCardModal" @close="showCardModal = false">
              <template v-slot:modal-title>
                {{ coffee.bicerin.coffeeTitle }}
              </template>
              <!-- ? ingredient list render -->
              <template v-slot:modal-ingredients>
                <p v-for="ingredient in coffeeIngredients.bicerin" :key="ingredient.id">
                  {{ ingredient }}
                </p>
                <br>
                        <p>
                          Возраст: 19 лет (старый)
                        </p>
              </template>
              <!-- ? guide list render -->
              <template v-slot:modal-steps-guide>
                <li class="mb-4" v-for="guide in coffeeIngredients.bicerinGuide" :key="guide.id">
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
    bicerin: {
      coffeeImg: "/img/bull.jpg",
      coffeeTitle: "Бык",
      coffeeDesc:
        "Систематическая группа полорогих парнокопытных млекопитающих, в настоящее время имеющая таксономический ранг трибы в подсемействе Bovinae",
    },
  },
];

let coffeeIngredients = {
  bicerin: [
    "Раньше быки были единственными представителями подсемейства Bovinae, но после новых генетических исследований в него зачислили также и винторогих антилоп. Быков насчитывается 13 видов, из которых один обитает в Европе (ещё один в дикой природе уже вымер), один в Африке, один в Северной Америке, остальные в Азии. Ещё несколько видов быков вымерли в историческое время. Кроме того, известно несколько ископаемых видов быков. "
  ],

};
</script>