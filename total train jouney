Input: ( I want total distance covered by each train between chennai to delhi) -------- 
Source_city 	Dest_city 	Distance 	Train 
Chennai 		Nagpur 		15000 		A 
Nagpur 			Delhi 		12000 		A 
Chennai 		UP 			  17000 		B 
UP 				  Delhi 		6000 		  B
 
output: ------- 
Source_City  Dest_City  Train  Distance 
Chennai      Delhi      A      27000 
Chennai      Delhi      B      23000

%sql
CREATE TABLE train_routes (
    source_city STRING,
    dest_city STRING,
    distance INT,
    train STRING
);
INSERT INTO train_routes (source_city, dest_city, distance, train) VALUES
('Chennai', 'Nagpur', 15000, 'A'),
('Nagpur', 'Delhi', 12000, 'A'),
('Chennai', 'UP', 17000, 'B'),
('UP', 'Delhi', 6000, 'B');


%sql
SELECT
    'Chennai' AS source_city,
    'Delhi' AS dest_city,
    train,
    SUM(distance) AS distance
FROM train_routes
WHERE train IN (
    SELECT train FROM train_routes WHERE source_city = 'Chennai'
)
AND train IN (
    SELECT train FROM train_routes WHERE dest_city = 'Delhi'
)
GROUP BY train;
