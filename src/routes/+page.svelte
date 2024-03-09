<script lang="ts">
     let names: string[] = [];
     let numbers: number[] = [];
    let editNum = -1;

    function add() {
        const nameInput = document.getElementById('namesInput') as HTMLInputElement;
        const numberInput = document.getElementById('numbersInput') as HTMLInputElement;

         if (nameInput && numberInput) {
        names = [...names, nameInput.value];
        numbers = [...numbers, parseInt(numberInput.value)];

        nameInput.value = '';
        numberInput.value = '';
    };
    }

    function update() {
        const nameInput = document.getElementById('namesInput') as HTMLInputElement;
    const numberInput = document.getElementById('numbersInput') as HTMLInputElement;

        if (nameInput && numberInput) {
        names[editNum] = nameInput.value;
        numbers[editNum] = parseInt(numberInput.value);

        nameInput.value = '';
        numberInput.value = '';

        editNum = -1; // Reset editNum after update
    }
}

    function edit(index: number) {
          editNum = index;
          const nameInput = document.getElementById('namesInput') as HTMLInputElement;
         const numberInput = document.getElementById('numbersInput') as HTMLInputElement;

        if (nameInput && numberInput) {
          nameInput.value = names[index];
          numberInput.value = numbers[index].toString();
    }

}
	function deleteFunction(index: number): any {
		names = names.filter((_, i) => i !== index);
		numbers = numbers.filter((_, i) => i !== index);
	}
</script>

<main>
    <div class="right">
        <h1>Provide the details.</h1>
        <div class="name">
            <h3>Name</h3>
            <input type="text" placeholder="Type here" class="input input-bordered input-primary w-full max-w-xs" id="namesInput"/>
        </div>
        <div class="number">
            <h3>Number</h3>
           <input type="number" placeholder="Type here" class="input input-bordered input-primary w-full max-w-xs" id="numbersInput"/>
        </div>
        <button class="btn btn-primary" on:click={add}>ADD</button>
        <button class="btn btn-primary" on:click={update}>UPDATE</button>
    </div>
    <div class="left">
        {#each names as name, index}
        <div class="card w-96 bg-neutral text-neutral-content">
            <div class="card-body items-center text-center">
              <h2 class="card-title">{name}</h2>
              <p>{numbers[index]}</p>
              <div class="card-actions justify-end">
                <button class="btn btn-primary" on:click={() => edit(index)}>Edit</button>
                <button class="btn btn-ghost"on:click={() => deleteFunction(index)}>Delete</button>
              </div>
            </div>
          </div>
          {/each}
    </div>
</main>

<style>
     .text-neutral-content{
        border: 1px solid white;
     }
    .btn-ghost{
        border: 1px solid white;
    }
    h1{
        font-size: x-large;
        color: white;
    }
    h3{
        color: white;
        font-weight: bold;
    }
    main {
        background: #24292E;
        position: absolute;
        padding: 100px;
        width: 100%;
        height: 100%;
        display: flex;
        align-items: center;
    }
    div{
        padding: 5px;
    }
    button{
        width: 160px;
    }
    .left, .right {
        height: 100%;
        width: 100%;
        padding: 130px;
    }

    .right {
        border-right: 1px solid white;
    }
    .left{
        display: flex;
        align-items: center;
        justify-content: space-between;
        flex-direction: column;
    }
</style>
