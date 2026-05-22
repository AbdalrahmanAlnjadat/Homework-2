# Home work 2
#Abdalrahman ALNJADAT 
#202311140
SET SERVEROUTPUT ON;

DECLARE
    TODAY DATE := SYSDATE;
    TOMORROW TODAY%TYPE;
BEGIN
    DBMS_OUTPUT.PUT_LINE('Hello World');
    TOMORROW := TODAY + 1;
    DBMS_OUTPUT.PUT_LINE('Today is: ' || TODAY);
    DBMS_OUTPUT.PUT_LINE('Tomorrow will be: ' || TOMORROW);
END;
/

DECLARE
    my_date DATE := SYSDATE;
    v_last_day DATE;
BEGIN
    DBMS_OUTPUT.PUT_LINE('Formatted Date: ' || TO_CHAR(my_date, 'Month DD, YYYY'));
    v_last_day := LAST_DAY(my_date);
    DBMS_OUTPUT.PUT_LINE('Last day of this month: ' || v_last_day);
END;
/

DECLARE
    my_date DATE := SYSDATE;
    v_future_date DATE;
    v_months_between NUMBER(6, 2);
BEGIN
    v_future_date := my_date + 45;
    v_months_between := MONTHS_BETWEEN(v_future_date, my_date);
    DBMS_OUTPUT.PUT_LINE('Today: ' || my_date);
    DBMS_OUTPUT.PUT_LINE('Date after 45 days: ' || v_future_date);
    DBMS_OUTPUT.PUT_LINE('Months between: ' || v_months_between);
END;
/

CREATE TABLE countries (
    country_name VARCHAR2(50),
    median_age NUMBER(6, 2)
);

INSERT INTO countries (country_name, median_age) VALUES ('Japan', 49.50);
INSERT INTO countries (country_name, median_age) VALUES ('Jordan', 23.80);
INSERT INTO countries (country_name, median_age) VALUES ('Canada', 41.10);
COMMIT;

DECLARE
    CURSOR c_country IS
        SELECT country_name, median_age 
        FROM countries
        WHERE country_name = 'Japan';
        
    v_country_name countries.country_name%TYPE;
    v_median_age   countries.median_age%TYPE;
BEGIN
    OPEN c_country;
    FETCH c_country INTO v_country_name, v_median_age;
    
    IF c_country%FOUND THEN
        DBMS_OUTPUT.PUT_LINE('The median age in ' || v_country_name || ' is ' || v_median_age || '.');
    ELSE
        DBMS_OUTPUT.PUT_LINE('Country not found.');
    END IF;
    
    CLOSE c_country;
END;
/
