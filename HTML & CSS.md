# **HTML & CSS**

## 🔹 Image 
### Fallback image
``` HTML
<img onerror='path image or function'>
```

``` CSS
div {
    background: url('path'), url('path image replace');
}
```
### Tối ưu performance image với srcset

* Theo kích thức image
``` HTML
<img
    srcset="
        elva-fairy-480w.jpg 480w,
        elva-fairy-800w.jpg 800w
        "
    sizes="
        (max-width: 600px) 480px,
        800px"
    src="elva-fairy-800w.jpg"
    alt="Elva dressed as a fairy" 
/>
```

* Theo DPR
``` HTML
<img
    srcset="
        elva-fairy-480w.jpg 1x,
        elva-fairy-800w.jpg 2x
        "
    src="elva-fairy-800w.jpg"
    alt="Elva dressed as a fairy" 
/>
```

* Theo bối cảnh nội dung image
``` HTML
<picture>
    <source media='(max-width: 575px)' srcset="small.jpg" type="image/svg+xml">
    <img src="large.jpg" class="img-fluid img-thumbnail" alt="...">
</picture>
```