# JPA (JAVA Persistence API)

## 實體註解

| 名稱 | 說明 |
|------|------|
| @Entity | 註解 class 為實體 |
| @Table | 註解 class 為實體 |
| @MappedSuperclass | 用在 實體(entity) 繼承上 |
| @Embeddable | |

### @Entity

```java

@Entity
public class Authority {

}

```
### @Table

```java

@Entity
@Table(name = "authority", schema = "dbo", catalog = "dbname")
public class Authority {

}


```

### 主鍵嵌入

| 名稱 | 說明 |
|------|------|
| @IdClass | |
| @@EmbeddedId | |


### 欄位註解