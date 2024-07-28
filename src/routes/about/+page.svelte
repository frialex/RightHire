<svelte:head>
	<title>About</title>
	<meta name="description" content="About this app" />
</svelte:head>



<div class="text-column">
	<p>Record camera for interview questions</p>
	
	<video autoplay></video>
  <button on:click={startRecord}>Start</button>
  <button on:click={stopRecording}>Stop</button>
</div>



<script lang="ts">
  import { browser } from "$app/environment";

  let recorder: MediaRecorder;

  //audio false to prevent echo
  //https://mdn.github.io/dom-examples/media/web-dictaphone/

  browser && navigator.mediaDevices
    .getUserMedia({ video: { facingMode: "user" }, audio: false })
    .then((stream) => {
      const video = document.querySelector("video");
      if(video) video.srcObject = stream;

      recorder = new MediaRecorder(stream);
      recorder.ondataavailable = (e)=>{
        let blob = e.data;
        let type = blob.type;
        //TODO: post blob to api endpoint to be saved
        //TODO: save in to chunks[] ?
        let url = URL.createObjectURL(blob);
        playBlobVideo(url)
        debugger;

      }

    })
    .catch((error) => {
      console.log("Rejected!", error);
    });

    
    function playBlobVideo(url){
      //TODO;
      //https://developer.mozilla.org/en-US/docs/Web/API/MediaRecorder/dataavailable_event
        
    }

    function startRecord(){    recorder?.start();  }
    function stopRecording(){  recorder.stop();    }
</script>