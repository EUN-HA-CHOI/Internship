![image](https://github.com/EUN-HA-CHOI/Internship/assets/97012561/6b628130-55e3-4e13-bd8f-f12b54f87c5d)

어드민 페이지에서 삭제 기능을 구현 하다가 마지막에 url 에 대한 에러코드가 발생했다.
회사 컴퓨터로 api 호출을 위해 로컬 호스트를 적는 것이다. 

- 수정 전 코드 
```
const handleRemove = async(id) => {
setInfo(info => info.filter(item => item.id !== id));
let url = 'admin/agency/' + `?id=${id}`
let result = await comApiCall({method:'DELETE'},url);
console.log("result:::",result)
//debugger;
}
```

- 수정 후 코드 
```
const handleRemove = async(id) => {
setInfo(info => info.filter(item => item.id !== id));
let url = 'https://172.16.10.40:7272/admin/agency/identifier' + `?id=${id}`
let result = await comApiCall({method:'DELETE'},url);
console.log("result:::",result)
//debugger;
}
```

