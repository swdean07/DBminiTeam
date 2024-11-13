CREATE TABLE board (
    boardNo NUMBER PRIMARY KEY,
    title VARCHAR2(100) NOT NULL,
    content VARCHAR2(1000) NOT NULL,
    writer VARCHAR2(50) NOT NULL,
    empno NUMBER,
    regdate DATE DEFAULT SYSDATE,
    CONSTRAINT fk_emp FOREIGN KEY (empno)
        REFERENCES emp(empno)
        ON DELETE CASCADE
);

CREATE SEQUENCE board_seq
    START WITH 1
    INCREMENT BY 1
    NOCYCLE
    MAXVALUE 9999999999
    MINVALUE 1
    CACHE 20;

CREATE OR REPLACE TRIGGER trg_board_no
BEFORE INSERT ON board
FOR EACH ROW
BEGIN
    IF :NEW.boardNo IS NULL THEN
        SELECT board_seq.NEXTVAL INTO :NEW.boardNo FROM dual;
    END IF;
END;
/
