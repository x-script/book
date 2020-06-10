##### GET 别名

```
axios.get(url, {
	params: {}
}).then(res => {})

axios({
	methods: 'GET',
	url: '',
	params: {}
}).then(res => {})
```

##### POST 别名

```
axios.post(url, data, config
).then(res => {})

const formData = new FromData()
for (let key in data) {
	formData.append(key, data[key])
}
axios.post(url, formData, config
).then(res => {})

axios({
	methods: 'POST',
	url: '',
	data: {}
}).then(res => {})
```

##### PUT 别名

> PUT, PATCH 更新数据

> PUT 提交全部
>
> PATCH 提交更改部分

```
axios.put(url, data, config
).then(res => {})
```

##### PATCH 别名

```
axios.patch(url, data, config
).then(res => {})
```

##### DELETE 别名

```
axios.delete(url, {
	params: {}
}).then(res => {})

axios.delete(url, {
	data: {}
}).then(res => {})

axios({
	methods: 'DELETE',
	url: '',
	params: {},
	data: {}
}).then(res => {})
```

##### 并发（同时处理两个接口的数据）

```
axios.all([
	axios.get(url),
	axios.get(url)
]).then(axios.spread((res1, res2) => {}))
```

##### 实例 axios

```
const instance = axios.create({
	baseURL: url,	// 请求域名
	timeout: 1000	// 超时时间
})

instance.[get, post, put, delete](url).then(res => {})
```

