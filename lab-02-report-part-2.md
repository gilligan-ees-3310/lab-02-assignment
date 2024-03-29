Lab #2 Report, Part 2:
================
Put your name here
Lab: Mon. Jan. 31. Due: Wed. Feb. 9

-   [Instructions](#instructions)
-   [Worked Example for One-Layer
    Atmosphere](#worked-example-for-one-layer-atmosphere)
-   [Exercises from Chapter 3](#exercises-from-chapter-3)
    -   [Exercise 3.1 (Grad. students
        only)](#exercise-31-grad-students-only)
    -   [Exercise 3.2](#exercise-32)
    -   [Exercise 3.3](#exercise-33)

# Instructions

This document begins with a worked example to show you an example of
using RMarkdown to solve a layer-model (the 1-layer model from Chapter 3
of *Understanding the Forecast*) and then it has exercises from Chapter
3 for you to do yourself:

-   **All students** do Chapter 3, exercises 2–3.
-   **Graduate students** should also do Chapter 3, exercise 1.

When you do the exercises from Chapter 3. You have a choice:

-   Either you can do the exercises out of the book like regular
    homework and turn them in by posting your answers to Brightspace (if
    you do them with pencil and paper, take a photo or scan of your work
    and upload the images)

-   Or you can do them using RMarkdown and turn them by submitting them
    electronically on GitHub before class starts on Wednesday, Feb. 9.

    To submit the homework electronically,

    -   Accept the assignment on GitHub Classroom.

    -   Clone a local copy of the file repository from github.

    -   In your local repository, answer the exercises in the template
        `layer_models.Rmd`.

    -   When you are done, knit your `.Rmd` file into a PDF or DOCX
        (Microsoft Word) file.

    -   Use git to commit your changes (including the edits to
        `layer_models.Rmd` and the new PDF or DOCX file) to your local
        git repository.

    -   Push the changes from your local git repository to github.

        The last changes that you push before the due date (9am on
        Feb. 9) will be graded.

It is your choice how to do them. Either way is acceptable and will get
equal credit.

# Worked Example for One-Layer Atmosphere

``` r
I_solar = 1350
alpha = 0.30
sigma = 5.67E-8
epsilon = 1
```

> **A One-Layer Model.**

``` r
make_layer_diagram(1)
```

![An energy diagram for a planet with one pane of glass for an
atmosphere. The intensity of heat from visible light is
(1−*α*)*I*<sub>*s**o**l**a**r*</sub>/4.](lab-02-report-part-2_files/figure-gfm/one_layer_figure-1.png)

> 1.  Write the energy budgets for the atmospheric layer, for the
>     ground, and for the Earth as a whole.

**Answer:** Start at the top, at the boundary to sapce, and work
downward:

-   At the boundary to space,
    *I*<sub>1, *u**p*</sub> = (1−*α*)*I*<sub>*s**o**l**a**r*</sub>/4.

-   At the atmospheric layer,
    *I*<sub>1, *u**p*</sub> + *I*<sub>1, *d**o**w**n*</sub> = *I*<sub>*g**r**o**u**n**d*, *u**p*</sub>

-   At the ground,
    (1−*α*)*I*<sub>*s**o**l**a**r*</sub>/4 + *I*<sub>1, *d**o**w**n*</sub> = *I*<sub>*g**r**o**u**n**d*, *u**p*</sub>

We also know that

-   *I*<sub>1, *u**p*</sub> = *I*<sub>1, *d**o**w**n*</sub> = *ε**σ**T*<sub>1</sub><sup>4</sup>

-   *I*<sub>*g**r**o**u**n**d*, *u**p*</sub> = *σ**T*<sub>*g**r**o**u**n**d*</sub><sup>4</sup>

> 2.  Manipulate the budget for the Earth as a whole to obtain the
>     temperature T<sub>1</sub> of the atmospheric layer. Does this part
>     of the exercise seem familiar in any way? Does the term ring any
>     bells?

**Answer:**

(1−*α*)*I*<sub>*s**o**l**a**r*</sub>/4 = *I*<sub>1, *u**p*</sub> = *σ**T*<sub>1</sub><sup>4</sup>

(1−*α*)*I*<sub>*s**o**l**a**r*</sub>/4*ε**σ* = *T*<sub>1</sub><sup>4</sup>

$$T\_{1} = \\sqrt\[4\]{\\frac{(1 - \\alpha) I\_{solar}}{4 \\varepsilon \\sigma}}$$

This is familiar, because it’s the same as the formula for the bare-rock
temperature.

Here is R code to calculate *I*<sub>1,up</sub> and *T*<sub>1</sub>:

``` r
I_1_up = (1 - alpha) * I_solar / 4
T_1 = (I_1_up / (epsilon * sigma))^0.25
```

From the algebraic solution, we expect T<sub>1</sub> to be 254.1 K. From
the R code above, we get T<sub>1</sub> = 254.1 K.

> 3.  Now insert the value you found for T<sub>1</sub> into the budget
>     for atmospheric layer 1 to obtain the temperature of the ground,
>     T<sub>ground</sub>.

**Answer:**

-   *I*<sub>*g**r**o**u**n**d*</sub> = *I*<sub>1, *u**p*</sub> + *I*<sub>1, *d**o**w**n*</sub> = 2 × *I*<sub>1, *u**p*</sub>
-   *ε**σ**T*<sub>*g**r**o**u**n**d*</sub><sup>4</sup> = 2*ε**σ**T*<sub>1</sub><sup>4</sup>
-   *T*<sub>*g**r**o**u**n**d*</sub><sup>4</sup> = 2*T*<sub>1</sub><sup>4</sup>
-   $T\_{ground} = \\sqrt\[4\]{2} \\times T\_{1}$

And here is R code to calculate *I*<sub>1,down</sub>,
*I*<sub>ground</sub>, and *T*<sub>ground</sub>:

``` r
I_1_down = I_1_up
I_ground = I_1_up + I_1_down
T_ground = (I_ground / (epsilon * sigma))^0.25
```

From the algebraic solution, we get T<sub>ground</sub> = 302.1 K and
from the R code above, we get T<sub>ground</sub> = 302.1 K.

# Exercises from Chapter 3

-   **All students** do Chapter 3, exercises 2–3.
-   **Graduate students** should also do Chapter 3, exercise 1.

For the exercises, use the following numbers:

-   I<sub>solar</sub> = 1350 W/m<sup>2</sup>
-   *σ* = 5.67 × 10<sup>−8</sup>
-   *α* = 0.30
-   *ε* = 1.0

## Exercise 3.1 (Grad. students only)

> **The moon with no heat transport.** The Layer Model assumes that the
> temperature of the body in space is all the same. This is not really
> very accurate, as you know that it is colder at the poles than it is
> at the equator. For a bare rock with no atmosphere or ocean, like the
> moon, the situation is even worse because fluids like air and water
> are how heat is carried around on the planet. So let us make the other
> extreme assumption, that there is no heat transport on a bare rock
> like the moon. Assume for comparability that the albedo of this world
> is 0.30, same as Earth’s.
>
> What is the equilibrium temperature of the surface of the moon, on the
> equator, at local noon, when the sun is directly overhead? (Hint:
> First figure out the intensity of the local solar radiation
> I<sub>solar</sub>)

``` r
# TODO
# Put your R code here to answer the question
```

**Answer:** put your answer here …

> What is the equilibrium temperature on the dark side of the moon?

``` r
# TODO
# Put your R code here to answer the question
```

**Answer:** put your answer here …

## Exercise 3.2

> **A Two-Layer Model.** Insert another atmospheric layer into the
> model, just like the first one. The layer is transparent to visible
> light but a blackbody for infrared.

``` r
make_layer_diagram(2)
```

![An energy diagram for a planet with two panes of glass for an
atmosphere. The intensity of absorbed visible light is
(1−*α*)*I*<sub>*s**o**l**a**r*</sub>/4.](lab-02-report-part-2_files/figure-gfm/two_layer_figure-1.png)

> 1.  Write the energy budgets for both atmospheric layers, for the
>     ground, and for the Earth as a whole, like we did for the
>     One-Layer Model.

**Answer:** put your energy budgets here…

> 2.  Manipulate the budget for the Earth as a whole to obtain the
>     temperature T<sub>2</sub> of the top atmospheric layer, labeled
>     Atmospheric Layer 2 in the figure above. Does this part of the
>     exercise seem familiar in any way? Does the term ring any bells?

``` r
# TODO
# Put your R code here to answer the question
```

**Answer:** put the temperature T<sub>2</sub> here…

> 3.  Insert the value you found for T<sub>2</sub> into the energy
>     budget for layer 2, and solve for the temperature of layer 1 in
>     terms of layer 2. How much bigger is T<sub>1</sub> than
>     T<sub>2</sub>?

``` r
# TODO
# Put your R code here to answer the question
```

**Answer:** put the temperature T<sub>1</sub> here….

> 4.  Now insert the value you found for T<sub>1</sub> into the budget
>     for atmospheric layer 1 to obtain the temperature of the ground,
>     T<sub>ground</sub>. Is the greenhouse effect stronger or weaker
>     because of the second layer?

``` r
# TODO
# Put your R code here to answer the question
```

**Answer:** put your answer here…

## Exercise 3.3

``` r
make_nuclear_winter_diagram()
```

![An energy diagram for a planet with an opaque pane of glass for an
atmosphere. The intensity of absorbed visible light is
(1−*α*)*I*<sub>*s**o**l**a**r*</sub>/4.](lab-02-report-part-2_files/figure-gfm/nuclear_winter_diagram-1.png)

> **Nuclear Winter.** Let us go back to the One-Layer Model but change
> it so that the atmospheric layer absorbs visible light rather than
> allowing it to pass through (See the figure above). This could happen
> if the upper atmosphere were filled with dust. For simplicity, assume
> that the albedo of the Earth remains the same, even though in the real
> world it might change with a dusty atmosphere.> What is the
> temperature of the ground in this case?

``` r
# TODO
# Put your R code here to answer this question.
```

**Answer:** put your answer here … ”
