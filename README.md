Hotel reservation dataset to gain insights into guest preferences, booking trends, and other key factors that impact the hotel's operations. With SQL used to query and analyze the data



--1. What is the total number of reservations in the dataset?
select count(H.Booking_ID) as TotalNumberOfReservsation
from Hotel_Reservation H;

--2. Which meal plan is the most popular among guests?
select top 1 H.type_of_meal_plan
from Hotel_Reservation H
group by H.type_of_meal_plan order by Count(H.type_of_meal_plan) Desc ;



--3. What is the average price per room for reservations involving children?
select H.avg_price_per_room
from Hotel_Reservation H
where H.no_of_children > 1;


--4. How many reservations were made for the year 20XX (replace XX with the desired year)?
select count(H.Booking_ID) as TotalNumberOfReservsation
from Hotel_Reservation H where Year(H.arrival_date) = 2020;


--5. What is the most commonly booked room type?
select top 1 H.room_type_reserved
from Hotel_Reservation H group by H.room_type_reserved 
order by count(H.room_type_reserved) desc;


--6. How many reservations fall on a weekend (no_of_weekend_nights > 0)?

select count(H.Booking_ID) as NoOfReservationOnweekend
from Hotel_Reservation H
where H.no_of_weekend_nights > 0 ;


--7. What is the highest and lowest lead time for reservations?
select max(H.lead_time) As HighestLeadTime , Min(H.lead_time) As LowestLeadTime
from Hotel_Reservation H ;


--8. What is the most common market segment type for reservations?
select top 1 H.market_segment_type
from Hotel_Reservation H
group by H.market_segment_type order by Count(H.market_segment_type) desc;

--9. How many reservations have a booking status of "Confirmed"?
select Count(H.booking_status)
from Hotel_Reservation H
where H.booking_status = 'Confirmed';

--10. What is the total number of adults and children across all reservations?
select Sum(H.no_of_adults) As TotalNumberOfAdults,Sum(H.no_of_children) As TotalNumberOfChildren
from Hotel_Reservation H


--11. What is the average number of weekend nights for reservations involving children?
select avg(H.no_of_weekend_nights)
from Hotel_Reservation H
where H.no_of_children > 1

--12. How many reservations were made in each month of the year?

select Month(H.arrival_date) , Count(H.Booking_ID)
from Hotel_Reservation H
group by month(H.arrival_date)


--13. What is the average number of nights (both weekend and weekday) spent by guests for each room type?
select H.room_type_reserved ,Avg(H.no_of_week_nights + H.no_of_weekend_nights) as AverageNumberOfNights
from Hotel_Reservation H 
Group by H.room_type_reserved

--14. For reservations involving children, what is the most common room type, and what is the average price for that room type?
select top 1 H.room_type_reserved , Count(H.Booking_ID) As NoOfBookings , AVG(H.avg_price_per_room) As AveragePriceForRoomType
from Hotel_Reservation H
where H.no_of_children > 1 
group by H.room_type_reserved order by Count(H.Booking_ID) desc ;


--15. Find the market segment type that generates the highest average price per room.
select H.room_type_reserved
from Hotel_Reservation H
where H.avg_price_per_room = (
select Max(Hotel_Reservation.avg_price_per_room) from Hotel_Reservation) ;
