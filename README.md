What interests me most is how the properties of the dish - (nutritional info, prep time, etc) effects how users rate the recipe.

I personally have a tendency to enjoy foods high in sugars & fats, and was curious to learn: *Does the amount of sugar in a recipe influence the rating of the dish?* During my journey to answering this question, I also discovered correlations between certain nutritional contents and overall calories. 

This dataset as well as my analysis provides insights into the shared activity of creating meals that humans have been participating in for millions of years. Because recipes have been repeated to note their corresponding rating/review, this dataset contains 234,429 rows and 23 columns. Some columns of interest include 'ratings'-(floats between 0-5), 'calories'-(shown as floats), 'sugar (PDV)'-(Amount of Sugar in the dish represented by percent of daily value).

--- 

## Cleaning & Exploratory Data Analysis 
<br>
The Dataset I am working with is a result of two seperate datasets - A `recipes` dataset and a `reviews` dataset containing reviews for the recipes. These datasets were merged together based on the recipe id, resulting in duplicate recipe rows for each review, something that I had to keep in mind while working with the data. 

Once merged, I replaced the recipes with a rating of '0' with null values, as the lowest you can give a recipie is 1 star. The only way a recipe could be rated '0' would be if the review didn't include a rating or the recipe has no reviews. If the rating doesn't exist, a null value will better represent the dish's rating and makes calculating the average rating of a recipe more accurate as the 0's won't drag down the average. 

After calculating the `'avg rating'` column, I got to work converting columns into their proper values. Dates into DateTime objects, Strings representing lists into actual lists, and dropping the duplicate ID column. Finally, to make my life easier when answering my question, I changed the `'nutrition'` column containing various nutritional info about the recipie in a list into their own seperate columns: `'total fat (PDV)'`, `'sugar (PDV)'`, `'sodium (PDV)'`, `'protein (PDV)'`, `'saturated fat (PDV)'`, `'carbohydrates (PDV)'`.


<br>
<br>

**Let's take a look at our cleaned dataframe!**

<table border="1" class="dataframe" style="width: 50%">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>name</th>
      <th>id</th>
      <th>minutes</th>
      <th>contributor_id</th>
      <th>submitted</th>
      <th>tags</th>
      <th>n_steps</th>
      <th>steps</th>
      <th>description</th>
      <th>ingredients</th>
      <th>n_ingredients</th>
      <th>user_id</th>
      <th>date</th>
      <th>rating</th>
      <th>review</th>
      <th>avg rating</th>
      <th>calories (#)</th>
      <th>total fat (PDV)</th>
      <th>sugar (PDV)</th>
      <th>sodium (PDV)</th>
      <th>protein (PDV)</th>
      <th>saturated fat (PDV)</th>
      <th>carbohydrates (PDV)</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1 brownies in the world    best ever</td>
      <td>333281</td>
      <td>40</td>
      <td>985201</td>
      <td>2008-10-27</td>
      <td>[60-minutes-or-less,  time-to-make,  course,  main-ingredient,  preparation,  for-large-groups,  desserts,  lunch,  snacks,  cookies-and-brownies,  chocolate,  bar-cookies,  brownies,  number-of-servings]</td>
      <td>10</td>
      <td>['heat the oven to 350f and arrange the rack in the middle', 'line an 8-by-8-inch glass baking dish with aluminum foil', 'combine chocolate and butter in a medium saucepan and cook over medium-low heat , stirring frequently , until evenly melted', 'remove from heat and let cool to room temperature', 'combine eggs , sugar , cocoa powder , vanilla extract , espresso , and salt in a large bowl and briefly stir until just evenly incorporated', 'add cooled chocolate and mix until uniform in color', 'add flour and stir until just incorporated', 'transfer batter to the prepared baking dish', 'bake until a tester inserted in the center of the brownies comes out clean , about 25 to 30 minutes', 'remove from the oven and cool completely before cutting']</td>
      <td>these are the most; chocolatey, moist, rich, dense, fudgy, delicious brownies that you'll ever make.....sereiously! there's no doubt that these will be your fav brownies ever for you can add things to them or make them plain.....either way they're pure heaven!</td>
      <td>[bittersweet chocolate,  unsalted butter,  eggs,  granulated sugar,  unsweetened cocoa powder,  vanilla extract,  brewed espresso,  kosher salt,  all-purpose flour]</td>
      <td>9</td>
      <td>386585.0</td>
      <td>2008-11-19</td>
      <td>4.0</td>
      <td>These were pretty good, but took forever to bake.  I would send it ended up being almost an hour!  Even then, the brownies stuck to the foil, and were on the overly moist side and not easy to cut.  They did taste quite rich, though!  Made for My 3 Chefs.</td>
      <td>4.0</td>
      <td>138.4</td>
      <td>10.0</td>
      <td>50.0</td>
      <td>3.0</td>
      <td>3.0</td>
      <td>19.0</td>
      <td>6.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1 in canada chocolate chip cookies</td>
      <td>453467</td>
      <td>45</td>
      <td>1848091</td>
      <td>2011-04-11</td>
      <td>[60-minutes-or-less,  time-to-make,  cuisine,  preparation,  north-american,  for-large-groups,  canadian,  british-columbian,  number-of-servings]</td>
      <td>12</td>
      <td>['pre-heat oven the 350 degrees f', 'in a mixing bowl , sift together the flours and baking powder', 'set aside', 'in another mixing bowl , blend together the sugars , margarine , and salt until light and fluffy', 'add the eggs , water , and vanilla to the margarine / sugar mixture and mix together until well combined', 'add in the flour mixture to the wet ingredients and blend until combined', 'scrape down the sides of the bowl and add the chocolate chips', 'mix until combined', 'scrape down the sides to the bowl again', 'using an ice cream scoop , scoop evenly rounded balls of dough and place of cookie sheet about 1 - 2 inches apart to allow for spreading during baking', 'bake for 10 - 15 minutes or until golden brown on the outside and soft &amp; chewy in the center', 'serve hot and enjoy !']</td>
      <td>this is the recipe that we use at my school cafeteria for chocolate chip cookies. they must be the best chocolate chip cookies i have ever had! if you don't have margarine or don't like it, then just use butter (softened) instead.</td>
      <td>[white sugar,  brown sugar,  salt,  margarine,  eggs,  vanilla,  water,  all-purpose flour,  whole wheat flour,  baking soda,  chocolate chips]</td>
      <td>11</td>
      <td>424680.0</td>
      <td>2012-01-26</td>
      <td>5.0</td>
      <td>Originally I was gonna cut the recipe in half (just the 2 of us here), but then we had a park-wide yard sale, &amp; I made the whole batch &amp; used them as enticements for potential buyers ~ what the hey, a free cookie as delicious as these are, definitely works its magic! Will be making these again, for sure! Thanks for posting the recipe!</td>
      <td>5.0</td>
      <td>595.1</td>
      <td>46.0</td>
      <td>211.0</td>
      <td>22.0</td>
      <td>13.0</td>
      <td>51.0</td>
      <td>26.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>412 broccoli casserole</td>
      <td>306168</td>
      <td>40</td>
      <td>50969</td>
      <td>2008-05-30</td>
      <td>[60-minutes-or-less,  time-to-make,  course,  main-ingredient,  preparation,  side-dishes,  vegetables,  easy,  beginner-cook,  broccoli]</td>
      <td>6</td>
      <td>['preheat oven to 350 degrees', 'spray a 2 quart baking dish with cooking spray , set aside', 'in a large bowl mix together broccoli , soup , one cup of cheese , garlic powder , pepper , salt , milk , 1 cup of french onions , and soy sauce', 'pour into baking dish , sprinkle remaining cheese over top', 'bake for 25 minutes or until cheese is lightly browned', 'sprinkle with rest of french fried onions and bake until onions are browned and cheese is bubbly , about 10 more minutes']</td>
      <td>since there are already 411 recipes for broccoli casserole posted to "zaar" ,i decided to call this one  #412 broccoli casserole.i don't think there are any like this one in the database. i based this one on the famous "green bean casserole" from campbell's soup. but i think mine is better since i don't like cream of mushroom soup.submitted to "zaar" on may 28th,2008</td>
      <td>[frozen broccoli cuts,  cream of chicken soup,  sharp cheddar cheese,  garlic powder,  ground black pepper,  salt,  milk,  soy sauce,  french-fried onions]</td>
      <td>9</td>
      <td>29782.0</td>
      <td>2008-12-31</td>
      <td>5.0</td>
      <td>This was one of the best broccoli casseroles that I have ever made.  I made my own chicken soup for this recipe. I was a bit worried about the tsp of soy sauce but it gave the casserole the best flavor. YUM!  \nThe photos you took (shapeweaver) inspired me to make this recipe and it actually does look just like them when it comes out of the oven.  \nThanks so much for sharing your recipe shapeweaver. It was wonderful!  Going into my family's favorite Zaar cookbook :)</td>
      <td>5.0</td>
      <td>194.8</td>
      <td>20.0</td>
      <td>6.0</td>
      <td>32.0</td>
      <td>22.0</td>
      <td>36.0</td>
      <td>3.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>412 broccoli casserole</td>
      <td>306168</td>
      <td>40</td>
      <td>50969</td>
      <td>2008-05-30</td>
      <td>[60-minutes-or-less,  time-to-make,  course,  main-ingredient,  preparation,  side-dishes,  vegetables,  easy,  beginner-cook,  broccoli]</td>
      <td>6</td>
      <td>['preheat oven to 350 degrees', 'spray a 2 quart baking dish with cooking spray , set aside', 'in a large bowl mix together broccoli , soup , one cup of cheese , garlic powder , pepper , salt , milk , 1 cup of french onions , and soy sauce', 'pour into baking dish , sprinkle remaining cheese over top', 'bake for 25 minutes or until cheese is lightly browned', 'sprinkle with rest of french fried onions and bake until onions are browned and cheese is bubbly , about 10 more minutes']</td>
      <td>since there are already 411 recipes for broccoli casserole posted to "zaar" ,i decided to call this one  #412 broccoli casserole.i don't think there are any like this one in the database. i based this one on the famous "green bean casserole" from campbell's soup. but i think mine is better since i don't like cream of mushroom soup.submitted to "zaar" on may 28th,2008</td>
      <td>[frozen broccoli cuts,  cream of chicken soup,  sharp cheddar cheese,  garlic powder,  ground black pepper,  salt,  milk,  soy sauce,  french-fried onions]</td>
      <td>9</td>
      <td>1196280.0</td>
      <td>2009-04-13</td>
      <td>5.0</td>
      <td>I made this for my son's first birthday party this weekend. Our guests INHALED it! Everyone kept saying how delicious it was. I was I could have gotten to try it.</td>
      <td>5.0</td>
      <td>194.8</td>
      <td>20.0</td>
      <td>6.0</td>
      <td>32.0</td>
      <td>22.0</td>
      <td>36.0</td>
      <td>3.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>412 broccoli casserole</td>
      <td>306168</td>
      <td>40</td>
      <td>50969</td>
      <td>2008-05-30</td>
      <td>[60-minutes-or-less,  time-to-make,  course,  main-ingredient,  preparation,  side-dishes,  vegetables,  easy,  beginner-cook,  broccoli]</td>
      <td>6</td>
      <td>['preheat oven to 350 degrees', 'spray a 2 quart baking dish with cooking spray , set aside', 'in a large bowl mix together broccoli , soup , one cup of cheese , garlic powder , pepper , salt , milk , 1 cup of french onions , and soy sauce', 'pour into baking dish , sprinkle remaining cheese over top', 'bake for 25 minutes or until cheese is lightly browned', 'sprinkle with rest of french fried onions and bake until onions are browned and cheese is bubbly , about 10 more minutes']</td>
      <td>since there are already 411 recipes for broccoli casserole posted to "zaar" ,i decided to call this one  #412 broccoli casserole.i don't think there are any like this one in the database. i based this one on the famous "green bean casserole" from campbell's soup. but i think mine is better since i don't like cream of mushroom soup.submitted to "zaar" on may 28th,2008</td>
      <td>[frozen broccoli cuts,  cream of chicken soup,  sharp cheddar cheese,  garlic powder,  ground black pepper,  salt,  milk,  soy sauce,  french-fried onions]</td>
      <td>9</td>
      <td>768828.0</td>
      <td>2013-08-02</td>
      <td>5.0</td>
      <td>Loved this.  Be sure to completely thaw the broccoli.  I didn&amp;#039;t and it didn&amp;#039;t get done in time specified.  Just cooked it a little longer though and it was perfect.  Thanks Chef.</td>
      <td>5.0</td>
      <td>194.8</td>
      <td>20.0</td>
      <td>6.0</td>
      <td>32.0</td>
      <td>22.0</td>
      <td>36.0</td>
      <td>3.0</td>
    </tr>
  </tbody>
</table>

<br>

*You can see that I didn't convert the other lists into their own columns - this is because I didn't need them easily accessible to answer my question, and didn't want to add more columns to this already large dataframe.*

<br>


**Univariate Analysis:**
In order to account for outliers in the `'minutes'` column, I chose to only graph data in the 95th percentile. This solution preserves outliers in my dataframe in case I would like to work with them in the future, while still presenting the data in a clean, understandable way. 

<iframe src="assets/Recipes Time Distribution.html" width=800 height=600 frameBorder=0></iframe>

*Notice that the time distribution is not smooth. This is because of the tendency of users to round their times. (eg instead of reporting a recipe takes 33 mins users submit 35 mins).* 

<br>



**Bivariate Analysis:**
 I wanted to see if there was a noticeable difference in correlation of fat vs calories to protein vs calories. Like the previous graphs, I limited my data to within the 99.9th percentile in order to avoid the extreme outliers while still keeping as much data as possible.

<iframe src="assets/total fat (PDV) vs Calories.html" width=800 height=600 frameBorder=0></iframe>

*Here we see a significant positive correlation between Percent Daily Value of Fat and total calories of the dish.*

<iframe src="assets/protein (PDV) vs Calories.html" width=800 height=600 frameBorder=0></iframe>

*Here we see a noticeably more spread, however still positive correlation between Percent Daily Value of Protein and total calories of the dish.*

<br>

I thought that these plots were interesting, as it shows that protein is more losely correlated to calories compared to Fat. This makes sense, as fat is 9 calories per gram wheras protein is only 4 cal/g, making fat a larger contributor to total calories. There is also a suprisingly straight line lower limit that can be drawn in the `total fat (PDV) vs Calories` graph. I belive that this line would represent the minimum amount of calories a dish can be given it's PDV of Fat.

<br>

**Interesting Aggregates:**
One of the interesting aggregates I created was seeing the distribution of reviews by rating. From this aggregation, I saw that written reviews were mostly left for 'good' dishes (rated 4 or 5 stars) wheras people were less likely to take the time to write a bad review (dishes rated 1-3 stars).

|   rating |   Probability of writing a Review |
|---------:|----------------------------------:|
|        1 |                         0.0122382 |
|        2 |                         0.0101011 |
|        3 |                         0.0305892 |
|        4 |                         0.159097  |
|        5 |                         0.723592  |


<br>

--- 
## Assessment of Missingness
* **NMAR Analysis**


* **Missingness Dependency**

--- 
## Hypothesis Testing

