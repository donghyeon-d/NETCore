# Database

# MySQL
## Databases
1. MasterDataDB
    > MasterData를 업데이트 할 때는 모든 내용을 다 덮어씀. 그렇기 때문에 database 전체를 지웠다가 다시 생성함
    ``` sql
    DROP DATABASE IF EXISTS MasterDataDB;
    CREATE DATABASE IF NOT EXISTS MasterDataDB;
    ```
2. AccountDB
    ``` sql
    CREATE DATABASE IF NOT EXISTS AccountDB;
    ```
3. GameDB
    ``` sql
    CREATE DATABASE IF NOT EXISTS GameDB;
    ```

## Tables
### 1. MasterDataDB
> MasterData를 업데이트 할 때는 모든 내용을 다 덮어씀. 그렇기 때문에 table 전체를 지웠다가 다시 생성함
* **Item**
    ``` sql
    USE `MasterDataDB`;

    DROP TABLE IF EXISTS MasterDataDB.`Item`;
    CREATE TABLE IF NOT EXISTS MasterDataDB.`Item`
    (
        Code INT AUTO_INCREMENT PRIMARY KEY COMMENT '아이템 번호',
        Name VARCHAR(50) NOT NULL UNIQUE COMMENT '아이템 이름',
        Attribute INT NOT NULL COMMENT '특성',
        Sell BIGINT NOT NULL COMMENT '판매 금액',
        Buy BIGINT NOT NULL COMMENT '구입 금액',
        UseLv INT NOT NULL COMMENT '사용 가능 레벨',
        Attack BIGINT NOT NULL COMMENT '공격력',
        Defence BIGINT NOT NULL COMMENT '방어력',
        Magic BIGINT NOT NULL COMMENT '마법력',
        EnhanceMaxCount INT NOT NULL COMMENT '최대 강화 가능 횟수',
        PossessionCount INT NOT DEFAULT 1 COMMENT '겹침 가능 개수',
    ) COMMENT '아이템 정보 테이블';
    ```
* **ItemAttribute**
    ``` sql
    USE `MasterDataDB`;

    DROP TABLE IF EXISTS MasterDataDB.`ItemAttribute`;
    CREATE TABLE IF NOT EXISTS MasterDataDB.`ItemAttribute`
    (
        Name VARCHAR(50) NOT NULL UNIQUE COMMENT '특성 이름',
        Code INT AUTO_INCREMENT PRIMARY KEY COMMENT '아이템 번호',
    ) COMMENT '아이템 속성 정보 테이블';
    ```
* **AttendanceReward**
    ``` sql
    USE `MasterDataDB`;

    DROP TABLE IF EXISTS MasterDataDB.`AttendanceReward`;
    CREATE TABLE IF NOT EXISTS MasterDataDB.`AttendanceReward`
    (
        Code INT AUTO_INCREMENT PRIMARY KEY COMMENT '보상 번호',
        ItemCode INT NOT NULL COMMENT '아이템 번호',
        Count BIGINT NOT NULL COMMENT '아이템 개수',
    ) COMMENT '출석부 보상 정보 테이블';
    ```
* **InAppProduct**
    ``` sql
    USE `MasterDataDB`;

    DROP TABLE IF EXISTS MasterDataDB.`InAppProduct`;
    CREATE TABLE IF NOT EXISTS MasterDataDB.`InAppProduct`
    (
        Code INT NOT NULL COMMENT '상품 번호',
        ItemCode INT NOT NULL COMMENT '아이템 번호',
        ItemName VARCHAR(50) NOT NULL COMMENT '아이템 이름',
        ItemCount BIGINT NOT NULL COMMENT '아이템 개수',
    ) COMMENT '인생 삼풍 정보 테이블 묶음상품';
    ```
* **StageItem**
    ``` sql
    USE `MasterDataDB`;

    DROP TABLE IF EXISTS MasterDataDB.`StageItem`;
    CREATE TABLE IF NOT EXISTS MasterDataDB.`StageItem`
    {
        Code INT NOT NULL COMMENT '스테이지 단계',
        ItemCode INT NOT NULL COMMENT '파밍 가능 아이템'
    }
    ```
* **StageAttackNPC**
    ``` sql
    USE `MasterDataDB`;

    DROP TABLE IF EXISTS MasterDataDB.`StageAttackNPC`;
    CREATE TABLE IF NOT EXISTS MasterDataDB.`StageAttackNPC`
    {
        Code INT NOT NULL COMMENT '스테이지 단계',
        NPCCode INT NOT NULL COMMENT '공격 NPC',
        ItemCount INT NOT NULL COMMENT '공격 NPC 개수',
        Exp INT NOT NULL COMMENT '1개당 보상 경험치'
    }
    ```

### 2. AccountDB
> 계정 관리를 위한 Database
* **Account**
    ``` sql
    CREATE TABLE IF NOT EXISTS MasterDataDB.`Account`
    {
        Code INT NOT NULL AUTO_INCREMENT COMMENT '계정 번호',
        ID VARCHAR(50) PRIMARY KEY COMMENT '계정 이름',
        PW VARCHAR(100) NOT NULL COMMENT '비밀번호',
    }
    ```

### 3. GameDB
* 