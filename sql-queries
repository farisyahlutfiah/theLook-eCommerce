---(1) Jumlah pengguna dari berbagai negara
SELECT country, COUNT(DISTINCT id) AS jumlah_pengguna FROM `bigquery-public-data.thelook_ecommerce.users`
GROUP BY country
ORDER BY jumlah_pengguna DESC
LIMIT 5;

SELECT
  country,
  COUNTIF(EXTRACT(YEAR FROM created_at) = 2021) AS tahun_2021,
  COUNTIF(EXTRACT(YEAR FROM created_at) = 2022) AS tahun_2022,
  COUNTIF(EXTRACT(YEAR FROM created_at) = 2023) AS tahun_2023,
FROM
  `bigquery-public-data.thelook_ecommerce.users`
GROUP BY
  country
ORDER BY
  country ASC;

WITH DataTahun AS (
  SELECT
    country,
    SUM(CASE WHEN EXTRACT(YEAR FROM created_at) = 2021 THEN 1 ELSE 0 END) AS tahun_2021,
    SUM(CASE WHEN EXTRACT(YEAR FROM created_at) = 2022 THEN 1 ELSE 0 END) AS tahun_2022,
    SUM(CASE WHEN EXTRACT(YEAR FROM created_at) = 2023 THEN 1 ELSE 0 END) AS tahun_2023
  FROM
    `bigquery-public-data.thelook_ecommerce.users`
  GROUP BY
    country
)

SELECT
  country,
  tahun_2021,
  tahun_2022,
  tahun_2023,
  tahun_2021 + tahun_2022 + tahun_2023 AS total_pengguna
FROM
  DataTahun
ORDER BY
  total_pengguna DESC;



---perbandingan jenis kelamin pembeli
SELECT 
  gender,
  COUNT(DISTINCT user_id) jumlah_pelanggan
FROM  `bigquery-public-data.thelook_ecommerce.orders`
GROUP BY gender;

SELECT * FROM `bigquery-public-data.thelook_ecommerce.inventory_items`;

---(2) 5 kategori produk paling banyak terjual
SELECT DISTINCT t1.product_category AS kategori_produk,
  COUNT(t1.sold_at) terjual
FROM `bigquery-public-data.thelook_ecommerce.inventory_items` AS t1
GROUP BY kategori_produk
ORDER BY terjual DESC
LIMIT 5;

---(3) 3 kategori produk paling sedikit terjual
SELECT DISTINCT t1.product_category AS kategori_produk,
  COUNT(t1.sold_at) terjual
FROM `bigquery-public-data.thelook_ecommerce.inventory_items` AS t1
GROUP BY kategori_produk
ORDER BY terjual ASC
LIMIT 3;

---(4) rata rata durasi pemenyewaan sepeda diatas 40 menit
SELECT start_station_name, ROUND(AVG(duration_minutes),2) AS rata_rata_durasi, status FROM `bigquery-public-data.austin_bikeshare.bikeshare_trips` AS t1
JOIN `bigquery-public-data.austin_bikeshare.bikeshare_stations` AS t2 on t1.start_station_id = t2.station_id
GROUP BY status, start_station_name
HAVING rata_rata_durasi > 40
ORDER BY rata_rata_durasi DESC;

---(5) Data Tahun dan Jumlah Kejahatan
SELECT * FROM `bigquery-public-data.chicago_crime.crime`;

SELECT year AS tahun, COUNT(*) AS jumlah_kejahatan
FROM `bigquery-public-data.chicago_crime.crime`
GROUP BY year
ORDER BY year;

---(6) mengidentifikasi Jenis Kejahatan yang Paling Umum
SELECT primary_type AS jenis_kejahatan, COUNT(*) as total_kejahatan
FROM `bigquery-public-data.chicago_crime.crime`
GROUP BY jenis_kejahatan
ORDER BY total_kejahatan DESC
LIMIT 1;

---(7)Melihat Pola Kejahatan Berdasarkan Waktu:
SELECT EXTRACT(MONTH FROM date) as bulan, COUNT(*) as total_kejahatan
FROM `bigquery-public-data.chicago_crime.crime`
WHERE year = 2023
GROUP BY bulan
ORDER BY bulan;

---Reaksi yang Paling Sering Terjadi pada Kelompok Usia Tertentu:
SELECT consumer_age, reactions, COUNT(*) as jumlah_laporan
FROM `bigquery-public-data.fda_food.food_events`
GROUP BY consumer_age, reactions
ORDER BY jumlah_laporan DESC;

SELECT MIN(age) AS UmurTermuda, MAX(age) AS UmurTertua
FROM `bigquery-public-data.thelook_ecommerce.users`;

SELECT
    CASE
        WHEN age BETWEEN 12 AND 21 THEN '12-21'
        WHEN age BETWEEN 22 AND 31 THEN '22-31'
        WHEN age BETWEEN 32 AND 41 THEN '32-41'
        WHEN age BETWEEN 42 AND 51 THEN '42-51'
        WHEN age BETWEEN 52 AND 61 THEN '52-61'
        WHEN age BETWEEN 62 AND 70 THEN '62-70'
        ELSE 'Tidak Diketahui'
    END AS RangeUmur,
    COUNT(*) AS JumlahPengguna
FROM `bigquery-public-data.thelook_ecommerce.users`
GROUP BY RangeUmur
ORDER BY RangeUmur; 
