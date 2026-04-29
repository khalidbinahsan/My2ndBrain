Add this to **Elementor** code
```html
<script>
document.addEventListener('DOMContentLoaded', function() {
    const tabsWrapper = document.querySelector('.e-n-tabs-heading');
    const container = document.querySelector('.e-n-tabs');

    if (tabsWrapper && container) {
        // 1. Create Parent Container for Buttons
        const navParent = document.createElement('div');
        navParent.className = 'tab-nav-controls';

        // 2. Create Buttons
        const prevBtn = document.createElement('button');
        prevBtn.innerHTML = '&#10094;'; 
        prevBtn.className = 'tab-nav-btn prev-tab';

        const nextBtn = document.createElement('button');
        nextBtn.innerHTML = '&#10095;'; 
        nextBtn.className = 'tab-nav-btn next-tab';

        // 3. Assemble: Add buttons to parent, then parent to main container
        navParent.appendChild(prevBtn);
        navParent.appendChild(nextBtn);
        
        // Use prepend to put the whole group at the start
        container.prepend(navParent);

        // 4. Scroll Logic
        nextBtn.addEventListener('click', () => {
            tabsWrapper.scrollBy({ left: 200, behavior: 'smooth' });
        });

        prevBtn.addEventListener('click', () => {
            tabsWrapper.scrollBy({ left: -200, behavior: 'smooth' });
        });
        
        // Auto-hide if no scroll needed
        const toggleButtons = () => {
            const hasOverflow = tabsWrapper.scrollWidth > tabsWrapper.clientWidth;
            navParent.style.display = hasOverflow ? 'flex' : 'none';
        };

        window.addEventListener('resize', toggleButtons);
        toggleButtons();
    }
});
</script>

<style>
.e-tabs-header-wrapper {
    position: relative;
    display: flex;
    align-items: center;
}
.tab-nav-btn {
    background: #fff;
    border: 1px solid #ccc;
    border-radius: 50%;
    width: 40px;
    height: 40px;
    cursor: pointer;
    display: flex;
    align-items: center;
    justify-content: center;
    z-index: 10;
    transition: 0.3s;
}
.tab-nav-btn:hover {
    background: #f0f0f0;
}
.tab-nav-controls { justify-content: end; gap: 7px; }
</style>
```