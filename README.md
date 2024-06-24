![play](https://github.com/elishacmyk/system/assets/173669214/2e986f47-2c3c-4674-9986-c13407f7c265)
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="utf-8">
        <meta http-equiv="X-UA-Compatible" content="IE=edge">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <title>MUSIC SITE</title>
        <link rel="stylesheet" href="site.css">
    </head>
    <body>
       <div class="hero">
        <div class="navbar">
            <img src="" alt="logo">
            <ul>
                <li><a href="#">HOME</a></li>
                <li><a href="#">ABOUT</a></li>
                <li><a href="#">NEW SONG</a></li>
                <li><a href="#">ALBUM</a></li>
                <li><a href="#">CONTACT</a></li>
            </ul>
        </div>
        <div class="content">
            <div class="left">
                <h1>THE <br>REAL <br>MUSIC</h1>
            </div>
        </div>
        <div class="right">
            <p>click To Play</p>
            <img src="ply.png" id="icon">
        </div>
       </div> 
    </body>

    <audio id="mysong">
        <source src="chino.mp3" type="audio/mp3">
    </audio>

    <script>
        var mysong = document.getElementById("mysong");
        var icon = document.getElementById("icon");

        icon.onclick = function(){
            if(mysong.paused){
                mysong.play();
                icon.src = "media/play.png";
            }else{
                mysong.pause();
                icon.src = "media/pause.png";
            }

        }
    </script>
</html>
