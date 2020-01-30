# Bookmarklet

Bookmarklet 是一段可在网页中执行的代码，并且可以像书签一样添加到浏览器的标签栏中，故名**小书签**。

## 列表

|        标签名        | 功能 | 使用方式 |
| :------: | :------: | -------- |
| Revise MP Editor SVG | 修正微信公众号图文编辑器粘贴 SVG 时部分转换为 Embed 导致不支持 Dark Mode 的问题 | 粘贴图文之后点击小标签即可 |

使用方法：`双击` 以下链接并 `拖动` 到浏览器标签栏即可保存。

<center>
  <div>
    <a href="javascript: function loadSVG(src) {  return new Promise((resolve) => {    let ajax = new XMLHttpRequest();    ajax.open('GET', src, true);    ajax.send();    ajax.onload = function (e) {      let div = document.createElement('div');      div.innerHTML = ajax.responseText;      let svg = div.childNodes[1];      resolve(svg);    }  })}function revise() {  console.log(`【MP_SVG_REVISE】 Start`);  let ueditor = document.getElementById('ueditor_0');  let view = ueditor.contentDocument.getElementsByClassName('view')[0];  let embeds = view.querySelectorAll('embed');  console.log(`【MP_SVG_REVISE】 检测到 ${embeds.length} 个目标……`);  let promises = [];  embeds.forEach((embed, index) => {    console.log(`【MP_SVG_REVISE】 第 ${index} 个……`);    let parent_node = embed.parentNode;    promises.push(new Promise(resolve => {      loadSVG(embed.src).then(svg => {        parent_node.insertBefore(svg, embed);        parent_node.removeChild(embed);        resolve();      })    }))  });  Promise.all(promises).then(() => {    console.log('Revise complete！');    alert('Revise complete！');  })}revise()">Revise MP Editor SVG</a>
  </div>
</center>

