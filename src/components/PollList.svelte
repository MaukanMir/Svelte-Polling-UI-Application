<script>
// Component imports here
import PollDetails from "./PollDetails.svelte";
// import PollStore here
import PollStore from "../stores/PollStore";
// Lifecycle imports here
import {afterUpdate, beforeUpdate, onDestroy, onMount} from 'svelte';
// svelte imports here
import {fade,slide, scale} from "svelte/transition";

export let polls=[];

</script>

<div class="poll-list">
{#each $PollStore as poll (poll.id)}
    <div transition:fade> 
    <PollDetails {poll}/>
    </div>
{/each}
</div>

<style>
.poll-list{
display:grid;
grid-template-columns: 1fr 1fr;
grid-gap:20px;
}

</style>
