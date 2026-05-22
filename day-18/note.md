Today I continued working on the "Media Catalogue" Workshop.
I added the super-function to my __init__ method in the TVSeries class, 
so that it doesn't override the __init__ method in it's parents class (Movie).
I also added a few if-statements to check if the episodes or seasons in the TVSeries class are less then 1.
Then I added a __str__ method to the TVSeries class, to represent the series in the same way like the movies.
I also added docstrings to MediaCatalogue, TVSeries, Movie and MediaError classes. 
I added another exception to my try-except-block which makes it better to debug the code so I know which object causes problems.
Then I changed the loops in my __str__ method inside the MediaCatalogue class, to iterate seperatly over movies and series and 
print out the result divided in movie and series. I also gave the categories a title: '=== MOVIES ===' and '=== TV SERIES ==='.
With that I completed the Media Catalogue workshop.
