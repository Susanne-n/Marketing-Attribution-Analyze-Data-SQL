SELECT *
FROM page_visits
LIMIT 10;

/* The campaigns and sources that CoolTShirts uses */
SELECT DISTINCT utm_campaign, utm_source
FROM page_visits;

/* The different pages on the CoolTShirts website, with amount of visitors per page */
SELECT page_name, COUNT(DISTINCT user_id)
FROM page_visits
GROUP BY 1;

/* Amount of first touches that each campaign is responsible for */
WITH first_touch AS (
    SELECT user_id,
        MIN(timestamp) as first_touch_at
    FROM page_visits
    GROUP BY user_id)
SELECT ft.user_id,
    ft.first_touch_at,
    pv.utm_source,
		pv.utm_campaign,
    COUNT(utm_campaign)
FROM first_touch ft
JOIN page_visits pv
    ON ft.user_id = pv.user_id
    AND ft.first_touch_at = pv.timestamp
GROUP BY utm_campaign
ORDER BY 5 DESC;

/* Amount of last touches that each campaign is responsible for */
WITH last_touch AS (
  SELECT user_id,
      MAX(timestamp) AS last_touch_at
  FROM page_visits
  GROUP BY user_id)
SELECT lt.user_id,
    lt.last_touch_at,
    pv.utm_source,
    pv.utm_campaign,
    COUNT(utm_campaign)
FROM last_touch AS lt
JOIN page_visits AS pv
    ON lt.user_id = pv.user_id
    AND lt.last_touch_at = pv.timestamp
GROUP BY utm_campaign
ORDER BY 5 DESC;

/* Amount of visitors that make a purchase */
SELECT COUNT(DISTINCT user_id)
FROM page_visits
WHERE page_name = '4 - purchase';

/* Amount of last touches on the purchase page that each campaign is responsible for */
WITH last_touch AS (
  SELECT user_id,
      MAX(timestamp) AS last_touch_at
  FROM page_visits
  WHERE page_name = '4 - purchase'
  GROUP BY user_id)
SELECT lt.user_id,
    lt.last_touch_at,
    pv.utm_source,
    pv.utm_campaign,
    COUNT(utm_campaign)
FROM last_touch AS lt
JOIN page_visits AS pv
    ON lt.user_id = pv.user_id
    AND lt.last_touch_at = pv.timestamp
GROUP BY utm_campaign
ORDER BY 5 DESC;
