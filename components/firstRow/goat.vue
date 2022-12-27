<template>
    <div class="flex" v-for="coffee in coffees" :key="coffee.id">
      <CardComponent @show-modal="showCardModal = !showCardModal">
        <template v-slot:coffee-image>
          <img class="rounded-t-xl" :src="coffee.doppio.coffeeImg" />
        </template>
  
        <template v-slot:coffee-name>
          <h1>
            {{ coffee.doppio.coffeeTitle }}
          </h1>
        </template>
  
        <template v-slot:coffee-desc>
          <p>
            {{ coffee.doppio.coffeeDesc }}
          </p>
        </template>
  
        <template v-slot:card-modal>
          <ClientOnly>
            <Teleport to="#teleported">
              <CardModal :show="showCardModal" @close="showCardModal = false">
                <template v-slot:modal-title>
                  {{ coffee.doppio.coffeeTitle }}
                </template>
                <!-- ? ingredient list render -->
                <template v-slot:modal-ingredients>
                  <p
                    v-for="ingredient in coffeeIngredients.doppio"
                    :key="ingredient.id"
                  >
                    {{ ingredient }}
                  </p>
                  <br>
                        <p>
                          Возраст: 3 года (молодая)
                        </p>
                </template>
                <!-- ? guide list render -->
                <template v-slot:modal-steps-guide>
                  <li
                    class="mb-4"
                    v-for="guide in coffeeIngredients.doppioGuide"
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
      doppio: {
        coffeeImg: "/img/goat.jpg",
        coffeeTitle: "Коза",
        coffeeDesc:
          "Коза -  домашнее животное, вид парнокопытных из рода горные козлы (Capra) семейства полорогих. ",
      },
    },
  ];
  
  let coffeeIngredients = {
    doppio: [
      "Основная продукция, получаемая от коз — мясо, молоко, мех, шерсть и кожа. По направлению продуктивности породы коз делятся на типы: молочные, шёрстные, пуховые, молочно-мясо-шёрстные. Ангорская коза разводится для получения шерсти. Кашмирская коза и Оренбургская коза разводятся для пуха. В США некоторые хозяйства разводят обморочных коз. Удой обычно составляет 450—550 кг молока жирностью 3,8—4,5 % за лактацию. Настриг шерсти с козлов — 4—6 кг, с маток — 3—5 кг. Длина состригаемой шерсти составляет 15—18 см. Начёс пуха — 0,2—0,5 кг. Срок хозяйственного использования животного обычно достигает 7—8 лет. Из козьих шкур производят кожу высокой выделки — сафьян, шевро.",
    ],
  
  };
  </script>