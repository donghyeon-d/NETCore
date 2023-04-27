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
        EnhanceMaxCount TINYINT NOT NULL COMMENT '최대 강화 가능 횟수',
        MaxStack INT NOT NULL DEFAULT 1 COMMENT '겹침 가능 개수'
    ) COMMENT '아이템 정보 테이블';
    ```
* **ItemAttribute**
    ``` sql
    USE `MasterDataDB`;

    DROP TABLE IF EXISTS MasterDataDB.`ItemAttribute`;
    CREATE TABLE IF NOT EXISTS MasterDataDB.`ItemAttribute`
    (
        Name VARCHAR(50) NOT NULL UNIQUE COMMENT '특성 이름',
        Code INT AUTO_INCREMENT PRIMARY KEY COMMENT '아이템 번호'
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
        Count INT NOT NULL COMMENT '아이템 개수'
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
        ItemCount INT NOT NULL COMMENT '아이템 개수'
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
        ID INT AUTO_INCREMENT PRIMARY KEY COMMENT '계정 고유번호',
        UserID VARCHAR(50) COMMENT '계정 이름',
        PW VARCHAR(100) NOT NULL COMMENT '비밀번호'
    }
    ```

### 3. GameDB
* **Character**
    ``` sql
    CREATE TABLE IF NOT EXISTS MasterDataDB.`Character`
    {
        UID INT PRIMARY KEY COMMENT '계정 고유번호',
        Level INT NOT NULL DEFAULT 1 COMMENT '레벨',
        Exp INT NOT NULL DEFALUT 0 COMMENT '누적 경험치',
        Attack INT NOT NULL DEFALUT 10 COMMENT '공격력',
        Defence INT NOT NULL DEFALUT 10 COMMENT '방어력',
        Magic INT NOT NULL DEFALUT 10 COMMENT '마법력',
        TotalAttack INT NOT NULL DEFALUT 0 COMMENT '총 공격력',
        TotalDefence INT NOT NULL DEFALUT 0 COMMENT '총 방어력',
        TotalMagic INT NOT NULL DEFALUT 0 COMMENT '총 마법력'
    }
    ```
* **Inventory**
    * 케릭터가 갖고 있는 아이템
    * SELECT * FROM Character WHERE UID = '조회하고 싶은 계정명'
    ``` sql
    CREATE TABLE IF NOT EXISTS MasterDataDB.`Character`
    {
        UID INT NOT NULL COMMENT '계정 고유번호',
        ItemID INT AUTO_INCREMENT PRIMARY KEY COMMENT '아이템 고유번호',
        ItemCode INT NOT NULL COMMENT '아이템 번호',
        ItemCount INT NOT NULL COMMENT '아이템 개수',
        Attack BIGINT NOT NULL COMMENT '공격력',
        Defence BIGINT NOT NULL COMMENT '방어력',
        Magic BIGINT NOT NULL COMMENT '마법력',
        EnhanceLevel TINYINT NOT NULL COMMENT '강화 레벨',
        RemainingEnhanceCount TINYINT NOT NULL COMMENT '남은 강화 횟수',
        Destructed BOOLEAN DEFAULT FALSE COMMENT '파괴 유무'
    }
    ```
* **Equipment**
    ``` sql
    CREATE TABLE IF NOT EXISTS MasterDataDB.`Equipment`
    {
        UID INT PRIMARY KEY COMMENT '계정 고유번호',
        WeaponID INT DEFAULT NULL COMMENT '무기 아이템 번호',
        ShieldID INT DEFAULT NULL COMMENT '방패 아이템 번호',
        HatID INT DEFAULT NULL COMMENT '모자 아이템 번호',
        ClothID INT DEFAULT NULL COMMENT '옷 아이템 번호',
        ShoesID INT DEFAULT NULL COMMENT '신발 아이템 번호',
        GloveID INT DEFAULT NULL COMMENT '장갑 아이템 번호',
        CloakID INT DEFAULT NULL COMMENT '망토 아이템 번호'
    }
    ```
