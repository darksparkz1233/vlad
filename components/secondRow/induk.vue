<template>
    <div class="flex" v-for="coffee in coffees" :key="coffee.id">
      <CardComponent @show-modal="showCardModal = !showCardModal">
        <template v-slot:coffee-image>
          <img class="rounded-t-xl" :src="coffee.macchiato.coffeeImg" />
        </template>
  
        <template v-slot:coffee-name>
          <h1>
            {{ coffee.macchiato.coffeeTitle }}
          </h1>
        </template>
  
        <template v-slot:coffee-desc>
          <p class="">
            {{ coffee.macchiato.coffeeDesc }}
          </p>
        </template>
  
        <template v-slot:card-modal>
          <ClientOnly>
            <Teleport to="#teleported">
              <CardModal :show="showCardModal" @close="showCardModal = false">
                <template v-slot:modal-title>
                  {{ coffee.macchiato.coffeeTitle }}
                </template>
                <!-- ? ingredient list render -->
                <template v-slot:modal-ingredients>
                  <p
                    v-for="ingredient in coffeeIngredients.macchiato"
                    :key="ingredient.id"
                  >
                    {{ ingredient }}
                </p>
                <br>
                        <p>
                          Возраст: 2 года (молодой)
                        </p>
                </template>
                <!-- ? guide list render -->
                <template v-slot:modal-steps-guide>
                  <li
                    class="mb-4"
                    v-for="guide in coffeeIngredients.macchiatoGuide"
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
      macchiato: {
        coffeeImg: "/img/induk.jpg",
        coffeeTitle: "Индейка",
        coffeeDesc:
          "Один из распространённых видов домашних птиц из отряда курообразных, который ведёт своё начало от дикой индейки. ",
      },
    },
  ];
  
  let coffeeIngredients = {
    macchiato: [
      "Индейки вообще, и в особенности молодые, весьма чувствительны к холоду и сырости, и потому их разведение в частных хозяйствах идёт успешно только в тёплом и умеренном, более сухом климате, где они зимой могут содержаться в хорошо проконопаченных, хотя и не отапливаемых птичниках, защищённых от северных ветров. С южной стороны птичника, в стене на высоте 10—15 см от пола, устраивают лазы для выхода птицы из помещения. Дворик возле птичника, куда выпускают индеек, должен быть возможно просторнее, так как индейки, как и гуси, любят простор и без выгулов здоровье этой птице нельзя гарантировать."
    ],
  };
  </script>