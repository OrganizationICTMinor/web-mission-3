##Миссия 3 - Скайнет
ссылка на RuTube :) (https://rutube.ru/video/private/05a097ced53f8746a04fedbc94f92ec2/?p=lg7zC8RggSo5CCvAxEjHnQ)

##Select'ы
1. получить список юзернеймов пользователей
   ```sql
   select username from users
   ```
2. получить кол-во отправленных сообщений каждым пользователем:
   username - number of sent messages
   ```sql
   select username, count(*) as number_of_sent_messages
   from users as u join messages as m on u.id = m.from
   group by username
   ```
    
3. получить пользователя с самым большим кол-вом полученных сообщений и само количество
   username - number of received messages
  ```sql
  select username, count(*) as number_of_received_messages
  from users as u join messages as m on u.id = m.to
  group by username
  order by number_of_received_messages desc
  limit 1
  ```
4. Получить среднее кол-во сообщений, отправленное каждым пользователем
  ```sql
  select round(
  (select avg(t.number_of_sent_messages)
  from
  (select username, count(*) as number_of_sent_messages
  from users as u join messages as m on u.id = m.from
  group by username) as t)
  , 2)
  ```
