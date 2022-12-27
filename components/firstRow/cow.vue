<template>
    <div
      v-for="coffee in coffees"
      :key="coffee.id"
    >
        <CardComponent @show-modal="showCardModal = !showCardModal">
            <template v-slot:coffee-image>
              <img class="rounded-t-xl" :src="coffee.americano.coffeeImg" />
            </template>
    
            <template v-slot:coffee-name>
              <h1>
                {{ coffee.americano.coffeeTitle }}
              </h1>
            </template>
    
            <template v-slot:coffee-desc>
              <p>
                {{ coffee.americano.coffeeDesc }}
              </p>
            </template>
    
            <template v-slot:card-modal>
              <ClientOnly>
    
                <Teleport to="#teleported">
                  <CardModal :show="showCardModal" @close="showCardModal = false">
                    <template v-slot:modal-title> {{ coffee.americano.coffeeTitle }} </template>
                    <!-- ? ingredient list render -->
                    <template v-slot:modal-ingredients>
                        <div
                          v-for="ingredient in coffeeIngredients.americano" 
                          :key="ingredient.id" 
                        >
                          {{ ingredient  }}
                        </div>
                        <br>
                        <p>
                          Возраст: 25 лет (старая)
                        </p>
                    </template>
                    <!-- ? guide list render -->
                    <template v-slot:modal-steps-guide> 
                       <input v-model="waist" type="text">
                       <input v-model="length" type="text">

                       <button @click="calculateAnimal()">Рассчитать</button>

                       <p>
                         {{ waist }}
                        
                       </p>

                       <p>

                         {{ length }}
                       </p>

                       <p>
                        {{result}}
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
let showCardModal = ref(false)



let coffees = [
{
    americano: {
      coffeeImg: `/img/cow.jpg`,
      coffeeTitle: "Корова",
      coffeeDesc:
        "  Масса новорождённых тёлок зависит от породы и составляет 18-45 кг, реже до 60 кг. В отличие от быков, которые обычно весят 300—900 кг, масса взрослых коров всего 200—600 кг, реже до 1000 кг.  ",
    },
}
]

let coffeeIngredients = { 
    americano: [
      "Продолжительность беременности, которую у коров называют стельностью, 250—310 суток. Перед отёлом в течение т. н. сухостойного периода 45-60 суток коров не доят («запускают»). Продолжительность периода лактации (выделения молока) составляет 280—320 суток. Наибольшее количество молока коровы дают во время пятой-шестой лактации. ",

      "Продолжительность жизни составляет около 20 лет (в редких случаях 35), при этом период хозяйственного использования до 12-13 лет, за это время используется 9-12 лактаций. В качестве племенных животных используют 5-10 лет. "
    ],
    
}
</script>