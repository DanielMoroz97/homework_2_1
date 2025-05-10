# homework_2_1
1) Создал таблицу :
CREATE TABLE Sales (
    SaleID SERIAL PRIMARY KEY,
    SaleDate DATE NOT NULL,
    Amount DECIMAL(10, 2) NOT NULL
);

3) Добавил данные :
INSERT INTO Sales (SaleDate, Amount) VALUES
('2021-01-15', 120.50),
('2023-03-20', 85.00),
('2025-05-10', 200.00),
('2023-07-01', 50.75),
('2025-09-25', 150.25),
('2022-11-05', 90.00),
('2024-02-10', 110.00),
('2024-06-15', 180.00),
('2025-12-01', 180.00),
('2024-10-20', 75.50);

3) Функция для определения трети года :
CREATE OR REPLACE FUNCTION GetYearPart(sale_date DATE)
RETURNS INT
AS $$
DECLARE
    month INT;
BEGIN
    IF sale_date IS NULL THEN
        RETURN NULL;
    END IF;

    month := EXTRACT(MONTH FROM sale_date);

    CASE
        WHEN month BETWEEN 1 AND 4 THEN
            RETURN 1;
        WHEN month BETWEEN 5 AND 8 THEN
            RETURN 2;
        WHEN month BETWEEN 9 AND 12 THEN
            RETURN 3;
        ELSE
            RETURN 0;
    END CASE;
END;
$$ LANGUAGE plpgsql;


SELECT
    SaleID,
    SaleDate,
    Amount,
    GetYearPart(SaleDate) AS YearPart
FROM
    Sales;
![image](https://github.com/user-attachments/assets/e784a7c1-e3d0-4685-9b3f-05dc8f0a0efd)
