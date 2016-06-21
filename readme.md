
    1. How many users are there?
    50
    `select count (*)
     from users;`

    2. What are the 5 most expensive items?
    Small Cotton Gloves|9984
    Small Wooden Computer|9859
    Awesome Granite Pants|9790
    Sleek Wooden Hat|9390
    Ergonomic Steel Car|9341

   `select title, price
    from items
    order by price desc
    limit 5;`


    3. What's the cheapest book? (Does that change for "category is exactly 'book'" versus "category contains 'book'"?)

    The answer is the same in both cases.

    3a) Using category = "Books" as a condition
    Ergonomic Granite Chair|Books|1496

    `select title, price
     from items
     where category = "Books"
     order by price asc
     limit 1;`

     3b) Using category = "Books" as a condition
     Ergonomic Granite Chair|Books|1496

     `select title, category, price
      from items
      where category like "%Books%"
      order by price asc;`


    4. Who lives at "6439 Zetta Hills, Willmouth, WY"? Do they have another address?

        Corrine|Little|6439 Zetta Hills|Willmouth|WY

       `select users.first_name, users.last_name, addresses.street, addresses.city, addresses.state
        from users
        join addresses on users.id = addresses.user_id
        where addresses.street = "6439 Zetta Hills" AND addresses.city = "Willmouth" AND addresses.state = "WY";`

        Corrine does have another address, all her addresses are:

        Corrine|Little|6439 Zetta Hills|Willmouth|WY
        Corrine|Little|54369 Wolff Forges|Lake Bryon|CA

        `select users.first_name, users.last_name, addresses.street, addresses.city, addresses.state
         from users
         join addresses on users.id = addresses.user_id
         where users.first_name = "Corrine" AND users.last_name = "Little";`

    5. Correct Virginie Mitchell's address to "New York, NY, 10108".
        Virginie has two addresses in the original database:

        Virginie|Mitchell|12263 Jake Crossing|Roxanehaven|NY|39
        Virginie|Mitchell|83221 Mafalda Canyon|Bahringerland|WY|39

        `select users.first_name, users.last_name, addresses.street, addresses.city, addresses.state, addresses.user_id
         from users
         join addresses on users.id = addresses.user_id
         where users.first_name = "Virginie" AND users.last_name = "Mitchell";`

        Updating all to New York, NY, 10108 (not proven in db; key points are that zip and user_id are integers):

        `update addresses
         set city = "New York", state = "NY", zip = 10108
         where user_id = 39;`

    6. How much would it cost to buy one of each tool?

    7383

    `select sum (price)
     from items
     where category = "Tools";`

    7. How many total items did we sell?

      2125

    `select sum (quantity)
     from orders;`

    8. How much was spent on books?

      420566

    `select sum(items.price * orders.quantity)
     from items
     inner join orders on items.id = orders.item_id
     where items.category = "Books";`


    9. Simulate buying an item by inserting a User for yourself and an Order for that User.

    Inserting user name:
    `insert into users(first_name, last_name, email)
     values ("Enrique", "Carral", "ecarralt@gmail.com");`

     Inserting an my order of 32 Rustic Rubber hats:
     `insert into orders(user_id, item_id, quantity)
      values(51, 99, 32);`
