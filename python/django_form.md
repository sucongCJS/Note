# request and post
- any request that could be used to change the state of the system - for example, a request that makes changes in the database - should use POST. GET should be used only for requests that do not affect the state of the system. 

---

# what is session
- Session是在服务端保存的一个数据结构，用来跟踪用户的状态，这个数据可以保存在集群、数据库、文件中
- Session指的是服务器端为客户端所开辟的存储空间，在其中保存的信息就是用于保持状态
- a session is a collection of data stored on the server and asscoiated with the given user(usually via a cookie containing an id code)

# what is cookies
- Cookie是客户端保存用户信息的一种机制，用来记录用户的一些信息，也是实现Session的一种方式
- a cookie is a bit of data stored by the browser and sent to the server with every request

# the relationship between session and cookies
- 服务端的session的实现对客户端的cookie有依赖关系的，上面我讲到服务端执行session机制时候会生成session的id值，这个id值会发送给客户端，客户端每次请求都会把这个id值放到http请求的头部发送给服务端，而这个id值在客户端会保存下来，保存的容器就是cookie，因此当我们完全禁掉浏览器的cookie的时候，服务端的session也会不能正常使用(ASP maybe could solve this)