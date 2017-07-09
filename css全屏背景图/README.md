# CSS全屏背景图

## 目标

- 全屏展示背景图片，无空白区域
- 必要时缩放图片
- 保持图像的纵横比
- 图片在页面居中显示
- 不出现滚动条
- 尽可能有较好的浏览器兼容性

## CSS3的实现方法

**CSS3:**

```css
html { 
  background: url(images/bg.jpg) no-repeat center center fixed; 
  -webkit-background-size: cover;
     -moz-background-size: cover;
       -o-background-size: cover;
          background-size: cover;
}
```

兼容：

- Safari 3+
- Chrome Whatever+
- IE 9+
- Opera 10+ (Opera 9.5 supported background-size but not the keywords)
- Firefox 3.6+ (Firefox 4 supports non-vendor prefixed version)

## CSS的实现方法

**CSS:**

```css
img.full-screen-bg {
  /* Set rules to fill background */
  min-height: 100%;
  min-width: 1024px;

  /* Set up proportionate scaling */
  width: 100%;
  height: auto;

  /* Set up positioning */
  position: fixed;
  top: 0;
  left: 0;
}

@media screen and (max-width: 1024px) { /* Specific to this particular image */
  img.full-screen-bg {
    left: 50%;
    margin-left: -512px;   /* 50% */
  }
}
```

**SCSS:**

```scss
/* the bg-min-width variable */
$full-screen-bg-min-width: 1024px;

img.full-screen-bg {
  /* Set rules to fill background */
  min-height: 100%;
  min-width: $full-screen-bg-min-width;

  /* Set up proportionate scaling */
  width: 100%;
  height: auto;

  /* Set up positioning */
  position: fixed;
  top: 0;
  left: 0;
}

@media screen and (max-width: $full-screen-bg-min-width) { /* Specific to this particular image */
  img.full-screen-bg {
    left: 50%;
    margin-left: $full-screen-bg-min-width/-2;   /* -50% */
  }
}
```

兼容：

- Any version of good browsers: Safari / Chrome / Opera / Firefox
- IE 6: Borked - but probably fixable if you use some kind of fixed positioning shim
- IE 7/8: Mostly works, doesn't center at small sizes but fills screen fine
- IE 9: Works

## jQuery方式

**HTML:**

```html
<img src="images/bg.jpg" id="bg" alt="">
```

**CSS:**

```css
#bg { position: fixed; top: 0; left: 0; }
.bgwidth { width: 100%; }
.bgheight { height: 100%; }
```

**Javascript:**

```js
$(window).load(function () {

  var theWindow = $(window),
    $bg = $("#bg"),
    aspectRatio = $bg.width() / $bg.height();

  function resizeBg() {
    if ((theWindow.width() / theWindow.height()) < aspectRatio) {
      $bg
        .removeClass()
        .addClass('bgheight');
    } else {
      $bg
        .removeClass()
        .addClass('bgwidth');
    }
  }

  theWindow.resize(resizeBg).trigger("resize");

});
```

## 原文

* [Perfect Full Page Background Image](https://css-tricks.com/perfect-full-page-background-image/)  --By Chris Coyier On November 20, 2010