Here is some CSS and Js code for Scroll to top button
Js code
```js
window.addEventListener('scroll', function () {
    const scrollTopBtn = document.querySelector('.scroll-top');
    if (window.scrollY >= 300) {
      scrollTopBtn.classList.add('active');
    } else {
      scrollTopBtn.classList.remove('active');
    }
  });
```
CSS code
```css
.scroll-top{
    position: fixed;
    right: 30px;
    bottom: -100%;
    transition: all 1s !important;
}

.scroll-top.active{
    bottom: 40px;
}
```
