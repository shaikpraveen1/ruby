# define the list of stores and their coupon discounts
stores = [
  { name: "Store 1", coupons: { "Ingredient A" => 0.1, "Ingredient B" => 0.2 } },
  { name: "Store 2", coupons: { "Ingredient A" => 0.2, "Ingredient C" => 0.3 } },
  { name: "Store 3", coupons: { "Ingredient B" => 0.1, "Ingredient C" => 0.1 } },
  { name: "Store 4", coupons: { "Ingredient C" => 0.2 } },
  { name: "Store 5", coupons: { "Ingredient A" => 0.1, "Ingredient B" => 0.1, "Ingredient C" => 0.1 } }
]

# define the list of recipes and their ingredients
recipes = [
  { name: "Recipe 1", ingredients: { "Ingredient A" => 1, "Ingredient B" => 2 } },
  { name: "Recipe 2", ingredients: { "Ingredient A" => 3, "Ingredient C" => 1 } },
  { name: "Recipe 3", ingredients: { "Ingredient B" => 2, "Ingredient C" => 3 } },
  { name: "Recipe 4", ingredients: { "Ingredient C" => 1 } },
  { name: "Recipe 5", ingredients: { "Ingredient A" => 2, "Ingredient B" => 1, "Ingredient C" => 1 } }
]

# define a method to calculate the total cost of a recipe at a specific store
def calculate_total_cost(store, recipe)
  total_cost = 0

  # iterate through each ingredient in the recipe
  recipe[:ingredients].each do |ingredient, quantity|
    # check if the store has a coupon for the ingredient
    if store[:coupons].key?(ingredient)
      # if the store has a coupon, apply the discount to the cost of the ingredient
      total_cost += quantity * (1 - store[:coupons][ingredient])
    else
      # if the store does not have a coupon, the cost is not discounted
      total_cost += quantity
    end
  end

  total_cost
end

# iterate through each recipe
recipes.each do |recipe|
  # find the store with the lowest total cost for the recipe
  cheapest_store = stores.min_by { |store| calculate_total_cost(store, recipe) }

  # print the name of the cheapest store and the total cost of the recipe
  puts "For #{recipe[:name]}, the cheapest store is #{cheapest_store[:name]} with a total cost of $#{calculate_total_cost(cheapest_store, recipe)}"
end
