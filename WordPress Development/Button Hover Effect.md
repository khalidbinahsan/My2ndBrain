Button hover effect like https://iihaquetech.com/
```html
<a 
class="custom-btn" 
href="/contact-us/#contact-form" 
data-text="Contact Us"
style="background-color: var(--e-global-color-secondary); --text-color: #fff; --btn-bg: var(--e-global-color-primary)"
>
   <span class="btn-text">Contact Us</span>
</a>
```
CSS
```css
/* ========== Site Main Btn ======== */
.custom-btn,
#kba-submit-btn .elementor-button-content-wrapper{
	  font-size: 16px;
    line-height: 1;
    padding: 15px 20px;
    border-radius: 6px;
    font-weight: 600;
    font-family: 'Sora', sans-serif;
    width: fit-content;
    white-space: nowrap;
    text-overflow: ellipsis;
    display: inline-flex;
    align-items: center;
    text-align: center;
    -o-transition: all 0.4s ease-in-out;
    -webkit-transition: all 0.4s ease-in-out;
    transition: all 0.4s ease-in-out;
    z-index: 0;
    overflow: hidden;
    position: relative;
    letter-spacing: -0.01em;
    transform-style: preserve-3d;
}
.custom-btn:hover{
	background: var(--btn-bg) !important;
}
#kba-submit-btn{
	padding: 0;
	min-height: 0;
}
.custom-btn::before,
#kba-submit-btn .elementor-button-content-wrapper::before{
	  position: absolute;
    content: '';
    border-radius: inherit;
    -webkit-transition: all 0.4s ease;
    transition: all 0.4s ease;
    z-index: -1;
    top: 0;
    left: 0;
    height: 100%;
    width: 100%;
    background-size: 102% 102%;
    opacity: 0;
}
.custom-btn:hover::before,
#kba-submit-btn:hover .elementor-button-content-wrapper::before{
	opacity: 1;
}

.custom-btn::after,
#kba-submit-btn .elementor-button-content-wrapper::after{
	content: attr(data-text);
    display: inline-block;
    position: absolute;
    top: 50%;
    opacity: 0;
    transform: translate(0, 100%);
    transition: opacity 0.2s, transform 0.2s;
    transition-timing-function: cubic-bezier(0.455, 0.03, 0.515, 0.955);
   white-space: nowrap;
	 color: var(--text-color);
}
#kba-submit-btn .elementor-button-content-wrapper::after{
	content: "Send Message";
}
.custom-btn:hover::after,
#kba-submit-btn:hover .elementor-button-content-wrapper::after{
	  transform: translate(0%, -50%);
    opacity: 1;
}
.btn-text{
	transition: opacity 0.2s, transform 0.2s;
  transition-timing-function: cubic-bezier(0.455, 0.03, 0.515, 0.955);
	color: var(--text-color);
}
#kba-submit-btn .elementor-button-text{
	transition: opacity 0.2s, transform 0.2s;
  transition-timing-function: cubic-bezier(0.455, 0.03, 0.515, 0.955);
	color: #fff;
}
.custom-btn:hover .btn-text,
#kba-submit-btn:hover .elementor-button-text{
	transform: translateY(-150%);
  opacity: 0;
}
/* ========== Site Main Btn End ======== */
```