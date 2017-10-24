# AOP (Aspect-Oriented Programming) 面相導向程式設計

主要用來解耦，讓一組類別可以共享相同行為。由於在 OOP 中透過繼承與介面實現會導致偶和度上升，且繼承只能單一繼承，阻礙更多行為添加到一組類別上。
<br>
常用在 交易管理(Transactional)、事件處理(Log)

## Annotation

| 名稱 | 說明 |
|------|------|
| @Aspect | 宣告切面 |
| @After | 定義 advice 可直接將攔截規則設為參數 |
| @Before | 定義 advice 可直接將攔截規則設為參數 |
| @Around | 定義 advice 可直接將攔截規則設為參數 |
| @PointCut | 定義攔截規則 |