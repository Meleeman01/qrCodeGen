
<script>
  import QrCode from "svelte-qrcode"
  import { SvelteToast,toast } from '@zerodevx/svelte-toast'



  let size = '300';
  let bgColor="#ffffff";
  let fgColor="#000000";

  let qrCodeLink = 'https://www.youtube.com/watch?v=H9K8-3PHZOU';
  let qrCodeColor='#000000';
  let qrCodeBackground='#ffffff';
  let input = '';
  // let toastOps = {
  //    duration: 8000,       // duration of progress bar tween to the `next` value
  // initial: 1,           // initial progress bar value
  // next: 0,              // next progress value
  // pausable: false,      // pause progress bar tween on mouse hover
  // dismissable: true,    // allow dismiss with close button
  // reversed: false,      // insert new toast to bottom of stack
  // intro: { x: 256 },    // toast intro fly animation settings
  // theme: {},            // css var overrides
  // classes: []           // user-defined classes
  // };

  function handleClick(e) {
    if (!input.includes('http')) {
      console.log('error, no http')
      toast.push('Error, not in http format.',{
        duration:8000,
        theme: {
    '--toastBackground': '#ff575c',
    '--toastColor': 'white',
    '--toastBarBackground': 'rgba(0, 0, 0, 0.1)',

  }
      })
    }
    else{
      console.log('input changed');
      qrCodeLink = input;
      qrCodeBackground = bgColor;
      qrCodeColor = fgColor;

      console.log(qrCodeColor,qrCodeBackground,qrCodeLink);
    } 
  }

  function changeFg(e) {
    // body...
    console.log(e.target);
    if (e.target.nodeName == 'DIV') {
      console.log('div clicked')
      e.target.children[0].click();
    }
    if (e.target.nodeName == 'LABEL') {
      console.log('lable clicked');
      e.target.previousElementSibling.click();
    }
    console.log(fgColor);
  }

  function changeBg(e) {
    console.log(e.target);
    if (e.target.nodeName == 'DIV') {
      console.log('div clicked')
      e.target.children[0].click();
    }
    if (e.target.nodeName == 'LABEL') {
      console.log('lable clicked');
      e.target.previousElementSibling.click();
    }
    console.log(bgColor);
    //make a copy of 
    let a = qrCodeLink;

    qrCodeLink = "http";

    qrCodeLink = a;


  }

</script>
<main>
  <SvelteToast />
  <div class="flx(column) center middle is-6">
    <h1>QR Code Generator</h1>
    <div class="flx center middle is-12 qr">
      <QrCode bind:color={qrCodeColor} background={qrCodeBackground}  size="{size}" value="{qrCodeLink}" />
    </div>
    <div class="flx(column) space-evenly center card" >
      <h3>
        Enter a url to Create a QR code!
      </h3>
      <label>Url:</label>
      <input class="padme is-round" type="text" bind:value={input} placeholder="{qrCodeLink}" />
      <label>Size:</label>
      <input class="padme is-round" type="text" bind:value={size} style="margin-bottom:1rem;">

      <div on:click={changeFg} class="flx(wrap) left middle is-fluid color-selector-wrapper">
        <input bind:value={fgColor} type="color" name="">
        <label style="margin-left: .5rem;">Foreground Color</label>
      </div>
      
      
      <div on:click={changeBg}  class="flx(wrap) left middle is-fluid color-selector-wrapper" style="background-color: white;">
        <input bind:value={bgColor} type="color" />
        <label style="margin-left: .5rem;">Background Color</label>
      </div>
      
      <button class="btn is-primary is-round" type="submit" on:click={handleClick}>
        Submit
      </button>
    </div>
    
  </div>
  

  
</main>

<style>
  h1 {
    text-align: center;
  }
  .card {
    background-color: #e3e3e3; 
    padding:2rem; 
    border-radius:1rem;
  }
  .card > input[type='text']:focus {
    border-radius: 4rem;
  }
  .card > input {
    margin-bottom: .5rem;
  }
  .card > h3 {
    text-align: center;
  }
  .qr {
    margin-bottom: 1rem;
  }
  .color-selector-wrapper {
    background-color: white;
    padding: .5rem;
    border-radius: 2rem;
    padding-left: 2rem;
    margin-bottom: 1rem;
  }
  input[type="color"] {
    -moz-appearance:none;
    -webkit-appearance: none;
    border:none;
      border-radius: 2rem;
      width: 30px;
      height: 20px;
  }
  ._toastBar {
  display: none;
}
</style>
