Make the header sticky top first. Then add this css
```css
selector.elementor-sticky--effects{
	background-color: rgba(0,0,0,0.4) !important;
	backdrop-filter: saturate(180%) blur(20px) !important;
}
selector{
	transition: background-color 1s ease !important;
}
selector.elementor-sticky--effects > .elementor-container{
	min-height: 70px;
}
selector > .elementor-container {
	transition: min-height 1s ease !important;
}
```