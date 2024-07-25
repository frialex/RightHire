<svelte:head>
	<title>About</title>
	<meta name="description" content="About this app" />
</svelte:head>

<div class="text-column">
	<p>Record camera for interview questions</p>
	
	<video autoplay></video>
</div>



<script>
  navigator.mediaDevices
    .getUserMedia({ video: true, audio: true })
    .then((localMediaStream) => {
      const video = document.querySelector("video");
      video.srcObject = localMediaStream;
    })
    .catch((error) => {
      console.log("Rejected!", error);
    });
</script>