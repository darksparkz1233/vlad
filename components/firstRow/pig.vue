<template>
  <div class="flex" v-for="coffee in coffees" :key="coffee.id">
    <CardComponent @show-modal="showCardModal = !showCardModal">
      <template v-slot:coffee-image>
        <img class="rounded-t-xl" :src="coffee.mocha.coffeeImg" />
      </template>

      <template v-slot:coffee-name>
        <h1>
          {{ coffee.mocha.coffeeTitle }}
        </h1>
      </template>

      <template v-slot:coffee-desc>
        <p class="">
          {{ coffee.mocha.coffeeDesc }}
        </p>
      </template>

      <template v-slot:card-modal>
        <ClientOnly>
          <Teleport to="#teleported">
            <CardModal :show="showCardModal" @close="showCardModal = false">
              <template v-slot:modal-title>
                {{ coffee.mocha.coffeeTitle }}
              </template>
              <!-- ? ingredient list render -->
              <template v-slot:modal-ingredients>
                <p
                  v-for="ingredient in coffeeIngredients.mocha"
                  :key="ingredient.id"
                >
                  {{ ingredient }}
                </p>
                <br>
                        <p>
                          Возраст: 34 года (старая)
                        </p>
              </template>
              <!-- ? guide list render -->
              <template v-slot:modal-steps-guide>
                <li
                  class="mb-4"
                  v-for="guide in coffeeIngredients.mochaGuide"
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
    mocha: {
      coffeeImg: "/img/pig.jpg",
      coffeeTitle: "Домашняя свинья",
      coffeeDesc:
        "Крупное парнокопытное, разновидность кабана, одомашненная человеком около 7000 лет назад и распространённая главным образом в странах Запада, в Восточной Азии и в Океании.  ",
    },
  },
];

let coffeeIngredients = {
  mocha: [
    "Свинина является одним из основных видов мяса во многих странах мира. На вид мясо свиньи имеет бледно-розовую окраску, содержит заметные прослойки жира. По вкусовым качествам свинина отличается бо́льшей мягкостью и жирностью в сравнении с говядиной и бараниной. В пищу обычно употребляется мясо самок свиньи, или (реже) боровов, кастрированных до начала полового созревания. Мясо хряков-производителей также годно в пищу, однако оно обладает существенно худшими вкусовыми качествами.",

  ],

};
</script>