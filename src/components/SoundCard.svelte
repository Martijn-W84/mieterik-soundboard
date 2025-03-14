<script>
    export let img = ''
    export let sound = ''
    export let title = ''

    let song = null

	function playSong() {
        song = new Audio(sound)
		song.src = sound
        song.volume = 0.5
		song.play()        		
	}
</script>

<button class="ripple" onclick={playSong}>
    <img width=180px height=180px src={img} alt="" />
    <h3 class="title">{title}</h3>	
</button>

<style>
    button {
        background-color: rgb(255, 255, 255);
        border-style: none;
        box-shadow: 2px 4px 24px -6px rgba(0, 0, 0, 0.1);
        padding : 1.25em;
        font-family: 'Lucida Sans', 'Lucida Sans Regular', 'Lucida Grande', 'Lucida Sans Unicode', Geneva, Verdana, sans-serif;
        transition: all .2s ease-in-out;
    }

    button:hover {
        /*animation: wiggle 2s;*/
        transform: scale(1.03);    
    }

    @keyframes wiggle {
        0%,
        5%{
            transform: rotateZ(0);
        }    
        15%{
            transform: rotateZ(-15deg);
        }
        20%{
            transform: rotateZ(10deg);
        }
        25%{
            transform: rotateZ(-10deg);
        }
        30%{
            transform: rotateZ(6deg);
        }
        35%{
            transform: rotateZ(-4deg);
        }
        40%,
        100%{
            transform: rotateZ(0);
        }
    }   

    .ripple {
  position: relative;
  overflow: hidden;
  transform: translate3d(0, 0, 0);
}

.ripple:after {
  content: "";
  display: block;
  position: absolute;
  width: 100%;
  height: 100%;
  top: 0;
  left: 0;
  pointer-events: none;
  background-image: radial-gradient(circle, #000 10%, transparent 10.01%);
  background-repeat: no-repeat;
  background-position: 50%;
  transform: scale(10,10);
  opacity: 0;
  transition: transform .5s, opacity 1s;
}

.ripple:active:after {
  transform: scale(0,0);
  opacity: .2;
  transition: 0s;
}
</style>