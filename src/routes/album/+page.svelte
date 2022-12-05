<script>
	import { audioData } from './audioData.js';

	import TrackHeading from './TrackHeading.svelte';
	import ProgressBarTime from './ProgressBarTime.svelte';
	import Controls from './Controls.svelte';
	import VolumeSlider from './VolumeSlider.svelte';
	import PlayList from './PlayList.svelte';
	import { onMount } from 'svelte';

// Get Audio track
	let trackIndex = 0;
	let trackTitle = audioData[trackIndex].name;
	onMount(() => {
		audioFile = new Audio(audioData[trackIndex].url);
	});
	let audioFile = new Audio(audioData[trackIndex].url);

	

	
	// $: console.log(trackIndex)


	const loadTrack = () => {
		audioFile = new Audio(audioData[trackIndex].url);
		audioFile.onloadedmetadata = () => {
			totalTrackTime = audioFile.duration;
			updateTime();
		};
		trackTitle = audioData[trackIndex].name;
	};

	const autoPlayNextTrack = () => {
		if (trackIndex <= audioData.length - 1) {
			trackIndex += 1;
			loadTrack();
			audioFile.play();
		} else {
			trackIndex = 0;
			loadTrack();
			audioFile.play();
		}
	};

	// Track Duration and Progress Bar
	/**
	 * @type {number}
	 */
	let totalTrackTime;
	$: console.log(totalTrackTime);
	audioFile.onloadedmetadata = () => {
		totalTrackTime = audioFile.duration;
		updateTime();
	};

	let totalTimeDisplay = 'loading...';
	let currTimeDisplay = '0:00:00';
	let progress = 0;
	/**
	 * @type {string | number | NodeJS.Timeout | undefined}
	 */
	let trackTimer;

	function updateTime() {
		progress = audioFile.currentTime * (100 / totalTrackTime);

		let currHrs = Math.floor(audioFile.currentTime / 60 / 60);
		let currMins = Math.floor(audioFile.currentTime / 60);
		let currSecs = Math.floor(audioFile.currentTime - currMins * 60);

		let durHrs = Math.floor(totalTrackTime / 60 / 60);
		let durMins = Math.floor((totalTrackTime / 60) % 60);
		let durSecs = Math.floor(totalTrackTime - durHrs * 60 * 60 - durMins * 60);

		// @ts-ignore
		if (currSecs < 10) currSecs = `0${currSecs}`;
		// @ts-ignore
		if (durSecs < 10) durSecs = `0${durSecs}`;
		// @ts-ignore
		if (currMins < 10) currMins = `0${currMins}`;
		// @ts-ignore
		if (durMins < 10) durMins = `0${durMins}`;

		currTimeDisplay = `${currHrs}:${currMins}:${currSecs}`;
		totalTimeDisplay = `${durHrs}:${durMins}:${durSecs}`;

		if (audioFile.ended) {
			toggleTimeRunning();
		}
	}

	const toggleTimeRunning = () => {
		if (audioFile.ended) {
			isPlaying = false;
			clearInterval(trackTimer);
			console.log(`Ended = ${audioFile.ended}`);
		} else {
			trackTimer = setInterval(updateTime, 100);
		}
	};

	// Controls
	let isPlaying = false;
	$: console.log(`isPlaying = ${isPlaying}`);

	const playPauseAudio = () => {
		if (audioFile.paused) {
			toggleTimeRunning();
			audioFile.play();
			isPlaying = true;
		} else {
			toggleTimeRunning();
			audioFile.pause();
			isPlaying = false;
		}
	};

	const rewindAudio = () => (audioFile.currentTime -= 10);
	const forwardAudio = () => (audioFile.currentTime += 10);

	// Volume Slider
	let vol = 50;
	const adjustVol = () => (audioFile.volume = vol / 100);

	// Playlist
	// @ts-ignore
	const handleTrack = (e) => {
		if (!isPlaying) {
			trackIndex = Number(e.target.dataset.trackId);
			loadTrack();
			playPauseAudio(); // auto play
		} else {
			isPlaying = false;
			audioFile.pause();
			trackIndex = Number(e.target.dataset.trackId);
			loadTrack();
			playPauseAudio(); // auto play
		}
	};
</script>

<div class="text-column">
	<!-- <main> -->

	<section id="player-cont">
		<TrackHeading {trackTitle} />
		<!-- need better way to space this :/ jaja  -->
		<br />
		<br />
		<br />
		<br />
		<br />
		<br />
		<br />
		<br />
		<br />
		<br />
		<br />
		<br />
		<br />
		<br />
		<div id="cntrls">
			
			<Controls
				{isPlaying}
				on:rewind={rewindAudio}
				on:playPause={playPauseAudio}
				on:forward={forwardAudio}
			/>

			<VolumeSlider bind:vol on:input={adjustVol} />

			<ProgressBarTime {currTimeDisplay} {totalTimeDisplay} {progress} />

			
			
		</div>
	</section>

	<PlayList on:click={handleTrack} />
	<!-- </main> -->
</div>

<style>
	/* main {
		width: 100vw;
		height: 100vh;
		display: flex;
		flex-direction: column;
		align-items: center;
		justify-content: center;
		padding: 20px 0 0 0;
		background-color: #ddd;
	} */

	#player-cont {
		width: 480px;
		height: 480px;
		/* padding: 0.7rem 1.5rem 0; */
		box-shadow: 0 0 5px black;
		background: transparent;
		color: var(--color-theme-1);
		border-radius: 5px 5px 0 0;
		background: url('/bobpeace2.gif');
	}

	#cntrls {
		vertical-align: bottom;
	}
</style>
