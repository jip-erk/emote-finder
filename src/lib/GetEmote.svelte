<script>
    import Radio from './Radio.svelte';
    import SevenTV from '7tv';
    import AutoComplete from "simple-svelte-autocomplete";


    let group = 1;
    const api = SevenTV();

    var emote;
    var emotePrev;
    let input ='';
    let currentEmote = '';
   

    async function getEmote() {
       
        const emotes = await api.fetchUserEmotes("fristi4");

        for (let i = 0; i < emotes.length; i++) {
            //console.log(emotes[i].name);
            if ((emotes[i].name).toLowerCase() == (input).toLowerCase()) {

                emote = `https://cdn.7tv.app/emote/${emotes[i].id}/`;
                emotePrev = `https://cdn.7tv.app/emote/${emotes[i].id}/4x`;
              //  console.log(results);
       
            }
        }
    }

    //autoComplete
    
    var emote_dic = {};
    var emote_name = [];

    var results = {};

    getEmoteNames();
    async function getEmoteNames() {
       
       const emotes = await api.fetchUserEmotes("fristi4");

       for (let i = 0; i < emotes.length; i++) {
           //console.log(emotes[i].name);
            //emote_names.push({name: emotes[i].name,id: emotes[i].id});
            emote_dic[emotes[i].name] = `https://cdn.7tv.app/emote/${emotes[i].id}/4x`;
            emote_name.push(emotes[i].name);
       }
       changeAutoComplete();
       
    }


    function changeAutoComplete() {
    
        results = {};
    if (emote_name.length) {
      let autoCompleteValues = autoComplete(input);
      autoCompleteValues.forEach(value => { results[value] = emote_dic[value] });
    }
  }

    function autoComplete(inputval){
        return emote_name.filter((value) => value.toLowerCase().includes(inputval.toLowerCase()));
    }

    function yestest(name){
        input = name;
        getEmote();
    }

    async function copy(){
     
        navigator.clipboard.writeText(emote + group + "x");

    }

  


  </script>
  


  <div class="imgHolder">
    <img src={emotePrev || 'https://cdn.7tv.app/emote/61eff3971300d0c637b93d45/4x'} alt="emote">
  </div>
 
  <div class="dowloadCont">
      <button class="copy" on:click={() => copy()}>copy</button>
    
      <Radio bind:group value={1}>1x</Radio>
      <Radio bind:group value={2}>2x</Radio>
      <Radio bind:group value={3}>3x</Radio>
      <Radio bind:group value={4}>4x</Radio>
</div>
    <div class="inputDiv">
        <input  type="text" bind:value={input} on:change={getEmote} on:input={() => changeAutoComplete()}  placeholder="emote">

        <div class="autoComplete">
            {#each Object.entries(results) as [name, id]}
                {#if name == input}
		            <div style="background-color: #008dd9;" on:click={() => yestest(name)} class="item"><img class="prevImg" alt="icon" src={id}><span class="text">{name.substring(0, 15)}</span></div>
                {:else}
                    <div on:click={() => yestest(name)} class="item"><img class="prevImg" alt="icon" src={id}><span class="text">{name.substring(0, 15)}</span></div>
                {/if}
	        {/each}
        </div>
    </div>
 


  <style>
    @import url('https://fonts.googleapis.com/css2?family=Roboto+Mono&display=swap');

    .imgHolder{
        padding: 5px;
    
        height: 300px;
       
       
    }

    img{
        height: 100%;
        width: auto;
    }

    input[type="text"]{
       width: 310px;
       background-color: #282c34;
       height: 35px;
       border: none;
       border-radius: 6px;
       padding-left: 5px;
       outline: none;
       font-size: 25px;
       color: #9096a7;
       font-family: 'Roboto Mono', monospace;
    }

    input[type="text"]:focus{
        outline: solid;
        outline-width: 2px;
        outline-color:aqua;
        outline-offset: 2px;
    }

    .inputDiv{
        border-radius: 8px;
        padding: 10px;
        background-color: #323844;
        margin: 0;
        width: 320px;
        height: 400px;
        margin-left: auto;
        margin-right: auto;
    }

    .dowloadCont{
        margin-bottom: 10px;
    }
    button{
        padding: 5px;
        margin: 3px 0 0 3px;
        width: 40px;
        border: none;
        height: 35px;
        border-radius: 5px;
        background-color: #323844;
        color: #9096a7;
        font-size: 20px;
        outline: solid;
        outline-color: rgba(0, 255, 255, 0);
        cursor: pointer;
    }
    button:hover{
        transition: outline-color 1s ease-out;
        
        outline: solid;
        outline-width: 2px;
        outline-color:aqua;
        outline-offset: 2px;
    }

    .copy{
        width: 150px;
    }
    

    .autoComplete{
        margin-top: 20px;
      
        height: 345px;
        overflow-y: scroll;
    }

    .item{
        width: 98%;
        height: 60px;
        margin-bottom: 5px;
        border-radius: 6px;
        background-color: #404653;
        display:flex;align-items:center;
    }

    .text{
   margin-left: 20px;
    }
    .prevImg{
        float: left;
        border-radius: 6px 0 0 6px;
    }
 
  </style>
  