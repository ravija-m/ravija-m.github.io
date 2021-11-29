---
layout: default
title: "Thesis - OrthoApp"
permalink: /projects/thesis
---

### Thesis - Application for Postoperative care of Orthopaedic Patients


The demand for hip and knee replacement procedures is steadily rising each year as the prevalence of osteoarthritis increases. This mobile application provides an economical alternative to traditional rehabilitation for orthopaedic patients.

There's a full [report](https://drive.google.com/file/d/11QQbEJHkhoSAiykp7OfeOrpgM3UIDt04/view?usp=sharing) if you're interested.

<div id="drag-container">
  <div id="spin-container">
    <!-- Application screens -->
    <img src="../assets/home.png" alt="Home">
    <img src="../assets/rom.png" alt="ROM Upload">
    <img src="../assets/exercises.png" alt="Exercises">
    <img src="../assets/postop.png" alt="Post=operative Info">
    <img src="../assets/wound.png" alt="Wound Upload">
    <img src="../assets/notifications.png" alt="Notifications">
    <img src="../assets/settings.png" alt="Settings">

    <!-- Text at center of ground -->
    <p> Main Application Screens </p>

  </div>
  <div id="ground"></div>
</div>

<div id="music-container"></div>

<style>
    html,
    body {
        height: 100%;
        /* for touch screen */
        /* touch-action: none;  */
    }

    body {
        overflow: hidden;
        display: -webkit-box;
        display: -ms-flexbox;
        display: flex;
        flex-direction: column;
        -webkit-perspective: 1000px;
                perspective: 1000px;
        -webkit-transform-style: preserve-3d;
                transform-style: preserve-3d;
    }

    #drag-container, #spin-container {
        position: relative;
        display: -webkit-box;
        display: -ms-flexbox;
        display: flex;
        margin: auto;
        -webkit-transform-style: preserve-3d;
                transform-style: preserve-3d;
        -webkit-transform: rotateX(-10deg);
                transform: rotateX(-10deg);
    }

    #drag-container img, #drag-container video {
        -webkit-transform-style: preserve-3d;
                transform-style: preserve-3d;
        position: absolute;
        left: 0;
        top: 0;
        width: 100%;
        height: 100%;
        line-height: 200px;
        font-size: 50px;
        text-align: center;
        -webkit-box-shadow: 0 0 8px #fff;
                box-shadow: 0 0 8px #fff;
        -webkit-box-reflect: below 10px linear-gradient(transparent, transparent, #0005);
    }

    #drag-container img:hover, #drag-container video:hover {
        -webkit-box-shadow: 0 0 15px #fffd;
                box-shadow: 0 0 15px #fffd;
        -webkit-box-reflect: below 10px linear-gradient(transparent, transparent, #0007);
    }

    #drag-container p {
        margin-top: 10%;
        font-family: Serif;
        position: absolute;
        top: 100%;
        left: 50%;
        -webkit-transform: translate(-50%,-50%) rotateX(90deg);
                transform: translate(-50%,-50%) rotateX(90deg);
        color: #fff;
    }

    #ground {
        width: 900px;
        height: 900px;
        position: absolute;
        top: 100%;
        left: 50%;
        -webkit-transform: translate(-50%,-50%) rotateX(90deg);
                transform: translate(-50%,-50%) rotateX(90deg);
        background: -webkit-radial-gradient(center center, farthest-side , #9993, transparent);
    }

    #music-container {
        position: absolute;
        top: 0;
        left: 0;
    }

    @-webkit-keyframes spin {
    from{
        -webkit-transform: rotateY(0deg);
                transform: rotateY(0deg);
    } to{
        -webkit-transform: rotateY(360deg);
                transform: rotateY(360deg);
    }
    }

    @keyframes spin {
    from{
        -webkit-transform: rotateY(0deg);
                transform: rotateY(0deg);
    } to{
        -webkit-transform: rotateY(360deg);
                transform: rotateY(360deg);
    }
    }
    @-webkit-keyframes spinRevert {
    from{
        -webkit-transform: rotateY(360deg);
                transform: rotateY(360deg);
    } to{
        -webkit-transform: rotateY(0deg);
                transform: rotateY(0deg);
    }
    }
    @keyframes spinRevert {
    from{
        -webkit-transform: rotateY(360deg);
                transform: rotateY(360deg);
    } to{
        -webkit-transform: rotateY(0deg);
                transform: rotateY(0deg);
    }
    }
</style>

<script>
    // Author: Hoang Tran (https://www.facebook.com/profile.php?id=100004848287494)
    // Github verson (1 file .html): https://github.com/HoangTran0410/3DCarousel/blob/master/index.html


    // You can change global variables here:
    var radius = 240; // how big of the radius
    var autoRotate = true; // auto rotate or not
    var rotateSpeed = -60; // unit: seconds/360 degrees
    var imgWidth = 150; // width of images (unit: px)
    var imgHeight = 290; // height of images (unit: px)

    // Link of background music - set 'null' if you dont want to play background music
    var bgMusicURL = null;
    var bgMusicControls = false; // Show UI music control


    // ===================== start =======================
    // animation start after 1000 miliseconds
    setTimeout(init, 1000);

    var odrag = document.getElementById('drag-container');
    var ospin = document.getElementById('spin-container');
    var aImg = ospin.getElementsByTagName('img');
    var aVid = ospin.getElementsByTagName('video');
    var aEle = [...aImg, ...aVid]; // combine 2 arrays

    // Size of images
    ospin.style.width = imgWidth + "px";
    ospin.style.height = imgHeight + "px";

    // Size of ground - depend on radius
    var ground = document.getElementById('ground');
    ground.style.width = radius * 3 + "px";
    ground.style.height = radius * 3 + "px";

    function init(delayTime) {
    for (var i = 0; i < aEle.length; i++) {
        aEle[i].style.transform = "rotateY(" + (i * (360 / aEle.length)) + "deg) translateZ(" + radius + "px)";
        aEle[i].style.transition = "transform 1s";
        aEle[i].style.transitionDelay = delayTime || (aEle.length - i) / 4 + "s";
    }
    }

    function applyTranform(obj) {
    // Constrain the angle of camera (between 0 and 180)
    if(tY > 180) tY = 180;
    if(tY < 0) tY = 0;

    // Apply the angle
    obj.style.transform = "rotateX(" + (-tY) + "deg) rotateY(" + (tX) + "deg)";
    }

    function playSpin(yes) {
    ospin.style.animationPlayState = (yes?'running':'paused');
    }

    var sX, sY, nX, nY, desX = 0,
        desY = 0,
        tX = 0,
        tY = 10;

    // auto spin
    if (autoRotate) {
    var animationName = (rotateSpeed > 0 ? 'spin' : 'spinRevert');
    ospin.style.animation = `${animationName} ${Math.abs(rotateSpeed)}s infinite linear`;
    }

    // add background music
    if (bgMusicURL) {
    document.getElementById('music-container').innerHTML += `
    <audio src="${bgMusicURL}" ${bgMusicControls? 'controls': ''} autoplay loop>    
    <p>If you are reading this, it is because your browser does not support the audio element.</p>
    </audio>
    `;
    }

    // setup events
    document.onpointerdown = function (e) {
    clearInterval(odrag.timer);
    e = e || window.event;
    var sX = e.clientX,
        sY = e.clientY;

    this.onpointermove = function (e) {
        e = e || window.event;
        var nX = e.clientX,
            nY = e.clientY;
        desX = nX - sX;
        desY = nY - sY;
        tX += desX * 0.1;
        tY += desY * 0.1;
        applyTranform(odrag);
        sX = nX;
        sY = nY;
    };

    this.onpointerup = function (e) {
        odrag.timer = setInterval(function () {
        desX *= 0.95;
        desY *= 0.95;
        tX += desX * 0.1;
        tY += desY * 0.1;
        applyTranform(odrag);
        playSpin(false);
        if (Math.abs(desX) < 0.5 && Math.abs(desY) < 0.5) {
            clearInterval(odrag.timer);
            playSpin(true);
        }
        }, 17);
        this.onpointermove = this.onpointerup = null;
    };

    return false;
    };

    document.onmousewheel = function(e) {
    e = e || window.event;
    var d = e.wheelDelta / 20 || -e.detail;
    radius += d;
    init(1);
    };

</script>


