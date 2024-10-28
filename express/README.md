## [Udemy - NodeJS 완벽 가이드(39시간14분)](https://www.udemy.com/course/nodejs-mvc-rest-apis-graphql-deno/)

### 1. 소개(40분) 👌🏻

### 2. 선택 사항: JavaScript - 간단한 복습

### 3. 기본 개념 이해(94분) 👌🏻

- 모듈 소개 01:50
- 웹 작동 방식 04:11
- Node 서버 생성 13:22
  → 서버 생성 방법? 몇 개의 서버 코어 모듈이 있음

  - http: 서버를 생성하거나, 요청을 보내는 것 같은 작업, 여러 서버 간에 소통할 수 있음
  - https: 모든 전송 데이터가 암호화되는 ssl 서버를 출시할 때 도움이 됨
  - 그외 fs, path, os가 있음

  ```jsx
  // server.js 또는 app.js로 이름을 붙임

  const http = require("http"); // 파일을 불러올 수 있음

  function rqListener(req, res) {}

  http.createServer(rqListener);
  // 이것이 node.js의 주된 이벤트 드리븐 아키텍쳐(EDA)

  const server = http.createServer((req, res) => {
    console.log(req);
  });
  // 이렇게도 가능, 콜백 함수

  server.listen(3000);
  // 터미널에서 `node app.js` 실행 후, localhost:3000으로 들어가면 터미널에 콘솔 로그가 남음
  ```

- Node의 라이프사이클 및 이벤트 루프 04:53

  - Node.js Program Lifecycle
    ![image](https://github.com/user-attachments/assets/7beb715c-6161-477b-8630-887babdb98ab)

    node app.js 실행 → start script → 코드 분석, 변수와 함수 등록 (전체 코드를 읽고 실행) → 이벤트 루프 (작업이 남아 있는 한 이벤트 리스너가 계속 작동함 → 이것이 node 애플리케이션) → 제거해야 한다면 process.exit

  ```jsx
  const http = require("http");

  const server = http.createServer((req, res) => {
    console.log(req);
    process.exit(); // 프로세스 종료
  });

  server.listen(3000);
  ```

- Node.js 프로세스 제어 00:09
  실행 중인 Node.js 서버를 종료하고 싶으신가요?
  `node app.js` 파일을 실행해 서버를 시작한 곳에서 Terminal이나 명령 프롬프트창에서 `Ctrl+C`를 누르세요.
- 요청의 이해 03:10

  ```jsx
  const http = require("http");

  const server = http.createServer((req, res) => {
    console.log(req.url, req.method, req.headers); // 요청에 대한 정보에 접근하는 법 ex) `/ GET { ... }`
  });

  server.listen(3000);
  ```

- 응답 전송 05:37

  ```jsx
  const http = require("http");

  const server = http.createServer((req, res) => {
    res.setHeader("Content-Type", "text/html"); // 브라우저가 이해하고 받아들이는 값
    res.write("<html>");
    res.write("<head><title>My First Page</title></head>");
    res.write("<body><h1>hellow from  my Node.js Server!</h1></body>");
    res.write("</html>");
    res.end();
  });

  server.listen(3000);
  ```

- 요청과 응답 헤더 00:22
  요청 및 응답 모두 메타데이터를 A에서 B로 이동하기 위해 Http 헤더가 추가됩니다.
  사용 가능한 헤더와 각각의 역할을 간략하게 알아보려면 다음 문서를 참고하세요.
  https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers

  보다 깊은 수준의 지식을 위한 유용한 자료지만, **목록을 암기할 필요는 없습니다!** 강의를 통해 많은 헤더를 접하게 될 것이며 필요할 때마다 설명드릴게요.

- 라우터 요청 05:48

  ```jsx
  const http = require('http');

  const server = http.createServer((req, res) => {
  	const url = req.url;

  	if(url === '/') {
  		res.setHeader('Content-Type', 'text/html');
  		res.write('<html>');
  		res.write('<head><title>Enter Message</title></head>');
  		res.write('<body><form action='/message' method='POST'><input type='text' name='message'><button type='submit'>Send</button></form></body>');
  		res.write('</html>');
  		return res.end();
  	}

  	res.setHeader('Content-Type', 'text/html');
  	res.write('<html>');
  	res.write('<head><title>My First Page</title></head>');
  	res.write('<body><h1>hellow from  my Node.js Server!</h1></body>');
  	res.write('</html>');
  	res.end();
  });

  server.listen(3000);
  ```

- 요청 리디렉션 04:11

  ```jsx
  const http = require('http');
  const fs = require('fs');

  const server = http.createServer((req, res) => {
  	const url = req.url;
  	const method = req.method;

  	if(url === '/') {
  		res.setHeader('Content-Type', 'text/html');
  		res.write('<html>');
  		res.write('<head><title>Enter Message</title></head>');
  		res.write('<body><form action='/message' method='POST'><input type='text' name='message'><button type='submit'>Send</button></form></body>');
  		res.write('</html>');
  		return res.end();
  	}

  	if (url === '/message' && method === 'POST') {
  		fs.writeFileSync('message.txt', 'DUMMY');
  		// res.writeHead(302, {});
  		res.statusCode = 302;
  		res.etHeader('Location', '/');
  		retuen res.end();
  	}

  	res.setHeader('Content-Type', 'text/html');
  	res.write('<html>');
  	res.write('<head><title>My First Page</title></head>');
  	res.write('<body><h1>hellow from  my Node.js Server!</h1></body>');
  	res.write('</html>');
  	res.end();
  });

  server.listen(3000);
  ```

- 요청 분문 분석 11:12

  - Streams & Buffers
    ![image](https://github.com/user-attachments/assets/682f9420-e31e-417b-971a-85f9bd87920c)

    [stream] (idea: stert working on the Data early) - [request body part 1] - (your code: how do you work with flow data? → work with chunk of data! → buffer) - [request body part 2] - [request body part 3] - {[request body part 4] - [request body part 5] = buffer} → [fully parsed]

  ```jsx
  const http = require('http');
  const fs = require('fs');

  const server = http.createServer((req, res) => {
  	const url = req.url;
  	const method = req.method;

  	if(url === '/') {
  		res.setHeader('Content-Type', 'text/html');
  		res.write('<html>');
  		res.write('<head><title>Enter Message</title></head>');
  		res.write('<body><form action='/message' method='POST'><input type='text' name='message'><button type='submit'>Send</button></form></body>');
  		res.write('</html>');
  		return res.end();
  	}

  	if (url === '/message' && method === 'POST') {
  		const body = [];
  		req.on('data', (chunk) => {
  			console.log(chunk); // <Buffer 6d 65 73 73 ... >
  			body.push(chunk);
  		});
  		req.on('end', () => {
  			const parsedBody = Buffer.concat(body).toString();
  			console.log(parsedBody); // message=입력값
  			const message = parsedBody.splite('=')[1];
  			fs.writeFileSync('message.txt', message);
  		})
  		res.statusCode = 302;
  		res.etHeader('Location', '/');
  		retuen res.end();
  	}

  	res.setHeader('Content-Type', 'text/html');
  	res.write('<html>');
  	res.write('<head><title>My First Page</title></head>');
  	res.write('<body><h1>hellow from  my Node.js Server!</h1></body>');
  	res.write('</html>');
  	res.end();
  });

  server.listen(3000); // 터미널에서 `node app.js` 실행 후, localhost:3000으로 들어간 후 input에 입력값을 넣고 Send 버튼을 누르면 message.txt 파일이 생성되고 안에 입력값이 저장됨
  ```

- 이벤트 기반 코드 실행의 이해 06:00

  ```jsx
  const http = require('http');
  const fs = require('fs');

  const server = http.createServer((req, res) => {
  	const url = req.url;
  	const method = req.method;

  	if(url === '/') {
  		res.setHeader('Content-Type', 'text/html');
  		res.write('<html>');
  		res.write('<head><title>Enter Message</title></head>');
  		res.write('<body><form action='/message' method='POST'><input type='text' name='message'><button type='submit'>Send</button></form></body>');
  		res.write('</html>');
  		return res.end();
  	}

  	if (url === '/message' && method === 'POST') {
  		const body = [];
  		req.on('data', (chunk) => {
  			console.log(chunk);
  			body.push(chunk);
  		});

  		retuen req.on('end', () => {
  			const parsedBody = Buffer.concat(body).toString();
  			console.log(parsedBody);
  			const message = parsedBody.splite('=')[1];
  			fs.writeFileSync('message.txt', message);
  			res.statusCode = 302;
  			res.etHeader('Location', '/');
  			retuen res.end();
  		}) // 함수 안에 함수를 넣을 경우 나중에 실행됨 (비동기식) // 콜백 함수를 이벤트 리스너에 등록하고 다음 코드로 넘어간 다음에야 실행하게 되는데, 그럼 너무 늦기에 Error: cannot set headers after they are sent to the client 오류가 생김 // retuen 을 넣어줌으로써 기존에는 하단 코드만 실행되었지만, 위 코드를 실행하고 하단 코드는 실행하지 않게끔 함.
  	}

  	res.setHeader('Content-Type', 'text/html');
  	res.write('<html>');
  	res.write('<head><title>My First Page</title></head>');
  	res.write('<body><h1>hellow from  my Node.js Server!</h1></body>');
  	res.write('</html>');
  	res.end();
  });

  server.listen(3000);
  ```

- 블로킹 및 논블로킹 코드 05:04

  ```jsx
  const http = require('http');
  const fs = require('fs');

  const server = http.createServer((req, res) => {
  	const url = req.url;
  	const method = req.method;

  	if(url === '/') {
  		res.setHeader('Content-Type', 'text/html');
  		res.write('<html>');
  		res.write('<head><title>Enter Message</title></head>');
  		res.write('<body><form action='/message' method='POST'><input type='text' name='message'><button type='submit'>Send</button></form></body>');
  		res.write('</html>');
  		return res.end();
  	}

  	if (url === '/message' && method === 'POST') {
  		const body = [];
  		req.on('data', (chunk) => {
  			console.log(chunk);
  			body.push(chunk);
  		});

  		retuen req.on('end', () => {
  			const parsedBody = Buffer.concat(body).toString();
  			console.log(parsedBody);
  			const message = parsedBody.splite('=')[1];
  			fs.writeFile('message.txt', message, err => {
  				res.statusCode = 302;
  				res.etHeader('Location', '/');
  				retuen res.end();
  			}); // writeFile와는 다르게 writeFileSync는 Sync(동기화)가 있음으로 이 파일이 생성되기 전까지 코드 실행을 막음 // 파일 저장이 완료될 때까지 아래 코드의 실행을 멈출 것 // 그건 원하지 않기에 writeFile로 바꿈
  		})
  	}

  	res.setHeader('Content-Type', 'text/html');
  	res.write('<html>');
  	res.write('<head><title>My First Page</title></head>');
  	res.write('<body><h1>hellow from  my Node.js Server!</h1></body>');
  	res.write('</html>');
  	res.end();
  });

  server.listen(3000);
  ```

- Node.js 백그라운드 확인 12:01

  - Single Thread, Event Loop & Blocking Code
    ![image](https://github.com/user-attachments/assets/d22efb19-9054-4af9-9915-3b6e058e817a)

    node.js는 기본적으로 Single Thread인데 어떻게 여러개 작업을 처리할 수 있을까? 보안적 문제는? (요청 A와 요청 B의 데이터가 서로 접근할 수 있을지) → 각 기능의 범위를 다른 기능이 접근할 수 없음

    Event Loop는 node.js가 시작하면 자동으로 시작됨. Event Loop는 이벤트 콜백을 다룸.

    대신 파일 시스템 연산 등의 오래 걸리는 연산은 Worker Pool에 보내짐. 다른 javascript 코드에서 분리되어 다른 여러 스레드에서 작동할 수 있음. 작업을 마치면 Event Loop에서 node.js가 알맞은 콜백을 실행함

  - Event Loop
    ![image](https://github.com/user-attachments/assets/04a61c7e-82ee-40fc-adb4-c451d0edeba6)

    node.js를 계속 실행하도록 하는 루프 모든 콜백을 처리함

- Node 모듈 시스템 사용 10:05

  ```jsx
  // app.js
  const http = require('http');

  const routes = require('./routes');

  const server = http.createServer(routes);
  /* const server = http.createServer(routes.handler); */

  server.listen(3000);

  // routes.js
  const fs = require('fs');

  const requestHandler = (req, res) => {
  	const url = req.url;
  	const method = req.method;

  	if(url === '/') {
  		res.setHeader('Content-Type', 'text/html');
  		res.write('<html>');
  		res.write('<head><title>Enter Message</title></head>');
  		res.write('<body><form action='/message' method='POST'><input type='text' name='message'><button type='submit'>Send</button></form></body>');
  		res.write('</html>');
  		return res.end();
  	}

  	if (url === '/message' && method === 'POST') {
  		const body = [];
  		req.on('data', (chunk) => {
  			console.log(chunk);
  			body.push(chunk);
  		});

  		retuen req.on('end', () => {
  			const parsedBody = Buffer.concat(body).toString();
  			console.log(parsedBody);
  			const message = parsedBody.splite('=')[1];
  			fs.writeFile('message.txt', message, err => {
  				res.statusCode = 302;
  				res.etHeader('Location', '/');
  				retuen res.end();
  			});
  		})
  	}

  	res.setHeader('Content-Type', 'text/html');
  	res.write('<html>');
  	res.write('<head><title>My First Page</title></head>');
  	res.write('<body><h1>hellow from  my Node.js Server!</h1></body>');
  	res.write('</html>');
  	res.end();
  };

  // 1번째
  module.exports = requestHandler;

  // 2번째
  /* module.exports = {
  	handler: requestHandler,
  	someText: 'Some hard coded text',
  }; */

  // 3번째
  /* module.exports.handler = requestHandler;
  module.exports.someText = 'Some hard coded text'; */

  // 4번째
  /* exports.handler = requestHandler;
  exports.someText = 'Some hard coded text'; */

  // 코드를 깔끔하게 app.js와 routes.js 2개로 나눔
  ```

- 마무리 05:15

  - Module Summary
    ![image](https://github.com/user-attachments/assets/c4b87287-113d-4dfd-9916-5c440f2c73ad)

- 유용한 자료 및 링크 00:31
  첨부된 파일은 이번 섹션의 소스 코드입니다.
  아래의 유용한 자료를 참고하세요.
  - 공식 Node.js 자료: https://nodejs.org/en/docs/guides/
  - 모든 코어 모듈에 대한 Node.js 참고자료: https://nodejs.org/dist/latest/docs/api/
  - Node.js 이벤트 루프 추가자료: https://nodejs.org/en/docs/guides/event-loop-timers-and-nexttick/
  - 블로킹 및 논블로킹 코드:https://nodejs.org/en/docs/guides/dont-block-the-event-loop/

### 4. 개선된 개발 워크플로우 및 디버깅

### 5. Express.js 작업(95분) 👌🏻

- 모듈 소개 02:15
  - What’s this mouule?
    1. what is Express.js
    2. using Middleware
    3. working with Request & Response (elegantly!)
    4. Routing
    5. Returning HTML pages (files)
- Express.js란? 03:43
  - What and Why?
    - Server logic is complex!
    - you want to focus on bussiness logic, not on the nitty-gritty details!
    - use a frameworrk for the heavy lifting!
      - frameworrk: helper functions, tiils & rules that help you build your application!
  - alternatives to Express.js
    - vanila node.js, adonis.js, koa, …
- Express.js 설치 03:47
  `npm install —-save express`

  ```jsx
  // app.js

  const http = require("http");

  const express = require("express");

  const app = express();

  const server = http.createServer(app);

  server.listen(3000); // npm staer 하면 발생하는 로직을 아무 것도 정의해 주지 않았기 떄문에 요청을 처리하진 않음
  ```

- 미들웨어 추가 05:13

  - it’s all about middleware
    1. request →
    2. middleware → next()
    3. middleware → res.send()
    4. response →

  ```jsx
  // app.js

  const http = require("http");

  const express = require("express");

  const app = express();

  app.use((req, res, next) => {
    console.log("In the middleware!");
    next(); // 있어야 아래 다른 미들웨어로 이동함
  }); // next는 전달되는 함수 // 다음 미들웨어로 요청이 이동되어 실행

  app.use((req, res, next) => {
    console.log("In another middleware!");
  });

  const server = http.createServer(app);

  server.listen(3000);
  ```

- 미들웨어 작동 방식 02:58

  ```jsx
  // app.js

  const http = require("http");

  const express = require("express");

  const app = express();

  app.use((req, res, next) => {
    console.log("In the middleware!");
    next();
  });

  app.use((req, res, next) => {
    console.log("In another middleware!");
    res.send("<h1>Hellow form Express!</h1>"); // 기본 setHeader나 write 대신, 새로운 유틸리티 send를 사용하면 응답을 보내고, any 유형을 body를 첨부할 수 있음 // 자동으로 'Content-Type: text/html'이 설정이 됨
  });

  const server = http.createServer(app);

  server.listen(3000);
  ```

- Express.js 백그라운드 확인 03:42

  ```jsx
  // app.js

  /* const http = require('http'); */

  const express = require("express");

  const app = express();

  app.use((req, res, next) => {
    console.log("In the middleware!");
    next();
  });

  app.use((req, res, next) => {
    console.log("In another middleware!");
    res.send("<h1>Hellow form Express!</h1>");
  });

  /* const server = http.createServer(app);
  server.listen(3000); */
  app.listen(3000); // 더 간결하게
  ```

- 다른 라우트 사용법 04:59

  ```jsx
  // app.js

  const express = require("express");

  const app = express();

  app.use("/", (req, res, next) => {
    console.log("This always runs!");
    next();
  }); // 항상 실행되고 다음 미들웨어로 넘어감

  app.use("/add-product", (req, res, next) => {
    console.log("In another middleware!");
    res.send('<h1>The "Add product" Page</h1>');
  });

  app.use("/", (req, res, next) => {
    console.log("In another middleware!");
    res.send("<h1>Hellow form Express!</h1>");
  });

  app.listen(3000);
  ```

- 수신 요청 분석 08:00

  ```jsx
  // app.js

  const express = require("express");
  const bodyParser = require("body-parser");

  const app = express();

  app.use(bodyParser.urlencoded({ extended: false })); // 요청 본문 분석 `npm install--save body-parser`

  app.use("/add-product", (req, res, next) => {
    res.send(
      "<form action='/product' mothod='POST'><input type='text' name='title'><button type='submit'>Add product</button></form>"
    );
  });

  app.use("/product", (req, res, next) => {
    console.log(req.body); // { title: '입력값' }으로 보이게 됨
    res.redirect("/");
  }); // GET 요청에 대해서도 실행됨

  app.listen(3000);
  ```

- POST 요청으로 미들웨어 실행 제한 01:48

  ```jsx
  // app.js

  const express = require("express");
  const bodyParser = require("body-parser");

  const app = express();

  app.use(bodyParser.urlencoded({ extended: false }));

  app.use("/add-product", (req, res, next) => {
    res.send(
      "<form action='/product' mothod='POST'><input type='text' name='title'><button type='submit'>Add product</button></form>"
    );
  });

  // app.get // GET 요청만 실행됨
  // app.delete, app.patch, app.put 등
  app.post("/product", (req, res, next) => {
    console.log(req.body);
    res.redirect("/");
  }); // 위 input을 통해 실행된 POST 요청만 실행됨

  app.listen(3000);
  ```

- Express 라우터 사용 08:04

  ```jsx
  // app.js

  const express = require("express");

  const bodyParser = require("body-parser");

  const app = express();

  const adminRoutes = require("./routes/admin");
  const shopRoutes = require("./routes/shop");

  app.use(bodyParser.urlencoded({ extended: false }));

  // 순서 중요**
  app.use(adminRoutes());
  app.use(shopRoutes());

  app.listen(3000);

  // routes/admin.js

  const express = require("express");

  const router = express.Router();

  router.get("/add-product", (req, res, next) => {
    res.send(
      "<form action='/product' mothod='POST'><input type='text' name='title'><button type='submit'>Add product</button></form>"
    );
  });

  router.post("/product", (req, res, next) => {
    console.log(req.body);
    res.redirect("/");
  });

  module.export = router;

  // routes/shop.js

  const express = require("express");

  const router = express.Router();

  router.get("/", (req, res, next) => {
    res.send("<h1>Hellow from Express!</h1>");
  }); // get은 use와 다르게 정확히 '/' 일치하는 경로만 확인함

  module.export = router;
  ```

- 404 오류 페이지 추가 02:30

  ```jsx
  // app.js

  const express = require("express");

  const bodyParser = require("body-parser");

  const app = express();

  const adminRoutes = require("./routes/admin");
  const shopRoutes = require("./routes/shop");

  app.use(bodyParser.urlencoded({ extended: false }));

  app.use(adminRoutes());
  app.use(shopRoutes());

  // 위에서 요청이 처리되지 않았을 경우
  app.use((req, res, next) => {
    // res.setHeader()도 가능
    res.status(404).send("<h1>Page not found</h1>");
  });

  app.listen(3000);
  ```

- 경로 필터링 03:38

  ```jsx
  // app.js

  const express = require("express");

  const bodyParser = require("body-parser");

  const app = express();

  const adminRoutes = require("./routes/admin");
  const shopRoutes = require("./routes/shop");

  app.use(bodyParser.urlencoded({ extended: false }));

  // 이렇게 공통 경로를 설정할 수 있음
  app.use("/admin", adminRoutes());
  app.use(shopRoutes());

  app.use((req, res, next) => {
    res.status(404).send("<h1>Page not found</h1>");
  });

  app.listen(3000);

  // routes/admin.js

  const express = require("express");

  const router = express.Router();

  // /admin/add-product를 GET 의미함
  router.get("/add-product", (req, res, next) => {
    res.send(
      "<form action='/admin/add-product' mothod='POST'><input type='text' name='title'><button type='submit'>Add product</button></form>"
    );
  });

  // /admin/add-product를 POST 의미함
  router.post("/add-product", (req, res, next) => {
    console.log(req.body);
    res.redirect("/");
  });

  module.export = router;

  // routes/shop.js

  const express = require("express");

  const router = express.Router();

  router.get("/", (req, res, next) => {
    res.send("<h1>Hellow from Express!</h1>");
  });

  module.export = router;
  ```

- HTML 페이지 생성 05:09
- HTML 페이지 서비스하기 07:19

  ```jsx
  // app.js

  const express = require("express");

  const bodyParser = require("body-parser");

  const app = express();

  const adminRoutes = require("./routes/admin");
  const shopRoutes = require("./routes/shop");

  app.use(bodyParser.urlencoded({ extended: false }));

  app.use("/admin", adminRoutes());
  app.use(shopRoutes());

  app.use((req, res, next) => {
    res.status(404).send("<h1>Page not found</h1>");
  });

  app.listen(3000);

  // routes/admin.js

  const path = require("path");

  const express = require("express");

  const router = express.Router();

  router.get("/add-product", (req, res, next) => {
    res.sendFile(path.join(__dirname, "../", "views", "add-product.html"));
  });

  router.post("/add-product", (req, res, next) => {
    console.log(req.body);
    res.redirect("/");
  });

  module.export = router;

  // routes/shop.js

  const path = require("path");

  const express = require("express");

  const router = express.Router();

  router.get("/", (req, res, next) => {
    // res.sendFile('/views/shop.html');
    res.sendFile(path.join(__dirname, "../", "views", "shop.html")); // 실행 중인 운영체제를 감지하여 자동으로 올바른 경로를 생성 // __dirname란 현재 파일의 위치를 의미하므로 ../를 사용하여 위치를 조정해줌
  });

  module.export = router;
  ```

  ```html
  <!-- views/shop.html -->
  <html lang="en">
    <head>
      <meta charset="UTF-8" />
      <meta name="viewport" content="width=device-width, initial-scale=1.0" />
      <meta http-equiv="X-UA-Compatible" content="ie=edge" />
      <title>Add Product</title>
    </head>

    <body>
      <header>
        <nav>
          <ul>
            <li><a href="/">Shop</a></li>
            <li><a href="/admin/add-product">Add Product</a></li>
          </ul>
        </nav>
      </header>

      <main>
        <form action="/add-product" method="POST">
          <input type="text" name="title" />
          <button type="submit">Add Product</button>
        </form>
      </main>
    </body>
  </html>

  <!-- views/add-product.html -->
  <html lang="en">
    <head>
      <meta charset="UTF-8" />
      <meta name="viewport" content="width=device-width, initial-scale=1.0" />
      <meta http-equiv="X-UA-Compatible" content="ie=edge" />
      <title>Add Product</title>
    </head>

    <body>
      <header>
        <nav>
          <ul>
            <li><a href="/">Shop</a></li>
            <li><a href="/admin/add-product">Add Product</a></li>
          </ul>
        </nav>
      </header>

      <main>
        <h1>My Products</h1>
        <p>List of all the products...</p>
      </main>
    </body>
  </html>
  ```

- 404 페이지 반환 02:00

  ```jsx
  // app.js

  const path = require("path");

  const express = require("express");

  const bodyParser = require("body-parser");

  const app = express();

  const adminRoutes = require("./routes/admin");
  const shopRoutes = require("./routes/shop");

  app.use(bodyParser.urlencoded({ extended: false }));

  app.use("/admin", adminRoutes());
  app.use(shopRoutes());

  app.use((req, res, next) => {
    res.status(404).sendFile(path.join(__dirname, "views", "404.html"));
  }); // 이렇게 html으로 반환

  app.listen(3000);
  ```

  ```html
  <!-- views/404.html -->
  <html lang="en">
    <head>
      <meta charset="UTF-8" />
      <meta name="viewport" content="width=device-width, initial-scale=1.0" />
      <meta http-equiv="X-UA-Compatible" content="ie=edge" />
      <title>Page not found</title>
    </head>
    <body>
      <h1>Page not found!</h1>
    </body>
  </html>
  ```

- 힌트! 00:26
  다음 강의에서는 다음과 같은 코드를 작성합니다.
  `module.exports = path.dirname(process.mainModule.filename);`
  _(다음 강의를 진행하면서 왜 이 코드를 사용하는지 설명할게요!)_
  `deprecation warning`이 나타나는 것을 유의해야 합니다. 해당 오류가 나타나면, 다음과 같은 코드로 바꾸면 됩니다.
  `module.exports = path.dirname(require.main.filename);`
  아주 간단하죠 :)
- 내비게이션을 위한 헬퍼 함수 사용 03:37

  ```jsx
  // util/path.js

  const path = require("path");

  module.export = path.dirname(process.mainMoudule);

  // routes/admin.js

  const path = require("path");

  const express = require("express");

  const rootDir = require("../util/path.js");

  const router = express.Router();

  router.get("/add-product", (req, res, next) => {
    // res.sendFile(path.join(__dirname, '..', 'views', 'add-product.html')); // ../ 대신 ..을 사용해도 가능! 경로를 설정할 때 구분자가 무엇인지 가정하지 않음
    res.sendFile(path.join(rootDir, "views", "add-product.html"));
  });

  router.post("/add-product", (req, res, next) => {
    console.log(req.body);
    res.redirect("/");
  });

  module.export = router;

  // routes/shop.js

  const path = require("path");

  const express = require("express");

  const rootDir = require("../util/path.js");

  const router = express.Router();

  router.get("/", (req, res, next) => {
    res.sendFile(path.join(rootDir, "views", "shop.html")); // 이렇게 수정
  });

  module.export = router;
  ```

- 페이지 스타일링 13:58
- 정적으로 파일 서비스하기 07:49

  ```jsx
  // app.js

  const express = require("express");

  const bodyParser = require("body-parser");

  const app = express();

  const adminRoutes = require("./routes/admin");
  const shopRoutes = require("./routes/shop");

  app.use(bodyParser.urlencoded({ extended: false }));
  app.use(express.static(__dirname, "public")); // 정적으로 서비스하기 원하는 폴더 경로를 압력 (읽기 전용) // 여러개 폴더를 등록할 수 있으며 요청은 원하는 파일을 찾을 때까지 모든 폴더를 통과하게 됨

  app.use("/admin", adminRoutes());
  app.use(shopRoutes());

  app.use((req, res, next) => {
    res.status(404).send("<h1>Page not found</h1>");
  });

  app.listen(3000);
  ```

  ```html
  <!DOCTYPE html>
  <html lang="en">
    <head>
      <meta charset="UTF-8" />
      <meta name="viewport" content="width=device-width, initial-scale=1.0" />
      <meta http-equiv="X-UA-Compatible" content="ie=edge" />
      <title>Add Product</title>
      <!-- 이렇게 css를 import해서 사용할 수 있음 -->
      <link rel="stylesheet" href="/css/main.css" />
    </head>

    <body>
      <header class="main-header">
        <nav class="main-header__nav">
          <ul class="main-header__item-list">
            <li class="main-header__item">
              <a class="active" href="/">Shop</a>
            </li>
            <li class="main-header__item">
              <a href="/admin/add-product">Add Product</a>
            </li>
          </ul>
        </nav>
      </header>

      <main>
        <h1>My Products</h1>
        <p>List of all the products...</p>
      </main>
    </body>
  </html>
  ```

- 마무리 03:36
- 유용한 자료 및 링크 00:16
  첨부된 파일은 이번 섹션의 소스 코드입니다.
  소스 코드를 사용할 때, 추출된 폴더에 `npm install`을 실행하는 것을 잊지 마세요!
  아래의 유용한 자료를 참고하세요.
  - Express.js 공식 참고자료: https://expressjs.com/en/starter/installing.html

### 6. 동적 콘텐츠 작업 및 템플릿 엔진 추가

### 7. 모델 뷰 컨트롤러 (MVC)

### 8. 선택 사항: 앱 향상

### 9. 동적 라우트 및 고급 모델

### 10. SQL 소개(53분) 👌🏻

- 모듈 소개 01:33
- 데이터베이스 선택하기 04:17
  - What’s SQL?
    ![image](https://github.com/user-attachments/assets/cb4f8f8f-fd7e-4fef-8d81-d327f8c452b0)
    - 강력한 데이터 스키마를 지니고 있어 각각의 표마다 내부 데이터의 형태, 보유한 영역과 각각에 저장되는 데이터의 종류를 분명하게 정의함
    - 또한 데이터 간 상관관계가 존재. 일대일, 일대다 또는 다대다라는 세 가지 중요한 상관관계로 다양한 테이블들의 관계를 결정하게 됨 (즉 테이블들이 연결되어 있다)
- NoSQL 소개 04:20
  - NoSQL
    ![image](https://github.com/user-attachments/assets/90c3c4b6-065e-47b4-9492-deaba6d094f7)
    - 간단히 말해 SQL의 방식을 따르지 않는다. 다양한 쿼리 언어를 사용하지만 스키마와 상관관계 대신 NoSQL은 다른 신경 쓰는 부분이나 다른 장점들이 있음
    - 테이블과 같은 개념이지만 NoSQL에서는 집합(collections)이라고 부름. JavaScript 객체와 약간 닮아있다. NoSQL에는 엄격한 스키마(데이터 상관관계)가 없음. 같은 집단에 각각 다른 구조를 지닌 다수의 문서들을 저장할 수 있음. 물론 여전히 비슷한 구조로 통일해 두려고 하겠지만 어떤 애플리케이션에서는 데이터베이스에 저장하는 데이터에 항상 동일한 영역을 가질 수 없는 경우도 종종 일어나는데 NoSQL에서는 괜찮음.
  - What’s SQL?
    ![image](https://github.com/user-attachments/assets/151883c0-c137-4e36-9977-62696c673b35)
    - 또 다른 점은 NoSQL 세계에는 실제 상관관계가 존재하지 않음. 대신 데이터를 복제하게 됨.
      즉 집합이 있다면 중첩된 문서에 더 자세하게 분리된 문서로 저장될 수 있음.
      단순히 데이터를 복제하는데 정확히 말하자면 특정 집합에 필요한 데이터를 복제하는 것
      물론 데이터가 변경된다면 여러 장소에서 이를 업데이트 해야 함을 뜻함.
    - 하지만 데이터를 받았을 때 다수의 테이블을 하나로 합칠 필요가 없다는 큰 이점을 제공해 매우 길고 어려운 코드가 되어 성능에까지 영향을 미치는 일이 없음. 데이터를 집합에서 읽어오기만 하면 되고 다른 집합으로 이동하는 일 없이 페이지에 표시하면 됨. 따라서 매우 빠른 속도로 진행할 수 있음.
- SQL과 NoSQL 비교하기 05:06
  - 데이터베이스를 확장할 때 사용하는 두 가지 방법
    - 수평 스케일링
      - 서버를 더 추가하는 것. 장점은 이를 무한으로 진행할 수 있다는 것
        클라우드 제공업체든 자체 데이터 서버든 언제든지 새로 서버를 구매해서, 데이터베이스에 연결한 뒤 서버들에 데이터를 분산시키면 됨.
      - 동시에 쿼리를 모든 서버에 실행하고 지능적으로 통합하는 절차도 일부 필요함. 따라서 쉽다고만 할 수는 없지만 스케일링하기에 좋은 방법
    - 수직 스케일링
      - 존재하는 서버에 CPU나 메모리 등을 추가하여 더 강력하게 만드는 것. 클라우드 제공업체의 경우 이 방식이 일반적으로 용이하여, 그냥 다른 옵션을 고르고 돈을 더 내면 끝
      - 문제는 한계가 존재함. 단일 머신에 무한정 CPU 출력을 집어넣을 수는 없음.
  - SQL vs NoSQL
    - SQL
      - 스케일링에 있어서는 SQL이 작동하는 방식(데이터가 수많은 테이블에 분산된 뒤 상관관계를 통해 연결)으로 인해 수평 스케일링이 매우 어렵거나 심지어 불가능한 경우도 있음.
      - 수직 스케일링은 쉽게 할 수 있음 서버를 더 강력하게 만들면 되지만, 서버를 추가하는 수평 스케일링은 매우 어렵거나 심지어 불가능할 수도 있음. 매초 다수 혹은 수천 건의 쿼리를 읽고 쓰면 문제 될 수 있는 부분임
    - NoSQL
      - 연결의 수가 적은 작동 방식으로 인해 수평 스케일링이 더 쉬움. 따라서 방대한 읽기 및 쓰기 요청에 대해 탁월한 성능을 얻게 되고 NoSQL은 처리량이 많은 애플리케이션에서 매우 고성능을 발휘함.
- MySQL 설정 07:16
  ![image](https://github.com/user-attachments/assets/6b30e5bb-1e79-4423-a636-9f480b627415)
  - MySQL 설치와 서버 실행
  - MySQL workbench를 통해 스키마 생성
- 앱을 SQL 데이터베이스에 연결하기 06:50

  - 노드 내부에서 SQL을 사용하거나 상호작용 하기 위해 `npm install --save mysql2` 설치
    → 이를 통해 노드 내부에서 SQL 코드를 작성 및 실행하며 데이터베이스와 상호작용 할 수 있도록 함
  - node 애플리케이션 내부에서 데이터베이스에 연결
    → 여기에 코드를 설정해서 SQL 데이터베이스로 연결하고, 쿼리를 실행하게 하는 연결 객체를 전달받을 수 있도록 함

    - SQL 데이터베이스와 연결하는 방법
      1. 단일 연결: 연결 하나를 설정한 다음 쿼리를 실행. 쿼리를 완료한 다음에는 항상 연결을 닫아야 함. 하지만 새로운 쿼리마다 연결을 생성하기 위해 코드를 재실행 해야 해서 비효율적.
      2. 커넥션 풀: 연결 설정 등에 대한 선택지가 있음. 다중 연결을 관리하는 이 풀에서 새로운 연결을 받아오게 되면 각 쿼리마다 개별적으로 연결하므로 다수의 쿼리를 동시에 실행할 수 있음.
         쿼리가 완료된 다음에는 연결을 다시 풀로 돌려주게 되고 새 쿼리를 위해 사용될 수 있음. 풀은 애플리케이션을 종료할 때 완료됨.

    ```jsx
    // util/database.js

    const mysql = require("mysql2");

    const pool = mtsql.createPool({
      host: "localhost",
      user: "root",
      database: "node-complete",
      password: "", // 설치 중 생성했던 암호
    });

    module.exports = pool.promise(); // promise를 사용함으로써 콜백 대신 비동기적 데이터를 다룰 수 있게 됨.

    // app.js

    const db = require("./util/database");

    db.execute("SELECT * FROM products"); // 쿼리를 실행할 수 있음 (query도 있지만 execute가 좀 더 안전)
    ```

- 기본 SQL 및 테이블 생성 04:07
  ![image](https://github.com/user-attachments/assets/9fcc4075-64bf-42c1-b460-c42a4be45d3e)
  ![image](https://github.com/user-attachments/assets/7a50ffad-b24b-490c-9a30-9437d568ab42)

- 데이터 검색 03:00

  ```jsx
  // app.js

  const db = require("./util/database");

  db.execute("SELECT * FROM products")
    .then((res) => {
      console.log(res[0], res[1]);
    })
    .catch((err) => {
      console.log(err);
    });
  ```

- 제품 가져오기 06:30

  - 데이터를 가져올 때 static 메서드를 사용할 수 있지만, 파일이 아니라 데이터베이스에서 데이터를 가져오도록 수정

    ```jsx
    // models/products.js

    const db = require("../util/database");

    const Cart = require("./cart");

    module.exports = class Product {
      constructor(id, title, imageUrl, description, price) {
        this.id = id;
        this.title = title;
        this.imageUrl = imageUrl;
        this.description = description;
        this.price = price;
      }

      save() {}

      static deleteById(id) {}

      static fetchAll() {
        // execute가 전체 promise를 반환하여 다른 곳에서 사용할 수 있도록 함
        return db.execute("SELECT * FROM products");
      }

      static findById(id) {}
    };
    ```

    ```jsx
    // controllers/shop.js

    const Product = require("../models/product");
    const Cart = require("../models/cart");

    // 기존
    /* exports.getIndex = (req, res, next) => {
      Product.fetchAll((products => {
        res.render('shop/index', {
          prods: products,
          pageTitle: 'Shop',
          path: '/' 
        });
      });
    } */

    exports.getIndex = (req, res, next) => {
      Product.fetchAll()
        // 구조 분해 기능
        .then(([rows, fieldData]) => {
          res.render("shop/index", {
            prods: rows,
            pageTitle: "Shop",
            path: "/",
          });
        })
        .catch((err) => console.log(err));
    };
    ```

- 제품 가져오기 - 실습 시간 01:04

  ```jsx
  // controllers/shop.js

  const Product = require("../models/product");
  const Cart = require("../models/cart");

  // 기존
  /* exports.getProducts = (req, res, next) => {
    Product.fetchAll((products => {
      res.render('shop/product-list', {
        prods: products,
        pageTitle: 'All Products',
        path: '/products' 
      });
    });
  } */

  exports.getProducts = (req, res, next) => {
    Product.fetchAll()
      .then(([rows, fieldData]) => {
        res.render("shop/product-list", {
          prods: rows,
          pageTitle: "All Products",
          path: "/products",
        });
      })
      .catch((err) => console.log(err));
  };
  ```

- 데이터베이스에 데이터 삽입 04:12

  ```jsx
  // models/products.js

  const db = require("../util/database");

  const Cart = require("./cart");

  module.exports = class Product {
    constructor(id, title, imageUrl, description, price) {
      this.id = id;
      this.title = title;
      this.imageUrl = imageUrl;
      this.description = description;
      this.price = price;
    }

    save() {
      return db.execute(
        "INSERT INTO products (title, price, imageUrl, description) VALUES (?, ?, ?, ?)", // 사용자가 웹 페이지 입력 필드에 특이 데이터를 삽입해 SQL 쿼리로 실행될 때 발생하는 공격 패턴인 SQL 인젝션을 방지하기 위해 물음표만 사용
        [this.title, this.price, this.imageUrl, this.description] // MySQL 패키지가 입력값을 안전하게 escape해서 숨겨진 SQL 명령을 위해 파싱한 후 제거함. 즉 보안을 추가로 확보하는 것
      );
    }

    static deleteById(id) {}

    static fetchAll() {
      return db.execute("SELECT * FROM products");
    }

    static findById(id) {}
  };
  ```

  ```jsx
  // controllers/admin.js

  const Product = require("../models/product");

  exports.getAddProduct = (req, res, next) => {
    res.render("admin/edit-product", {
      pageTitle: "Add Product",
      path: "/admin/add-product",
      editing: false,
    });
  };

  exports.postAddProduct = (req, res, next) => {
    const title = req.body.title;
    const imageUrl = req.body.imageUrl;
    const price = req.body.price;
    const description = req.body.description;
    const product = new Product(null, title, imageUrl, description, price);
    // 기존
    /* product.save();
  	   res.redirect('/'); */
    product
      .save()
      .then(() => {
        res.redirect("/");
      })
      .catch((err) => console.log(err));
  };
  ```

- "where" 조건으로 단일 제품 가져오기 02:57

  - Details 버튼을 클릭할 수 있도록 만들어 데이터베이스 내에 하나의 문서나 항목에서 데이터를 검색하는 법

    ```jsx
    // models/products.js

    const db = require("../util/database");

    const Cart = require("./cart");

    module.exports = class Product {
      constructor(id, title, imageUrl, description, price) {
        this.id = id;
        this.title = title;
        this.imageUrl = imageUrl;
        this.description = description;
        this.price = price;
      }

      save() {
        return db.execute(
          "INSERT INTO products (title, price, imageUrl, description) VALUES (?, ?, ?, ?)",
          [this.title, this.price, this.imageUrl, this.description]
        );
      }

      static deleteById(id) {}

      static fetchAll() {
        return db.execute("SELECT * FROM products");
      }

      static findById(id) {
        // 하나의 제품에 대한 모든 열. 즉 모든 데이터를 가져옴
        return db.execute("SELECT * FROM products WHERE products.id = ?", [id]); // id = ?를 입력하면 MySQL에 값을 다시 주입하라고 알려주는 것 (여기서 인수는 id)
      }
    };
    ```

    ```jsx
    // controllers/shop.js

    const Product = require("../models/product");
    const Cart = require("../models/cart");

    // 기존
    /* exports.getProducts = (req, res, next) => {
      const prodId = req.params.productId;
      Product.findById((prodId, products => {
        res.render('shop/product-detail', {
          product: product,
          pageTitle: product.title,
          path: '/products' 
        });
      });
    } */

    exports.getProduct = (req, res, next) => {
      const prodId = req.params.productId;
      Product.findById(prodId)
        .then(([product]) => {
          res.render("shop/product-detail", {
            product: product[0], // 하나의 요소만 있긴 하지만 여전히 배열인데 뷰에 한 객체만 가진 배열이 아닌 한 객체를 넣어야 함
            pageTitle: product.title,
            path: "/products",
          });
        })
        .catch((err) => console.log(err));
    };
    ```

- 마무리 01:24
  - 필요한 기능을 모두 추가하려면 장바구니에 제품을 담거나 주문 관련해서 사용자와 상호 작용하는 등의 기능은 모두 여기서 작성하고 있는 SQL 쿼리를 통해 추가할 수 있음
    하지만 애플리케이션 논리가 복잡해질수록 쿼리 역시 점점 복잡해질 것. 또한 현재는 연결할 테이블이 하나라서 데이터베이스 관계가 없지만 추후에 많아지면 복잡해질 수 밖에 없음.
  - 보통의 경우 쿼리를 전부 작성하지 않아도 되는 (SQL 코드를 아예 작성하지 않고도) 연결, 삭제, 추가 등 필요한 기능을 제공하는 내장 JavaScript 객체만을 이용함. Node.js에 추가할 수 있는 외부 패키지를 이용하면 훨씬 쉬움. (Sequelize 이용)
- 유용한 자료 및 링크 00:22
  아래 첨부 파일에서 이번 섹션의 소스 코드를 찾을 수 있습니다.
  아래의 소스 코드를 사용할 땐 추출 폴더에서 `npm install`을 실행해야 하는 것을 잊지 마세요!
  유용한 자료.
  - MySQL/SQL에 대해 전반적으로 자세히 알아보기:https://www.w3schools.com/sql/
  - Node MySQL 패키지에 대해 자세히 알아보기: https://github.com/sidorares/node-mysql2

### 11. Sequelize의 이해(112분) 🤚🏻

- 모듈 소개 01:26
- Sequelize란? 02:35
- 데이터베이스에 연결 03:57
- 모델 정의 05:47
- 데이터베이스에 JS 정의 동기화하기 04:29
- 데이터 삽입 및 제품 생성 04:49
- 필독: Sequelize 5의 findById() 00:12
- 데이터 검색 및 제품 찾기 03:01
- where 조건으로 단일 제품 얻기 04:30
- 관리자 상품 가져오기 01:25
- 상품 업데이트하기 05:18
- 상품 삭제하기 02:48
- 사용자 모델 생성하기 02:48
- 일대다 관계 추가하기 05:54
- 더미 사용자 생성 및 관리하기 06:01
- 관계 설정 메서드 사용하기 03:42
- 관련 상품 가져오기 02:46
- 일대다 및 다대다 관계 06:03
- 카트 생성 및 가져오기 05:45
- 장바구니에 새 상품 추가하기 06:42
- 관련 상품 추가 및 장바구니 항목 검색하기 04:55
- 관련 상품 삭제 및 장바구니 상품 삭제하기 02:24
- 주문 모델 추가하기 04:19
- 장바구니 상품을 주문 상품으로 저장하기 08:19
- 장바구니 재설정 및 주문 가져오기와 출력하기 09:53
- 마무리 01:49
- 유용한 자료 및 링크 00:14

### 12. NoSQL 작업 및 MongoDB 사용(139분) 🤚🏻

- 모듈 소개 01:17
- MongoDB란? 03:57
- NoSQL에서의 관계 03:58
- MongoDB 설정하기 04:48
- MongoDB 드라이버 설치하기 07:01
- 데이터베이스 연결 생성하기 03:25
- 데이터베이스 연결 완료하기 04:21
- 데이터베이스 연결 사용하기 05:14
- 제품 만들기 02:08
- MongoDB Compass의 이해 02:38
- 모든 제품 가져오기 04:34
- 단일 제품 가져오기 07:45
- "편집" 및 "삭제" 버튼 다시 작동하시키기 02:21
- 제품 편집을 위한 제품 모델 작업하기 07:14
- "제품 업데이트" 코드 완성하기 03:57
- 제품 업데이트 참고 사항 01:47
- 제품 삭제하기 03:30
- "제품 추가" 기능 수정하기 01:28
- 새로운 사용자 생성하기 07:00
- 데이터베이스에 사용자 저장하기 05:40
- 장바구니 항목 및 주문 작업하기 07:13
- "장바구니에 담기" 기능 추가하기 06:14
- 장바구니에 여러 제품 저장하기 07:01
- 장바구니 항목 표시하기 09:20
- 버그 수정하기 01:02
- 장바구니 항목 삭제하기 04:02
- 주문 추가하기 04:36
- 관계형 주문 데이터 추가하기 06:21
- 주문 받기 03:20
- 장바구니에서 삭제된 항목 제거하기 02:58
- 마무리 02:19
- 유용한 자료 및 링크 00:32
- 두 가지 수정(백그라운드) 00:09

### 13. Mongoose 작업(77분) 🤚🏻

- 모듈 소개 01:23
- Mongoose란? 02:04
- Mongoose로 MongoDB 서버에 연결하기 04:47
- 제품 스키마 생성하기 06:01
- Mongoose를 통한 데이터 저장하기 06:10
- 모든 제품 가져오기 02:27
- 단일 제품 가져오기 01:24
- 제품 업데이트하기 04:14
- 상품 삭제하기 01:19
- 사용자 모델 추가 및 사용하기 06:36
- Mongoose에서 관계 사용하기 03:44
- 관계 가져오기에 대한 한 가지 중요한 사항 03:54
- 장바구니 작업하기 05:25
- 장바구니 로드하기 05:12
- 장바구니 항목 삭제하기 02:45
- 주문 생성 및 받기 09:56
- 모든 주문 관련 데이터 저장하기 01:52
- 주문 저장 후 장바구니 비우기 01:59
- 주문 가져오기 및 표시하기 03:40
- 마무리 01:37
- 유용한 자료 및 링크 00:13

### 14. 세션 및 쿠키

### 15. 인증 추가

### 16. 이메일 전송

### 17. 고급 인증

### 18. 검증 이해

### 19. 오류 처리

### 20. 파일 업로드 및 다운로드

### 21. 페이지화(Pagination) 추가

### 22. 비동기 요청 이해

### 23. 결제 기능 추가

### 24. REST API 작업 - 기본 개념(63분) 👌🏻

- 모듈 소개 01:25
  - What’s in this module?
    - what are ‘REST APIs’?
    - why use/ build REST APIs?
    - core REST concept & principles
    - first REST API!
- REST API 정의 및 사용 이유? 07:01
  - REST API의 REST는 Representational State Transfer의 약자로 사용자 인터페이스 대신 데이터 전송을 의미
  - HTML 대신 데이터만 전송하고 클라이언트 및 프론트엔드가 모바일 앱이던 단일 페이지 애플리케이션이든 전송받은 데이터로 작업하도록 하는 것
  - What & Why?
    ![image](https://github.com/user-attachments/assets/0dd3d006-425d-4c08-b45a-bcccf3a20175)
- REST API로 데이터 액세스하기 05:41

  - REST API big picture
    ![image](https://github.com/user-attachments/assets/201a81bd-f157-4ccc-9260-edef3e467e10)
  - Data format
    ![image](https://github.com/user-attachments/assets/5d134d8f-a16d-4c73-a4ba-6194cebd5492)

- 라우팅과 HTTP 메소드 이해하기 05:25
  - Routing
    - 서버 측 라우팅에 경로를 정의하고 들어오는 요청을 기다리며 경로가 처리할 HTTP 메서드를 정의해서 모든 경로에 아무 요청이나 도달하지 않도록 함
    - API 엔드 포인트? POST나 GET 같은 HTTP 메서드와 각 경로를 말하는 것
  - http method (http verbs)
    - GET 메서드는 서버로부터 리소스를 얻고
    - POST 메서드 서버로 리소스를 보내서 서버에 생성하거나 기존 리소스 배열에 첨부
    - PUT 메서드는 리소스를 서버에 놓고 싶을 때
      즉 리소스를 생성하거나 기존 리소스를 덮어쓴다는 뜻
    - PATCH 메서드는 전체적으로 덮어쓰는 게 아니라 기존 리소스의 일부분만 업데이트
    - DELETE 메서드는 서버에 있는 리소스를 삭제
    - OPTIONS 메서드는 브라우저가 자동으로 요청을 보내 다음 요청을 알아보는 것
- REST API - 핵심 원칙 04:09
  - REST principals
    ![image](https://github.com/user-attachments/assets/94a9b30b-731d-4751-abfd-d7445985813f)
- REST API 프로젝트 생성 및 라우트 설정 구현 06:41
  `npm install --save express`
  `npm install —save-dev nodemon` // 변경이 있을 때마다 서버를 수동으로 재시작하고 싶지 않기 때문
  `npm install —save-dev bodr-parser` // 들어오는 요청 본문을 분석할 수 있습니다

  ```jsx
  /* package.json */

  {
  	"scripts": {
  		// 추가해줌
  		"start": "nodemon apps.js",
  	},
  }

  /* app.js */

  const express = require('express');

  const feedRoutes = require('./routes/feed');

  const app = express();

  app.use('/feed', feedRoutes); // 이렇게 라우트를 등록해줌

  app.listen(8080);

  /* routes/feed.js */

  const express = require('express');

  const feedController = require('../controllers/feed');

  const router = express.Router();

  // GET /feed/posts
  router.get('/posts', feedController.getPosts); // 이렇게 controller 함수를 할당

  module.export = router;

  /* controllers/feed.js */

  exports.getPosts = (req, res, next) => {};
  ```

- 요청 및 응답 보내기 및 Postman 작업 13:28

  ```jsx
  /* app.js */

  const express = require('express');
  const bodyParser = require('body-parser');

  const feedRoutes = require('./routes/feed');

  const app = express();

  // app.use(bodyParser.urlencoded()); // x-www-form-urlencoded 형식의 데이터를 담고 있는 데이터 포맷 또는 요청에 대해서는 좋은 방법 <form>
  app.use(bodyParser.json()); // application/json

  app.use('/feed', feedRoutes);

  app.listen(8080);

  /* routes/feed.js */

  const express = require('express');

  const feedController = require('../controllers/feed');

  const router = express.Router();

  // GET /feed/posts
  router.get('/posts', feedController.getPosts);

  // POST /feed/posts
  router.post('/posts', feedController.createPost);

  module.export = router;

  /* controllers/feed.js */

  exports.getPosts = (req, res, next) => {
  	// res.render(); // 뷰를 랜더링하지 않기에
  	res.status(200).json({
  		posts: [{title: 'first post', content: 'this is content!'}]
  	});
  };

  // 클라이언트에서 쉽게 처리할 수 있도록 응답을 보낼 때 상태 코드를 명확히 표시해야 함 // 클라이언트가 응답을 기반으로 사용자 인터페이스를 렌더링하므로

  // npm start 후 localhost:8080/feed/posts로 들어가면 위 json이 보이고 응답 헤더가 서버에 의해 Content-Type: applicaion/json; 설정됨

  exports.createPost = (req, res, next) => {
  	const { title, content } = req.body;
  	// db에 저장해야 함
  	// 리소스 생성 성공을 알리려면 201을 사용하는 게 나음 200은 그냥 성공을 나타냄
  	res.status(201).json({
  		message: 'Post created successfully'',
  		post: {
  			id: new Date().toISOString(),
  			title,
  			content,
  		}
  	});
  };
  ```

  ![image](https://github.com/user-attachments/assets/9d49b168-9a27-48d6-a7db-090063f01382)

- REST API, 클라이언트 및 CORS 오류 10:33
  ![image](https://github.com/user-attachments/assets/28ae0b8f-0205-4388-be4d-a0d69e4339c6) - 따라서 CORS 오류를 해결해야 하며, 이 경우 CodePen에서 실행되는 이 브라우저에 우리 서버에서 전송하는 응답을 받아도 된다고 알려주어야 합니다.
  그리고 브라우저에 이를 알리려면 서버에서 무언가를 변경해야 하는데 여기서 많은 실수를 하곤 합니다. 많은 사람이 이 오류를 보고 브라우저 측 JavaScript 코드에서 해결하려고 하지만 이는 불가능한 일이며 서버에서만 해결할 수 있습니다.
  → 서버 측 코드로 돌아가서 특수 헤더를 몇 가지 설정하면 됩니다.

  ```jsx
  /* app.js */

  const express = require('express');
  const bodyParser = require('body-parser');

  const feedRoutes = require('./routes/feed');

  const app = express();

  app.use(bodyParser.json()); // application/json

  app.use(() => {
  	// res.setHeader('Access-Control-Allow-Origin', 'codepen.io');
  	res.setHeader('Access-Control-Allow-Origin', '*'); // any clients
  	res.setHeader('Access-Control-Allow-Methods', 'GET, POST, PUT, PATCH, DELETE'); // 특정 http 메서드 사용을 허용
  	res.setHeader('Access-Control-Allow-Headers', 'Content-Type, Authorization'); // 헤더에 추가하는 것이 인증 데이터를 포함한 요청을 보낼 수 있으며, 요청의 콘텐츠 유형을 정의함
  	next(); // 요청이 계속해서 라우트에서 처리되도록 해줌
  }; // 보내는 모든 응답에 이와 같은 헤더가 포함됨

  app.use('/feed', feedRoutes);

  app.listen(8080);
  ```

- POST 요청 보내기 06:32
  ![image](https://github.com/user-attachments/assets/4116d0ad-17be-4720-ba36-7279c2540a6c)
  ![image](https://github.com/user-attachments/assets/0c04daff-c63d-4521-aa7c-5f422a8f755f)
  ![image](https://github.com/user-attachments/assets/72fa9b84-7eb6-45b4-8927-7a8f9f7bdd78)
  ![image](https://github.com/user-attachments/assets/cb67fdce-8113-47a6-9dbb-8eedd43566c0) - OPTIONS는 다음에 실행할 요청, 즉 POST 요청이 허용될 경우 성공할지를 판단하기 위해 브라우저가 사용하는 장치

- 마무리 02:14
  - Module Summary
- 유용한 자료 및 링크 00:18
  아래 첨부 파일에서 이번 섹션의 소스 코드를 찾을 수 있습니다.
  아래의 소스 코드를 사용할 땐 추출 폴더에서 `npm install`을 실행해야 하는 것을 잊지 마세요!
  유용한 자료.
  - 예시, RESTful API 만들기 참고자료: https://academind.com/learn/node-js/building-a-restful-api-with/

### 25. REST API 작업 - 실용적인 애플리케이션 생성 ✋🏻

- 모듈 소개 01:10
- REST API와 나머지 과정 03:59
- 프론트엔드 설정 이해하기 04:18
- API 계획하기 03:02
- 게시물 목록 가져오기 06:19
- Post 엔드 포인트 생성 추가하기 07:36
- 서버 측 검증 추가하기 06:19
- Post 모델 설정하기 05:14
- 데이터베이스에 게시물 저장하기 03:32
- 정적 이미지 및 오류 처리 06:53
- 단일 게시물 가져오기 07:48
- 이미지 이름 및 Windows 01:36
- 이미지 업로드 08:56
- 게시물 업데이트 14:02
- 게시물 삭제 04:17
- 페이지화 추가하기 06:20
- 사용자 모델 추가하기 04:08
- 사용자 가입 검증 추가 06:29
- 사용자 로그인 07:24
- 인증 작동 방법 03:10
- 사용자 로그인하기 03:51
- 로그인 및 JSON 웹 토큰(JWT) 생성 07:53
- 토큰 사용 및 검증 09:43
- 모든 라우트에 인증 미들웨어 추가하기 01:52
- 게시물과 사용자 연결 06:13
- 권한 확인 추가하기 03:50
- 사용자 관계 지우기 02:54
- 마무리 02:28
- 유용한 자료 및 링크 00:08

### 26. Node.js내 Async/Await 이해

### 27. 웹 소켓 및 Socket.io 이해

### 28. GraphQL 작업

### 29. 앱 배포

### 30. Node.js 애플리케이션 테스트

### 31. npm을 활용한 빌드 도구로서의 Node.js

### 32. 최신 JavaScript 및 NodeJS

### 33. NodeJS 및 TypeScript

### 34. Deno 소개

### 35. Deno, CRUD 및 데이터베이스 (MongoDB)

### 36. 전체 요약
