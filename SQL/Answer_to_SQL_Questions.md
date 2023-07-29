Answers to SQL Questions

1.	Give me list of Customers whose First Name starts with N Or they Live in city xyz.  (Return me Customer Id, First name, Last Name, City) 

ANS : 

      SELECT CustomerId as 'Customer_Id',FirstName as 'First_Name' ,LastName as 'Last_Name' ,City
      FROM Customers 
      WHERE FirstName LIKE 'N%' OR City='Oslo'

      ![image](https://github.com/mayuresh25027/DAX-DS-Assignment-2023-Mayur_Patil/assets/87094130/b2942adb-2f5c-44bc-b766-d722ff22bef5)


 

2.	Give me list of Tracks where unit prize range between x and y and whose composer name does not contain 'T' (Return me Track Id, Name, Composer, Unit Price) 

ANS:

      SELECT TrackId as 'Track_ID', Name, Composer, UnitPrice as 'Unit_Price'
      FROM Tracks
      WHERE UnitPrice BETWEEN 0.1 AND 1.0
      AND Composer NOT LIKE '%T%'

      ![image](https://github.com/mayuresh25027/DAX-DS-Assignment-2023-Mayur_Patil/assets/87094130/499d4bdc-2988-408f-b6c5-c56b26f0dd7a)

 
3.	Calculate the sum of total Invoice bill and average of total Invoice bill for each day of month (June 2020). (Return me Invoice Date, Sum of Total bill for that day, Average of Total Bill for that day) 

ANS:

      SELECT InvoiceDate,SUM(Total) AS Sum_Bill, AVG(Total) AS Avg_Bill 
      FROM Invoices 
      WHERE strftime('%Y-%m', InvoiceDate) = '2009-06' 
      GROUP BY InvoiceDate

       ![image](https://github.com/mayuresh25027/DAX-DS-Assignment-2023-Mayur_Patil/assets/87094130/f60e5721-4e0b-4d37-b9c8-56800f56ffa3)



4.	Total Quantity of Each Track ID purchased so far. Sort the Track IDs in Descending order of it’s total Count (Return me Track ID and its total Quantity) 

ANS:

      SELECT TrackId,SUM(Quantity) AS Sum_Quantity 
      FROM invoice_items 
      GROUP BY TrackId 
      ORDER BY Sum_Quantity desc;

       ![image](https://github.com/mayuresh25027/DAX-DS-Assignment-2023-Mayur_Patil/assets/87094130/e699cd8b-7b7a-426b-a9e5-11404541e6a0)


5.	Give me list of Artist IDs,  whose none of the tracks are present in any Playlist. (Return Artist IDs and their names) 

ANS:

      SELECT * 
      FROM Artists 
      WHERE ArtistId NOT IN (
   	      SELECT ArtistId 
    	      FROM Albums 
    	      WHERE AlbumId IN (
        		SELECT AlbumId 
        		FROM Tracks 
        		WHERE TrackId IN (
            			SELECT TrackId 
            			FROM Playlist_Track
            			)
        		)
    	);

      ![image](https://github.com/mayuresh25027/DAX-DS-Assignment-2023-Mayur_Patil/assets/87094130/ee680ac7-b1b3-4e9e-b4f1-c7d719ec72ee)

      
6.	Give me a list of Album ID whose Tracks are present in more than 10 playlist(Return me Album ID, it's Title and the count of playlists wherein it's tracks are present)

ANS: 

      SELECT a.AlbumId, a.Title, COUNT(c.PlaylistId) AS count_playlist 
      FROM Albums a 
      INNER JOIN Tracks b ON a.AlbumId = b.AlbumId 
      INNER JOIN Playlist_track c ON b.TrackId = c.TrackId 
      GROUP BY a.AlbumId,a.Title 
      having count_playlist>10;

      ![image](https://github.com/mayuresh25027/DAX-DS-Assignment-2023-Mayur_Patil/assets/87094130/da7aac37-3bc2-4334-bc2c-c930b848e54a)
