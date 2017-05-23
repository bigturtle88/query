/*  Для заданного списка товаров получить названия всех категорий, в которых
представлены товары;  */

SELECT `category`.`title` 
FROM `category` 
LEFT JOIN `product_in_category` ON `product_in_category`.`category_id` = `category`.`id` 
WHERE `product_in_category`.`product_id` 
IN ( 1, 2, 3, 4, 5 )  GROUP BY `category`.`id`;

/* Для заданной категории получить список предложений всех товаров из этой категории и
ее дочерних категорий; */

SELECT `product_in_category`.`product_id` 
FROM `product_in_category`
 WHERE `product_in_category`.`category_id` IN (
  SELECT `category`.`id` FROM `category` WHERE `category`.`id` IN (10,5) OR `category`.`parent_id` IN (10,5)
 ) GROUP BY  `product_id`;

/* Для заданного списка категорий получить количество предложений товаров в каждой
категории;*/

SELECT COUNT(`product_in_category`.`product_id` ) as count ,
`product_in_category`.`category_id` FROM `product_in_category` WHERE `product_in_category`.`category_id` IN ( 10,50 ) 
GROUP BY  `product_in_category`.`category_id`;

/* Для заданного списка категорий получить общее количество уникальных предложений
товара; */

SELECT COUNT(DISTINCT  `product_in_category`.`product_id`) as count ,`product_in_category`.`category_id`
 FROM `product_in_category` WHERE `product_in_category`.`category_id` IN ( 10,5,7 ) GROUP BY  `product_in_category`.`category_id`;
 
/* Для заданной категории получить ее полный путь в дереве (breadcrumb, «хлебные
крошки»).*/
SELECT `l0`.`id` AS `lo`, `l1`.`id` AS `l1`, `l2`.`id` AS `l2`, `l3`.`id` AS `l3`
FROM `category` AS l0
LEFT JOIN `category` AS `l1` ON `l1`.`id` = `l0`.`parent_id`
LEFT JOIN `category` AS `l2` ON `l2`.`id` = `l1`.`parent_id`
LEFT JOIN `category` AS `l3` ON `l3`.`id` = `l2`.`parent_id`
WHERE `l0`.`id` = 280;


