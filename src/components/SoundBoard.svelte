<script>
	import sounds from '../data/sounds.json';	
	const playlist = sounds

	let playingState = 'paused'
	let songPlayingIndex = 0
	let song = null

	function loadSong() {
		song = new Audio(sounds[songPlayingIndex].audio)
		song.volume = 0.8
		song.play()		
	}

	function play() {
		if (playingState === 'playing') {
			pause()
		}
		
		playingState = 'playing'
		loadSong()
	}
	
	function playSelectedSong(event) {		
		const songIndex = +event.target.dataset.index
		
		/*
			if (songIndex === songPlayingIndex) {
			songPlayingIndex = null
			return pause()
		}
		*/
		
		songPlayingIndex = songIndex
		play()
	}

	function pause() {
		playingState = 'paused'
		song.pause()
	}

</script>

<div class="player">
	<div class="playlist">	
		{#each playlist as song, index}
			<button data-index={index} on:click={playSelectedSong} class="ripple">
				<img data-index={index} width=180px height=180px src={song.img} alt="" />
				<h3 data-index={index} class="title">{song.title}</h3>	
			</button>
		{/each}
	</div>
</div>

<style>
	.playlist {
		display: flex;
		gap: 2em;
		flex-wrap: wrap;
		min-width: 300px ;
		padding: 2em;
		justify-content: center;
	}
	
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