<template>
  <div id="app">
    <transition name="fade" mode="out-in">
        <router-view></router-view>
    </transition>
  </div>
</template>

<script>
import EventBus from './bus'
export default {
  name: 'App',
}
</script>


<style>
/* RESET

*****************************************/
html, body, div, span, applet, object, iframe, h1, h2, h3, h4, h5, h6, p, blockquote, pre, a, abbr, acronym, address, big, cite, code, del, dfn, em, font, ins, kbd, q, s, samp, small, strike, strong, sub, sup, tt, var, dl, dt, dd, ol, ul, li, fieldset, form, label, legend, table, caption, tbody, tfoot, thead, tr, th, td {border: 0;font-family: inherit;font-size: 100%;font-style: inherit;font-weight: inherit;margin: 0;outline: 0;padding: 0;vertical-align: baseline;}
article,aside,details,figcaption,figure,footer,header,hgroup,nav,section {display: block;font-family:'Ubuntu', sans-serif; }
audio,canvas,video {display: inline-block;max-width: 100%;}
html{-webkit-text-size-adjust: 100%;-ms-text-size-adjust:100%;}
body,button,input,select,textarea {color: #2b2b2b;font-family: 'Ubuntu', sans-serif;font-size: 16px;font-weight: 400;line-height: 1.5;}
body{background: white;}
a{color: #087be3;text-decoration: none;cursor: pointer;}
a:focus {outline: 0;color: #08c1e3;}
a:hover,a:active {outline: 0;}
a:active,a:hover {color: #065fb0;}
h1,h2,h3,h4,h5,h6{font-family:'Ubuntu', sans-serif; clear: both;font-weight: 700;margin: 36px 0 12px;}
h1{font-size: 26px;line-height: 1.3846153846;}
h2{font-size: 24px;line-height: 1;}
h3{font-size: 22px;line-height: 1.0909090909;margin-top: 60px;}
h4{font-size: 20px;line-height: 1.2;}
h5{font-size: 18px;line-height: 1.3333333333;}
h6{font-size: 14px;line-height: 1.3333333333;}
address{font-style: italic;margin-bottom: 24px;}
abbr[title]{border-bottom: 1px dotted #2b2b2b;cursor: help;}
b,strong{font-weight: 700;}
cite,dfn,em,i{font-style: italic;}
mark,ins{background: #fff9c0;text-decoration: none;}
p{margin-bottom: 24px; word-wrap: break-word;}
code,kbd,tt,var,samp,pre{font-family: monospace, serif;font-size: 15px;-webkit-hyphens: none;-moz-hyphens: none;-ms-hyphens:none;hyphens:none;line-height: 1.6;}
pre{border: 1px solid rgba(0, 0, 0, 0.1);-webkit-box-sizing: border-box;-moz-box-sizing:border-box;box-sizing:border-box;margin-bottom: 24px;max-width: 100%;overflow: auto;padding: 12px;white-space: pre;white-space: pre-wrap;word-wrap: break-word;}
blockquote,q {-webkit-hyphens: none;-moz-hyphens:none;-ms-hyphens:none;hyphens:none;quotes: none;}
blockquote:before,blockquote:after,q:before,q:after {content: "";content: none;}
blockquote {color: #767676;font-size: 19px;font-style: italic;font-weight: 300;line-height: 1.2631578947;margin-bottom: 24px;}
blockquote cite,blockquote small {color: #2b2b2b;font-size: 16px;font-weight: 400;line-height: 1.5;}
blockquote em,blockquote i,blockquote cite {font-style: normal;}
blockquote strong,blockquote b {font-weight: 400;}
small {font-size: smaller;}
big {font-size: 125%;}
sup,sub {font-size: 75%;height: 0;line-height: 0;position: relative;vertical-align: baseline;}
sup {bottom: 1ex;}sub {top: .5ex;}dl {margin-bottom: 24px;}dt {font-weight: bold;}dd {margin-bottom: 24px;}ul,ol {list-style: none;margin: 0 0 24px 20px;}
ul {list-style: disc;}ol{list-style: decimal;}li > ul,li > ol {margin: 0;}
img {-ms-interpolation-mode: bicubic;border: 0;vertical-align: middle;}
figure{margin: 0;}fieldset {border: 1px solid rgba(0, 0, 0, 0.1);margin: 0 0 24px;padding: 11px 12px 0;}
legend {white-space: normal;}
button,input,select,textarea {-webkit-box-sizing: border-box;-moz-box-sizing:border-box;box-sizing:border-box;font-size: 100%;margin: 0;max-width: 100%;vertical-align: baseline;}
button,input {line-height: normal;}
input,textarea {background-image: -webkit-linear-gradient(hsla(0,0%,100%,0), hsla(0,0%,100%,0));}
button,html input[type="button"],input[type="reset"],input[type="submit"] {-webkit-appearance: button;cursor: pointer;}
button[disabled],input[disabled] {cursor: default;}
input[type="checkbox"],input[type="radio"] {padding: 0;}
input[type="search"] {-webkit-appearance: textfield;}
input[type="search"]::-webkit-search-decoration {-webkit-appearance: none;}
button::-moz-focus-inner,input::-moz-focus-inner {border: 0;padding: 0;}
textarea {overflow: auto;vertical-align: top;}
table,th,td {border: 1px solid rgba(0, 0, 0, 0.1);}
table {border-collapse: separate;border-spacing: 0;border-width: 1px 0 0 1px;margin-bottom: 24px;width: 100%;}
caption,th,td { font-weight: normal;text-align: left;}th {border-width: 0 1px 1px 0;font-weight: bold;}
td {border-width: 0 1px 1px 0;}del {color: #767676;}hr {background-color: rgba(0, 0, 0, 0.1);border: 0;height: 1px;margin-top: 20px; margin-bottom: 30px;}
::selection {background: #087be3;color: white;text-shadow: none;}
::-moz-selection {background: #087be3;color: white;text-shadow: none;}
ul,li {list-style: none;margin: 0;padding: 0;}
mark, ins {background: transparent; text-decoration: none;}
.clear{clear: both;}
.hidden{display: none !important;}

#map {
    position: fixed;
    z-index: -1;
    width: 100%;
    height: 100%;
    top: 0;
    left: 0;
    pointer-events: none;
}
#map path{
    stroke-width: 0.1px;
    fill-rule:evenodd;
    transition: fill 450ms ease;
    transition-delay: 3000ms;
}
#map path.active{
}
#overmap {
    position: fixed;
    width: 100%;
    height: 100%;
    z-index: 1;
    pointer-events: none;
}
#overmap > div{
    width: 100%;
    position: absolute;
}

#overmap .top{
    top: 0;
    pointer-events: none;
}
#overmap .bottom{
    bottom: 0;
}
#overmap .right{
    right: 0;
}
#overmap .left{
    left: 0;
}
#overmap .right > div{
    margin-left: auto;
}
#overmap .main {
    padding: 0 10px;
    top: 100%;
    box-sizing: border-box;
    transition: top 350ms ease-in-out;
    pointer-events: none;
}
#overmap .main.active {
    top: 0;
}
#overmap .about {
    width: 100%;
    box-sizing: border-box;
    padding: 40px;
    max-width: 600px;
    background: #fffffff0;
    margin: 100px auto 0;
    pointer-events: all;
}
#overmap .about p:last-child {
    margin-bottom: 0;
}

.overmask {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    pointer-events: none;
}
.overmask.active {
    background: #00000087;
    pointer-events: all;
}

#sections {
    overflow: auto;
    position: relative;
}

.topmenu img {
    pointer-events: all;
    cursor: pointer;
}


.section-wrap {
    width: 100%;
    max-width: 600px;
    margin: 0;
}
.section{
    padding: 40px 40px;
    margin-bottom: 600px;
}
.section:last-child{
    margin-bottom: 0 !important;
}
.section h1{
}
.section p:last-child{
    margin-bottom: 20px !important;
}
.section img{
    width: 100%;
    max-width: 100%;
    height: auto;
}

.logos {
    width: 100%;
    max-width: 300px;
    display: flex;
}
.logos a {
    display: block;
    flex: 1 1 100%;
}

.topmenu {
    margin: 20px;
    width: 100%;
    max-width: 100px;
}


@media only screen and (min-width: 870px) {
    .section{
        padding: 40px 100px;
        margin-bottom: 600px;
    }
}






/* SVG Shits */
#world .animations > g {
    opacity: 0;
    transition: opacity 450ms ease;
    transition-delay: 2000ms;
}
#world .animations g.active {
    opacity: 1;
}



#app {
    height: 100%;
}


/* ANIMATIONS

*****************************************/
.fade-enter-active,
.fade-leave-active {
  transition-duration: 0.2s;
  transition-property: opacity;
  transition-timing-function: ease;
}

.fade-enter,
.fade-leave-active {
  opacity: 0
}
</style>