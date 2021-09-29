# S7-PLC_MySql_MariaDB
## MySql and MariaDB communication FB for Siemens PLC S7-1200 and S7-1500 
### General informations 

    Server user settings:
    The user you want to login to sql server needs to set up 
    using "mysql_native_password" as authentication method. 
    You should create a new user for connecting to plc by 
    typing following into your server commandline:
    1.    CREATE USER 'your_new_username'@'%';
    2.    ALTER USER 'your_new_username'@'%' IDENTIFIED WITH 'mysql_native_password';
    3.    ALTER USER 'your_new_username'@'%' IDENTIFIED BY 'your_new_password';
    4.    GRANT ALL PRIVILEGES ON your_databasename.your_tablename TO 'your_new_username'@'%';
    5.    FLUSH PRIVILEGES;
   
![S7-PLC_MySql_MariaDB_Bild02](https://user-images.githubusercontent.com/10088323/134991945-9647c52d-6c3b-4b9b-902b-713a36e629f7.JPG)

* Tested with:
  * CPU1214C DC/DC/DC FW:V4.3
  * CPU1514-2PN FW:V2.6
  * MySql Server: 8.0.26
  * MariaDB Server: 5.5.5-10.6.4-MariaDB

* Requirements:
  * PLC: S7-1200 or S7-1500
  * Server: must use "mysql_native_password" authentication plugin

* Functionality:
  * Connect with SQL-Server
  * Send PING to SQL-Server
  * Send QUERY String to SQL-Server
  * This client works with client/server protocol
  * Results are saved as Strings
                
* Settings:<br>
  The following constants can be adjusted depending on the expected maximum number of:
  * Colums      --   columns in a result message from Server
  * Rows        --   rows in a result message from Server
  * Stringsize  --   chars in a String of a result (column or row) from Server
  * Buffersize  --   bytes send from Server in a message from Server
 
### Call

![S7-PLC_MySql_MariaDB_Bild01](https://user-images.githubusercontent.com/10088323/134990602-6688fec2-1f42-4570-974f-aeafc84e737e.JPG)

### Parameter

![S7-PLC_MySql_MariaDB_Bild04](https://user-images.githubusercontent.com/10088323/134992000-0deb7db5-b711-4171-844d-7caab2488be3.JPG)


### Video
 
<div align="center"><iframe align="center" src="https://user-images.githubusercontent.com/10088323/134990531-046f66e1-0961-44b2-ace2-500b7aa3dfe5.mp4" title="YouTube video player" frameborder="5" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe></div>

### Status Codes
    Info:
    W#16#0000:  No Error
    W#16#0002:  TCP connection is not established
    Error:
    W#16#0010:  Bad IP-Address, IP-Address should be in this format: '192.168.0.1'
    W#16#0011:  Client capability "CONNECT_ATTRS" is set, but it is not implemented
    W#16#0012:  SQL error, for further information see errorPacket.ERROR_MESSAGE
    W#16#0013:  Client capability "SESSION_TRACK" is set, but it is not implemented
    W#16#0014:  Client capability "CLIENT_CACHE_METADATA" is set, but it is not implemented
    W#16#0015:  Client capability "CLIENT_EXTENDED_TYPE_INFO" is set, but it is not implemented
    W#16#0016:  Input "server" wrong, 1 = Mysql / 2 = MariaDB
    W#16#0017:  The user you want to login to sql Server is set up to 
                authenticate with "caching_sha2_password", 
                change this to "mysql_native_password", or create a new user for connecting to plc by 
                typing following into your server commandline:
                1.    CREATE USER 'your_new_username'@'%';
                2.    ALTER USER 'your_new_username'@'%' IDENTIFIED WITH 'mysql_native_password';
                3.    ALTER USER 'your_new_username'@'%' IDENTIFIED BY 'your_new_password';
                4.    GRANT ALL PRIVILEGES ON your_databasename.your_tablename TO 'your_new_username'@'%';
                5.    FLUSH PRIVILEGES;
    W#16#0020:  Wrong packet type recieved after login request, expectet OK or ERROR
    W#16#0021:  Recieved LOCALINFILE packet, but it is not implemented
    W#16#0023:  Number of colums in result data is greater than the set value number of columns, 
                adjust the constant "Columns"
    W#16#0024:  Number of recieved bytes is greater than the set value number of bytes, 
                adjust the constant "Buffersize"
    W#16#0025:  Number of rows in result data is greater than the set value number of rows, 
                adjust the constant "Rows"

### Server status:
        IN_TRANS                    00000000 00000001
        AUTO_COMMIT                 00000000 00000010
        MULTI_QUERY(unused)         00000000 00000100
        MORE_RESULTS_EXISTS         00000000 00001000
        BAD_INDEX_USED              00000000 00010000
        NO_INDEX_USED               00000000 00100000
        CURSOR_EXISTS               00000000 01000000
        LAST_ROW_SENT               00000000 10000000
        DB_DROPPED                  00000001 00000000
        NO_BACKSLASH_ESCAPES        00000010 00000000
        METADATA_CHANGED            00000100 00000000
        QUERY_WAS_SLOW              00001000 00000000
        PS_OUT_PARAMS               00010000 00000000
        IN_TRANS_READONLY           00100000 00000000
        SESSION_STATE_CHANGED       01000000 00000000

### Capabilities standard:
        CLIENT_MYSQL                00000000 00000001
        FOUND_ROWS                  00000000 00000010
        LONG_FLAG                   00000000 00000100
        CONNECT_WITH_DB             00000000 00001000
        NO_SCHEMA                   00000000 00010000
        COMPRESS                    00000000 00100000
        ODBC                        00000000 01000000
        LOCAL_FILES                 00000000 10000000
        IGNORE_SPACE                00000001 00000000
        SPEAKS_PROTOCOL_41          00000010 00000000
        CLIENT_INTERACTIVE          00000100 00000000
        SSL                         00001000 00000000
        IGNORE_SIGPIPE              00010000 00000000
        TRANSACTIONS                00100000 00000000
        RESERVED                    01000000 00000000
        AUTH_PROTOCOL_41            10000000 00000000
       
### Capabilities extended:
        MULTI_STATEMENTS            00000000 00000001
        MULTI_RESULTS               00000000 00000010
        PS_MULTI_RESULTS            00000000 00000100
        PLUGIN_AUTH                 00000000 00001000
        CONNECT_ATTRS               00000000 00010000
        PLUGIN_AUTH_LENENC          00000000 00100000
        HANDLE_EXPIRED_PASSWORDS    00000000 01000000
        SESSION_TRACK               00000000 10000000
        DEPRECATE_EOF               00000001 00000000
        
### Capabilities mariaDB:
        CLIENT_PROGRESS                      00000001
        CLIENT_COM_MULTI                     00000010
        CLIENT_STMT_BULK_OPERATIONS          00000100
        CLIENT_EXTENDED_TYPE_INFO            00001000
        CLIENT_CACHE_METADATA                00010000

### Field Details Flag:
        NOT_NULL                    00000000 00000001
        PRIMARY_KEY                 00000000 00000010
        UNIQUE_KEY                  00000000 00000100
        MULTIPLE_KEY                00000000 00001000
        BLOB                        00000000 00010000
        UNSIGNED                    00000000 00100000
        ZEROFILL_FLAG               00000000 01000000
        BINARY_COLLATION            00000000 10000000
        ENUM                        00000001 00000000
        AUTO_INCREMENT              00000010 00000000
        TIMESTAMP                   00000100 00000000
        SET                         00001000 00000000
        NO_DEFAULT_VALUE_FLAG       00010000 00000000
        ON_UPDATE_NOW_FLAG          00100000 00000000
        NUM_FLAG                    10000000 00000000

### Field Types:
        00: DECIMAL
        01: TINY
        02: SHORT
        03: LONG
        04: FLOAT
        05: DOUBLE
        06: NULL
        07: TIMESTAMP
        08: LONGLONG
        09: INT24
        10: DATE
        11: TIME
        12: DATETIME
        13: YEAR
        14: NEWDATE
        15: VARCHAR
        16: BIT
        17: TIMESTAMP2
        18: DATETIME2
        19: TIME2
        245: JSON
        246: NEWDECIMAL
        247: ENUM
        248: SET
        249: TINY_BLOB
        250: MEDIUM_BLOB
        251: LONG_BLOB
        252: BLOB
        253: VAR_STRING
        254: STRING
        255: GEOMETRY

### Collation:
        01: big5        | big5_chinese_ci
        03: dec8        | dec8_swedish_ci
        04: cp850       | cp850_general_ci
        06: hp8         | hp8_english_ci
        07: koi8r       | koi8r_general_ci
        08: latin1      | latin1_swedish_ci
        09: latin2      | latin2_general_ci
        10: swe7        | swe7_swedish_ci
        11: ascii       | ascii_general_ci
        12: ujis        | ujis_japanese_ci
        13: sjis        | sjis_japanese_ci
        16: hebrew      | hebrew_general_ci
        18: tis620      | tis620_thai_ci
        19: euckr       | euckr_korean_ci
        22: koi8u       | koi8u_general_ci
        24: gb2312      | gb2312_chinese_ci
        25: greek       | greek_general_ci
        26: cp1250      | cp1250_general_ci
        28: gbk         | gbk_chinese_ci
        30: latin5      | latin5_turkish_ci
        32: armscii8    | armscii8_general_ci
        33: utf8        | utf8_general_ci
        35: ucs2        | ucs2_general_ci
        36: cp866       | cp866_general_ci
        37: keybcs2     | keybcs2_general_ci
        38: macce       | macce_general_ci
        39: macroman    | macroman_general_ci
        40: cp852       | cp852_general_ci
        41: latin7      | latin7_general_ci
        51: cp1251      | cp1251_general_ci
        54: utf16       | utf16_general_ci
        56: utf16le     | utf16le_general_ci
        57: cp1256      | cp1256_general_ci
        59: cp1257      | cp1257_general_ci
        60: utf32       | utf32_general_ci
        63: binary      | binary
        92: geostd8     | geostd8_general_ci
        95: cp932       | cp932_japanese_ci
        97: eucjpms     | eucjpms_japanese_ci
        248: gb18030    | gb18030_chinese_ci
        255: utf8mb4    | utf8mb4_0900_ai_ci
