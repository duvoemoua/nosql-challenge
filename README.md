# nosql-challenge

Part 1: Database and Jupyter Notebook Set Up

To start part 1 I began by creating a new database and collection through my termainal.

 mongoimport --type json -d uk_food -c establishments --drop --jsonArray ../Resources/establishments.json

 
Once the database and collection was created I used the provided code to import MongoClient and pprint.
    -Then I confirmed that my database was created by printing the database names.
    -Then I confirmed that my collection was added by printing the collection name within the database.

I reviewed the document by 'pprint(db.establishments.find_one())' and assigned my collection to the variable 'establishments'.

Part 2: Update the Database

1.) For part 2 I created a dictionary called 'penang_flavours' and copied the provided information from bootcampspot and inserted it into my collection using the insert_one function.

I then verified that my new resturant was added into the collection by using the find_one function and searched by 'BusinessName'.

2.) To find the BusinessType for Restaurant/Cafe/Canteen I queried my collection for that specific BusinessType.
    -query = {'BusinessType': 'Restaurant/Cafe/Canteen'}

I then created fields to return only BusinessTypeID and BusinessType fields and pprinted the results


3.) That query returned a BusinessTypeID as 1. To update my restaurant I used the update_one function to set the BusinessTypeID as 1 and confirmed the changes were made by using the find_one function

4.) To find how many establishements were in Dover I used the count_documents function to could on LocalAuthorityName's for Dover. The total was 994. Then came time to delete all documents that include Dover. To do that I used the delete_many function  and then pprinted my initial search to confirm documents with Dover were removed and confirmed that documents remained with the find_one function using my establishments collection

5.) To change the latitude and longitude to decimal numbers I used the update_many function and set geocode.latitude and geocode.longitude to double. I used the provided code to set non_ratings to null. I then followed the same process to set 'RatingValue' from String to Integer.

Finally to confirm these changes were made I pprinted my collection to verify.





Part 3: Exploratory Analysis

1.) Which establishments have a hygiene score equal to 20?

To answer the first question within part 3 I created a query to query 'scores.Hygiene' with a score of 20 and then created a variable to hold my count_documents funtion within my query. I then pprinted my query to find that a total of 41 establishments have a hygiene score of 20. 

I then converted my results into a dataframe called establishments_df. To displat the number of rows in the dataframe I used the len function and displayed the first 10 rows of the dataframe. The dataframe had a total of 41 rows

2.) Which establishments in London have a RatingValue greater than or equal to 4?

To find the establishments with London as the Local Authority i first searched to see what each column was named by using the columns funtion on my established_df dataframe. From there I could see that LocalAuthorityBusinessID, LocalAuthorityName, LocalAuthorityCode, LocalAuthorityWebSite and LocalAuthorityEmailAddress exsisted. I did this to confirm if there were any easy option to find 'London' in. I decided to use 'LocalAuthorityName' and created a new query to find the establishments in London with a RatingValue greater than or equal to 4. I then followed the same steps as before and created a new_count variable to store my new count and pprinted my new query. I was able to display that there are 33 total establishments with London as the Local Authority and has a RatingValue greater than or equal to 4. I then converted this data into a new dataframe, 'london_df'.

3.) What are the top 5 establishments with a RatingValue rating value of 5, sorted by lowest hygiene score, nearest to the new restaurant added, "Penang Flavours"?

To start I first pprinted the Penang Flavours 'geocode.latitude' and 'geocode.longitude' using the find_one function. I then filled in the provided variables with the latitude and longitude information.

After the variables were set up I created a new geo_query that searched 'RatingValue' equal to 5 that had a latitude greater than or equal to the variable minus my degree _search of 0.01 and then latitude plus my degree_search to create my search range. I repeated the steps for longitude as well. I created a sort variable to sort by 'scores.Hygiene', 1 and then set my limit to 5 to get the top 5 results. I then pprinted the results and converted it into a dataframe, top_results_df. 


4.) How many establishments in each Local Authority area have a hygiene score of 0?

For this section I created a pipeline. I started by creating a match query to find Hygiene scores that match 0. And then crated a group query to group the matches by Local Authority. I then built out my pipeline with a sort_values to find the highest to lowest. The total number of documents in the results was 55. I pprinted the first 10 results of the query and coverted the data into a dataframe, final_df. 








