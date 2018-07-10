使用 script 标签，在 html 中会按照顺序来加载并执行脚本，在加载和执行的过程中，会阻塞后续的 DOM 渲染。

为了解决以上问题，使用 `async` 和 `defer`，这两个属性使得 script 都不会阻塞 DOM 的渲染。

> defer 

使用 `<script defer>`，浏览器会异步的下载该文件并且不会影响到后续的 DOM 渲染。如果有多个设置了 `defer` 的 `script` 标签存在，则会按照顺序执行所有的 script。

> async

会使得 script 脚本异步的加载并在允许的情况下执行。`async` 的执行，并不会按照 script 在页面中的顺序来执行，而是谁先加载完谁执行。