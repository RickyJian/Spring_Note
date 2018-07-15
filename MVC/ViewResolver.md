# ViewSolver

## ContentNegotiatingViewResolver

* 將資料直接以 JSON 或 XML 格式輸出
* 不自己處理 view 而是透過其他不同 viewResolver 來處理不同的 view
* 擁有最高優先權

## BeanNameViewReolver

* 用 bean 的名稱為返回字串的 view 來渲染視圖

## InternalResourceViewSolver

* 主要設置 前綴 及 後綴
* 常用的 viewResolver