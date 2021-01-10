# Soru 1
dsmbootcamp.sample.semi_structured_hw tablosunda 2 kişinin sahip olduğu araç bilgileri ve bu araçları satın alma tarihleri yer almaktadır. Tablodaki kolonların açıklamaları aşağıdaki gibidir. ​

    name: Araç sahibinin adı
    car: Araç id'si ve model bilgilerini içermektedir.
    manufacture: Araç id'si, üretim yılı ve üretildiği ülke bilgilerini içermektedir.
    purchase: Araç id'si ve satın alma tarihlerini içermektedir.

​ Beklenen dsmbootcamp.sample.semi_structured_hw tablosunu kullanarak dsmbootcamp.sample.semi_structured_hw_expected tablosundaki veriyi oluşturmaktır.



~~~  SQL 

select name ,
        array(select as struct car.id as car_id,
                    car.model as car_model,
                    manufacture.year as year, 
                    array(select as struct TIMESTAMP_ADD(purchase.date, INTERVAL 3 HOUR)  from unnest(purchase) AS purchase)
                from  unnest(car) as car
                cross join unnest(manufacture) as manufacture on car.id = manufacture.id ) as newStruct, 
from berker_ot.semi_structured_hw



~~~ 
