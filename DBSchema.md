# Movie-Ticket-Booking
It contains DB Design of Movie Booking and DB Schema and some Handson
# DB Schema

create table registration_type (
  regtype_id int primary key,
  regtype varchar(20));
  
create table registration (
  reg_id int primary key,
  name varchar(40),
  password varchar(40),
  email varchar(50),
  phonenum int,
  regtype_id int,
  CONSTRAINT fk_registration_type_registration
  FOREIGN KEY(regtype_id)
  REFERENCES registration_type(regtype_id));
      
create table login_type (
  login_type_id int primary key,
  login_type varchar(20));
 
 create table login (
  login_id int primary key,
  login_type_id int,
  CONSTRAINT fk_login_type_login
  FOREIGN KEY(login_type_id)
  REFERENCES login_type(login_type_id));
 
create table offer (
 offer_id int primary key,
 offer_type varchar(20),
 expirydate date);
   
create TABLE coupon (
     coupon_id int PRIMARY KEY,
     offer_id int,
     reward_id int,
     CONSTRAINT fk_offer_coupon
     FOREIGN KEY(offer_id)
     REFERENCES offer(offer_id),
     CONSTRAINT fk_rewards_coupon
     FOREIGN KEY(reward_id)
     REFERENCES rewards(reward_id));
 
create table user(
 user_id int primary key,
 name varchar(40),
 phonenum int,
 email_id varchar(40),
 reg_id int,
 location_id int,
 coupon_id int,
 reward_id int,
 CONSTRAINT fk_registration_user
 FOREIGN KEY(registration_id)
 REFERENCES registration(reg_id),
 CONSTRAINT fk_location_user
 FOREIGN KEY(location_id)
 REFERENCES location(location_id),
 CONSTRAINT fk_coupon_user
 FOREIGN KEY(coupon_id)
 REFERENCES coupon(coupon_id),
 CONSTRAINT fk_rewards_user
 FOREIGN KEY(reward_id)
 REFERENCES rewards(reward_id));
 

create table profile (
   profile_id int PRIMARY KEY,
   user_id int,
   total_rewards varchar(40),
   movies_watched varchar(40),
   CONSTRAINT fk_user_profile
     FOREIGN KEY(user_id)
     REFERENCES user(user_id));
     
   
insert into registration_type values( 1, 'old user');
insert into registration_type values( 2, 'existing user');
insert into registration_type values( 3, 'existing user');
insert into registration_type values( 4, 'existing user');
insert into registration_type values( 5, 'old user');
   
insert into registration values(1, 'Aiden','aid123' ,'aiden10@gmail.com', 789456123, 1);
insert into registration values(2, 'Daniel' ,'dan145','daniel10@gmail.com', 789456123, 2);
insert into registration values(3, 'Ethan' ,'mark199','ethan10@gmail.com', 789456123, 3);
insert into registration values(4, 'Carter' ,'cat124','carter@gmail.com', 789456123, 4);
insert into registration values(5, 'Samson' ,'chay4sam','samson10@gmail.com', 789456123, 5);
   
 insert into login_type values(1, 'customer');
insert into login_type values(2, 'Manager');
insert into login_type values(3, 'Stakeholder');
insert into login_type values(4, 'Employee');
insert into login_type values(5, 'owner');
   
insert into login values(1, 1);
insert into login values(2, 2);
insert into login values(3, 3);
insert into login values(4, 4);
insert into login values(5, 5);
   
   insert into offer values(1,'filmy pass @99rs');
   insert into login values(2, 'yes bank off buy 1 get 1 free');
   insert into offer values(3,'cashback offer on amazon pay');
   insert into login values(4, '4 free movie tickets using auram card');   
   insert into offer values(5,'enjoy online streaming events for free');
   
insert into coupon values(1, 1,1);
insert into coupon values(2, 2,2);
insert into coupon values(3, 3,3);
insert into coupon values(4, 4,4);
insert into coupon values(5, 5,5);
   
  insert into user values(1,'Aiden', 789456123, 'aiden@gmail.com', 1, 'UR1', 'Logged in as a client', '1');
insert into user values(2, 'Holbeck', 789456123, 'holbeck@gmail.com', 2, 'UR2', 'Logged in as a new user', '2');
insert into user values(3, 'Rogers', 789456123, 'rogers@gmail.com', 3, 'UR3', 'Logged in as an existing user', '3');
insert into user values(4, 'Prower', 789456123, 'prower@gmail.com', 4, 'UR4', 'Logged in as a client', '4');
insert into user values(5, 'Dobby', 789456123, 'dobby@gmail.com', 5, 'UR5', 'Logged in as a client', '5'); 
 
    insert into user values(1,'aiden@gmail.com',789456123,'Aiden', 1, 1,1,1);
    insert into user values(2,'holbeck@gmail.com',789456124,'holbeck',2,2,2,2);
     insert into user values(3,'rogers@gmail.com',805077564,'Rogers',3,3,3,3);
     insert into user values(4,'prower@gmail.com',987654323,'prower',4,4,4,4);
     insert into user values(5,'dobby@gmail.com',8765432451,'Dobby',5,5,5,5); 
   
   insert into PROFILE values(1,1,2,3);
    insert into PROFILE values(2,2,4,3);                           
    insert into PROFILE values(3,3,3,2);
    insert into PROFILE values(4,4,2,2);
    insert into PROFILE values(5,4,5,3);
    
    
create table location (
location_id int primary key,
loc_name varchar(60),
country_id int,
constraint fk_country_location
foreign key (country_id)
references country(country_id)
);

create table country (
country_id int primary key,
country_name varchar(60),
state_id int,
constraint fk_state_country
foreign key (state_id)
references state(state_id)
);


create table state (
state_id int primary key,
state varchar(60),
district_id int, 
constraint fk_district_state
foreign key (district_id)
references district(district_id)
);

create table city (
city_id int primary key,
city varchar(60)
)


create table theatre(
theatre_id int primary key,
name varchar(60),
country_id int,
contact_det,
constraint fk_country_theatre
foreign key (country_id)
references country(country_id)  
);

create table screen(
screen_id int primary key,
type_id int,
theatre_id int,
seat_id int,
constraint fk_screen_type_screen
foreign key (type_id)
references screen_type(type_id),
constraint fk_theatre_screen
foreign key (theatre_id)
references theatre(theatre_id),
constraint fk_seat_avaibility_screen
foreign key (seat_id)
references seat_avaibility(seat_id)
);

create table screen_type(
type_id int primary key,
screen_type varchar (60)
);


----------------INSERTION-----------------


insert into location values('1','SAKET','1');
insert into location values('2','NOIDA','2');
insert into location values('3','DWARKA','3');
insert into location values('4','NEHRU PLACE','4');
insert into location values('5','RAJA VIHAR','5');


insert into country values('1','INDIA','1');
insert into country values('2','VETICAN CITY','2');
insert into country values('3','RUSSIA','3');
insert into country values('4','SRI LANKA','4');
insert into country values('5','BHUTAN','5');

insert into state values ('1','DELHI','1');
insert into state values ('2','MAHARASHTRA','2');
insert into state values ('3','PUNJAB','3');
insert into state values ('4','RAJASTHAN','4');
insert into state values ('5','ANDHRA PRADESH','5');


insert into district values ('1','SOUTH-WEST','1');
insert into district values ('2','KOLHAPUR','2');
insert into district values ('3','LUDHIANA','3');
insert into district values ('4','UDAIPUR','4');
insert into district values ('5','KURNOOL','5');

insert into city values ('1','NEW-DELHI');
insert into city values ('2','PUNE');
insert into city values ('3','CHANDIGARH');
insert into city values ('4','UDAIPUR');
insert into city values ('5','KURNOOL');

insert into theatre values('1','ANUPAM','1','SAKET NEAR SAKET COURT'); 
insert into theatre values('2','SAHARA','1','GURGAON NEAR CARTERPURI ROAD');
insert into theatre values('3','PVR','1','NEHRU PLACE BESIDE EROS TOWER');
insert into theatre values('4','PVR PLAZA','1','CANNAUGHT PALACE NEAR H&M');
insert into theatre values('5','INOX','1','JYOTHI MALL');


insert into screen values('1','1','1','1');
insert into screen values('2','2','2','2');
insert into screen values('3','3','3','3');
insert into screen values('4','4','4','4');
insert into screen values('5','5','5','5');

insert into screen_type values('1','FRONT PROJECTION');
insert into screen_type values('2','REAR PROJECTION');
insert into screen_type values('3','3D PROJECTION');
insert into screen_type values('4','REAR PROJECTION');
insert into screen_type values('5','3D PROJECTION');
    

create table movie(
 movie_id int primary key,
 title varchar(50),
 description varchar(100),
 release_date date,
 user_id int,
 location_id int,
 rating_id int,
 cast_id int,
 crew_id int,
 genre_id int,
 constraint fk_movie_user_id
 foreign key(user_id)
 References user(user_id),
 constraint fk_movie_location_id
 foreign key(location_id)
 References location(location_id),
 constraint fk_movie_rating_id
 foreign key(rating_id)
 References rating(rating_id),
 constraint fk_movie_cast_id
 foreign key(cast_id)
 References cast(cast_id),
 constraint fk_movie_crew_id
 foreign key(crew_id)
 References crew(crew_id),
 constraint fk_movie_genre_id
 foreign key(genre_id)
 References genre(genre_id)
);

insert into movie values(1,'Bheemla Nayak','Upcoming Telugu action thriller movie','12/01/2022',1,1,1,1,1,1);
insert into movie values(2,'RRR','Period action drama film','07/01/2022',2,2,2,2,2,2);
insert into movie values(3,'Eternals','Marvel movie after the thanos snap','04/11/2022',3,3,3,3,3,3);
insert into movie values(4,'Pushpa','based on real life incidents and sandalwood smugglers','17/12/2022',4,4,4,4,4,4);


create table cast(
 cast_id int primary key,
 cast varchar(100)
);

insert into cast values(1,'Pawan Kalyan, Rana, Nitya Menon');
insert into cast values(2,'Ram Charan, NTR, Alia Bhatt');
insert into cast values(3,'Angelina Jolie, Richard Madden, Kit Harington, Salma Hayek');
insert into cast values(4,'Allu Arjun, Rashmika, Fahadh');


create table crew(
 crew_id int primary key,
 crew varchar(100)
);

insert into cast values(1,'Sagar K Chandra,Sitara Entertainments, Thaman, Trivikram');
insert into cast values(2,'Rajamouli,DVV Entertainments, Keeravani, Senthil');
insert into cast values(3,'Chloe Zhao, Marvel Studios, Ramin Djawadi, Ben Davis');
insert into cast values(4,'Sukumar, Mythri Movies, DSP, Ratnavelu');

create table language(
 language_id int primary key,
 language varchar(50)
);

insert into language values(1,'Telugu');
insert into language values(2,'Telugu,Tamil,Hindi,Kannada,Malayalam');
insert into language values(3,'English');
insert into language values(4,'Telugu,HIndi,Tamil,Kannada,Malayalam');

create table genre(
 genre_id int primary key,
 genre varchar(50)
);

insert into genre values(1,'Action/Drama/Thriller');
insert into genre values(2,'Action/Drama');
insert into genre values(3,'Adventure/Action');
insert into genre values(4,'Action/Drama');

create table rating_type(
 type_id int primary key,
 type varchar(30)
);

insert into rating_type values(1,'Average');
insert into rating_type values(2,'Good');
insert into rating_type values(3,'Excellent');
insert into rating_type values(4,'Bad');

create table rating(
 rating_id int primary key,
 type_id int,
 constraint fk_rating_type_id
 foreign key(type_id)
 References rating_type(type_id)
);

insert into rating values(1,1);
insert into rating values(2,2);
insert into rating values(3,3);
insert into rating values(4,3);

create table review(
 review_id int primary key,
 type_id int,
 rating_id int,
 constraint fk_review_type_id
 foreign key(type_id)
 References review_type(type_id),
 constraint fk_review_rating_id
 foreign key(rating_id)
 References rating(rating_id)
);

insert into review values(1,1,1);
insert into review values(2,2,2);
insert into review values(3,3,3);
insert into review values(4,4,4);


create table review_type(
type_id int PRIMARY KEY,
type Varchar(200)
);

insert into review_type values(1,'extraordinary');
insert into review_type values(2,'good');
insert into review_type values(3,'average');
insert into review_type values(4,'below average');
insert into review_type values(5,'bad');
-------------------------------------------------------------
create table show_tym (
show_id int PRIMARY KEY,
show_time TIMESTAMP ,
type_id int ,
screen_id int,
snack_id int,
constraint fk_show_type_show_tym foreign key(type_id)
references show_type (type_id),
constraint fk_screen_show_tym foreign key(screen_id)
references screen(screen_id),
constraint fk_grab_a_bite_show_tym foreign key(snack_id)
references grab_a_bite(snack_id));

insert into show_tym values(1,TO_TIMESTAMP ('07-JAN-2019 07:00:00','DD-MON-YYYY HH:MI:SS'),1,1,1);
insert into show_tym values(2,TO_TIMESTAMP ('08-JAN-2019 07:00:00','DD-MON-YYYY HH:MI:SS'),2,2,2);
insert into show_tym values(3,TO_TIMESTAMP ('09-JAN-2019 07:00:00','DD-MON-YYYY HH:MI:SS'),3,3,3);
insert into show_tym values(4,TO_TIMESTAMP ('10-JAN-2019 07:00:00','DD-MON-YYYY HH:MI:SS'),4,4,4);
insert into show_tym values(5,TO_TIMESTAMP ('11-JAN-2019 07:00:00','DD-MON-YYYY HH:MI:SS'),5,5,5);
--------------------------------------------------------------------------------------------------------
create table seat_availability(
seat_id int PRIMARY KEY,
status_id int,
constraint fk_status_seat_availability foreign key(status_id)
references status(status_id));

insert into seat_availability values(1,1);
insert into seat_availability values(2,2);
insert into seat_availability values(3,3);
insert into seat_availability values(4,4);
insert into seat_availability values(5,5);
--------------------------------------------------------------------------------------------------------------
create table show_type(
type_id primary key,
type varchar(100));

insert into show_type values(1,'mrng_show');
insert into show_type values(2,'matinee');
insert into show_type values(3,'first_show');
insert into show_type values(4,'second_show');
------------------------------------------------------------------------------------------------------------------
create table status(
status_id PRIMARY KEY,
type_id int,
constraint fk_status_type_status foreign key(type_id)
references status_type(type_id));

insert into status values(1,1);
insert into status values(2,2);
insert into status values(3,3);
insert into status values(4,4);
insert into status values(5,5);
------------------------------------------------------------------------------------------------------------------
create table status_type(
type_id PRIMARY KEY,
status_type varchar(100));

insert into status_type values(1,'available');
insert into status_type values(2,'not_available');
insert into status_type values(3,'not_available');
insert into status_type values(4,'available');
insert into status_type values(5,'not_available');
----------------------------------------------------------------------------------------------------------------------------------
create table tickets(
tic_id int PRIMARY KEY,
seat_num varchar(10),
count int,
theater_id int,
type_id int,
constraint fk_theater_tickets foreign key(theater_id)
references theater(theater_id),
constraint fk_ticket_type_tickets foreign key(type_id)
references type(ticket_type_id));

insert into tickets values(1,'A1',1,1,1);
insert into tickets values(1,'A2,A3',2,1,1);
insert into tickets values(1,'B1',1,3,2);
insert into tickets values(1,'C1',1,2,3);
insert into tickets values(1,'C2',1,2,3);
insert into tickets values(1,'C3',1,2,3);
----------------------------------------------------------------------------------------
create table tickets_type(
type_id PRIMARY KEY,
ticket_type varchar(100));

insert into tickets_type values(1,'platinum');
insert into tickets_type values(2,'gold');
insert into tickets_type values(3,'silver');
-----------------------------------------------------------------------------------------------------------

CREATE TABLE grab_a_byte(
snack_id int PRIMARY KEY,
snack_type_id int,
CONSTRAINT fk_snack_type_grab_a_byte 
FOREIGN KEY (snack_type_id) 
REFERENCES snack_type(snack_type_id)
);



CREATE TABLE snack_type(
snack_type_id int PRIMARY KEY,
snacktype VARCHAR(35)
);


CREATE TABLE payment(
payment_id int PRIMARY KEY,
payment_type_id int,
amount int,
CONSTRAINT fk_payment_type_payment
FOREIGN KEY (payment_type_id)
REFERENCES payment_type(payment_type_id)
);

CREATE TABLE payment_type(
payment_type_id int PRIMARY KEY,
payment_type varchar(40),
gateway_id int,
CONSTRAINT fk_payment_gateway_payment_type
FOREIGN KEY (gateway_id)
REFERENCES payment_gateway(gateway_id)
);

CREATE TABLE rewards(
reward_id int PRIMARY KEY,
is_bool BOOLEAN,
payment_id int,
expirydate DATETIME,
CONSTRAINT fk_payment_rewards
FOREIGN KEY (payment_id)
REFERENCES payment(payment_id)
);

CREATE TABLE payment_gateway(
gateway_id int PRIMARY KEY,
authentication_id int,
CONSTRAINT fk_authontication_payment_gateway
FOREIGN KEY (authentication_id)
REFERENCES authentication(authentication_id)
);


CREATE TABLE authentication(
authentication_id int PRIMARY KEY,
authentype_id int,
CONSTRAINT fk_authentication_type_authentication
FOREIGN KEY (authentype_id)
REFERENCES authentication_type(authentype_id)
);


CREATE TABLE authentication_type(
authetype_id int PRIMARY KEY,
authentype VARCHAR(40)
);
------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------


INSERT INTO grab_a_byte values (1,1);
INSERT INTO grab_a_byte values(2,2);
INSERT INTO grab_a_byte values(3,3);
INSERT INTO grab_a_byte values(4,4);
INSERT INTO grab_a_byte values(5,5);



INSERT INTO snack_type values(1,'popcorn');
INSERT INTO snack_type values(2,'Burger');
INSERT INTO snack_type values(3,'pepsi');
INSERT INTO snack_type values(4,'chicken-popcorn');
INSERT INTO snack_type values(5,'roles');



INSERT INTO payment values(1,1,220);
INSERT INTO payment values(2,2,300);
INSERT INTO payment values(3,3,350);
INSERT INTO payment values(4,4,425);
INSERT INTO payment values(5,5,600);


INSERT INTO payment_type values(1,'PHONEPAY',1);
INSERT INTO payment_type values(2,'GPAY',2);
INSERT INTO payment_type values(3,'GPAY',3);
INSERT INTO payment_type values(4,'PAYPAL',4);
INSERT INTO payment_type values(5,'PHONEPAY',5);




INSERT INTO rewards values(1,TRUE,1,'2021-10-02 14:00:00');
INSERT INTO rewards values(2,TRUE,2,'2021-10-04 10:15:00');
INSERT INTO rewards values(3,TRUE,3,'2021-10-06 12:00:00');
INSERT INTO rewards values(4,TRUE,4,'2021-10-08 14:35:00');
INSERT INTO rewards values(5,TRUE,5,'2021-10-10 16:55:00');



INSERT INTO payment_gateway values(1,1);
INSERT INTO payment_gateway values(2,2);
INSERT INTO payment_gateway values(3,3);
INSERT INTO payment_gateway values(4,4);
INSERT INTO payment_gateway values(5,5);

INSERT INTO authentication values(1,1);
INSERT INTO authentication values(2,2);
INSERT INTO authentication values(3,3);
INSERT INTO authentication values(4,4);
INSERT INTO authentication values(5,5);


INSERT INTO authentication_type values(1,'PASSWORD');
INSERT INTO authentication_type values(2,'PIN');
INSERT INTO authentication_type values(3,'PASSWORD');
INSERT INTO authentication_type values(4,'PIN');
INSERT INTO authentication_type values(5,'PASSWORD');


create table bill(
bill_id int primary key,
seatno varchar(20),
payment_id int,
movie_title varchar(45),
screen varchar(30),
snacks varchar(50),
CONSTRAINT fk_bill_payment_id
FOREIGN KEY(payment_id)
REFERENCES payment(payment_id)
);

INSERT INTO bill values(1,'A1',1,'Bheemla nayak','screen 3','popcorn');
INSERT INTO bill values(2,'D12,D13',2,'RRR','Screen 1','Burger');


CREATE TABLE m_rating (
m_rate_id VARCHAR(45),
rating VARCHAR(45)
);


INSERT INTO m_rating VALUES (1,'five star');
INSERT INTO m_rating VALUES (2,'four star');
INSERT INTO m_rating VALUES (3,'three star');

CREATE TABLE t_rating (
t_rate_id VARCHAR(45),
rating VARCHAR(45)
);


INSERT INTO t_rating VALUES (1,'five star');
INSERT INTO t_rating VALUES (2,'four star');
INSERT INTO t_rating VALUES (3,'three star');


create table h_rating(
rating_id int primary key,
m_rate_id int,
t_rate_id int,
CONSTRAINT fk_h_rating_m_rate_id
FOREIGN KEY(m_rate_id)
REFERENCES m_rating(m_rate_id),
CONSTRAINT fk_h_rating_t_rate_id
FOREIGN KEY(t_rate_id)
REFERENCES t_rating(t_rate_id)
);

insert into h_rating values(1,1,1);
insert into h_rating values(2,2,2);
insert into h_rating values(3,3,3);

create table h_language(
language_id int primary key,
language varchar(50)
);

insert into h_language values(1,'Telugu');
insert into h_language values(2,'Telugu, Hindi, Tamil, Kannada, Malayalam');


create table h_showtym(
show_id int primary key,
showtym TIMESTAMP
);

insert into h_showtym values(1,TO_TIMESTAMP ('12-JAN-2021 10:30:00','DD-MON-YYYY HH:MI:SS'));
insert into h_showtym values(2,TO_TIMESTAMP ('07-JAN-2021 15:00:00','DD-MON-YYYY HH:MI:SS'));

create table screen_type(
type_id int primary key,
type varchar(50)
);

insert into screen_type values(1,'BIG SCREEN');
insert into screen_type values(2,'VIP');

create table h_screen(
screen_id int primary key,
screen varchar(40),
show_id int,
type_id int,
CONSTRAINT fk_h_screen_show_id
FOREIGN KEY(show_id)
REFERENCES h_showtym(show_id),
CONSTRAINT fk_h_screen_type_id
FOREIGN KEY(type_id)
REFERENCES screen_type(type_id)
);

insert into h_screen values(1,'Screen 3',1,1);
insert into h_screen values(2,'Screen 1',2,2);

create table h_movie(
movie_id int primary key,
language_id int,
screen_id int,
rating_id int,
genre varchar(50),
cast varchar(100),
crew varchar(100),
CONSTRAINT fk_h_movie_language_id
FOREIGN KEY(language_id)
REFERENCES h_language(language_id),
CONSTRAINT fk_h_movie_screen_id
FOREIGN KEY(screen_id)
REFERENCES h_screen(screen_id),
CONSTRAINT fk_h_movie_rating_id
FOREIGN KEY(rating_id)
REFERENCES h_rating(rating_id)
);

insert into h_movie values(1,1,1,1,'Thriller','Pawan Kalyan, Rana','Sagar K chandra, Trivikram');
insert into h_movie values(2,2,2,2,'Drama','Ram charan, NTR','Rajamouli, Keeravani');
 

CREATE TABLE h_user (
user_id INT PRIMARY KEY,
country_id VARCHAR(45),
phonenum VARCHAR(45),
u_name VARCHAR(45),
email VARCHAR(45),
CONSTRAINT fk_h_user_country_id
FOREIGN KEY(country_id)
REFERENCES country(country_id)
);

CREATE TABLE h_country (
country_id VARCHAR(45),
country VARCHAR(45),
state_id VARCHAR(45),
CONSTRAINT fk_h_country_state_id
FOREIGN KEY(state_id)
REFERENCES state(state_id)
);

CREATE TABLE h_state (
state_id INT PRIMARY KEY,
state VARCHAR(45),
city_id VARCHAR(45),
CONSTRAINT fk_h_state_city_id
FOREIGN KEY(city_id)
REFERENCES city(city_id)
);


CREATE TABLE h_city (
city_id INT PRIMARY KEY,
city VARCHAR(45)
);

CREATE TABLE h_payment (
payment_id INT PRIMARY KEY,
ticket_id VARCHAR(45),
amount VARCHAR(45),
reward_id VARCHAR(45),
CONSTRAINT fk_h_payment_ticket_id
FOREIGN KEY(ticket_id)
REFERENCES ticket(ticket_id),
CONSTRAINT fk_h_payment_reward_id
FOREIGN KEY(reward_id)
REFERENCES reward(reward_id)
);


CREATE TABLE h_ticket (
ticket_id INT PRIMARY KEY,
movie_name VARCHAR(45),
amount VARCHAR(45),
screen VARCHAR(45),
show_tym VARCHAR(45),
ticket_type_id VARCHAR(45),
CONSTRAINT fk_h_ticket_ticket_type_id
FOREIGN KEY(ticket_type_id)
REFERENCES ticket_type(ticket_type_id)
);


INSERT INTO h_user VALUES ('1','001','7674563421','A','user1@gmail.com');
INSERT INTO h_user VALUES ('2','002','7645834256','B','user12@gmail.com');
INSERT INTO h_user VALUES ('3','003','7986537892','C','user13@gmail.com');

INSERT INTO h_country VALUES ('1','INDIA','2');
INSERT INTO h_country VALUES ('2','AUSTRIA','3');
INSERT INTO h_country VALUES ('3','CHINA','4');

INSERT INTO h_state VALUES ('1','AP','4');
INSERT INTO h_state VALUES ('1','up','6');
INSERT INTO h_state VALUES ('1','karnataka','8');

INSERT INTO h_city VALUES ('1','paris');
INSERT INTO h_city VALUES ('2','chennai');
INSERT INTO h_city VALUES ('3','london');

INSERT INTO h_payment VALUES ('1','01','200','2');
INSERT INTO h_payment VALUES ('2','02','500','4');
INSERT INTO h_payment VALUES ('3','03','800','6');

INSERT INTO h_ticket VALUES ('1','puspha','500','11AM to 1.45PM','2');
INSERT INTO h_ticket VALUES ('2','ala vaikuntapuramlo','500','2.30PM to 5.45PM','4');
INSERT INTO h_ticket VALUES ('1','Dj','500','6pM to 9PM','6');



CREATE TABLE h_ticket_type 
(	
 ticket_type_id  int PRIMARY KEY,	
 type VARCHAR(45)	
);


insert into h_ticket_type values(1,'second class');
insert into h_ticket_type values(2,'Balcony');
insert into h_ticket_type values(3,'VIP');
insert into h_ticket_type values(4,'First class');



CREATE TABLE h_snack_type 
(	
 snack_type_id  int PRIMARY KEY,	
 type VARCHAR(45)	
);

insert into h_snack_type values(1,'All');
insert into h_snack_type values(2,'Combos');
insert into h_snack_type values(3,'Beverages');
insert into h_snack_type values(4,'Snacks');
insert into h_snack_type values(5,'PopCorn');
insert into h_snack_type values(6,'Immunity Boosters');


CREATE TABLE h_snacks 
(	
 snack_id  int PRIMARY KEY,	
 snacks VARCHAR(100),
 snacks_type_id int, 
 CONSTRAINT fk_h_snack_type_h_snack	
 FOREIGN KEY(snack_type_id)	
 REFERENCES h_snack_type (snack_type_id) 
);

insert into h_snacks values(1,'2 large cheese popcorn + 2 small coke, Cold coffee, Tub cheese popcorn',1);
insert into h_snacks values(2,'large caramel popcorn + Large coke, Tub caramel popcorn + 2 large coke',2);
insert into h_snacks values(3,'Nachos with salsa & Cheese Sauce',3);
insert into h_snacks values(4,'Cold Coffee, Large Coke, Cardomom tea',4);
insert into h_snacks values(5,'Tub tom chilli popcorn, large caramel popcorn, large cheese popcorn',5);
insert into h_snacks values(6,'greenfit tea-tulsi, greenfit tea-Lemon honey, greenfit tea-Vitality',6);


CREATE TABLE h_rewards 
(	
 reward_id int PRIMARY KEY,	
 reward VARCHAR(45),
 expirydate DATE
);



insert into h_rewards values(1,'Payback points','31/10/2021');
insert into h_rewards values(2,'Reward points Redemption','02/11/2021');
insert into h_rewards values(3,'SBI card rewards offer','13/11/2021');
