<script>
    //Poll store import here
    import PollStore from "../stores/PollStore";
    //import components here
    import Button from "../shared/Button.svelte";
    // svelte imports here
    import {createEventDispatcher} from "svelte";

let dispatch = createEventDispatcher();
let fields = {
    question:"",
    answerA: "",
    answerB:""
}

let errors = {
    question:"",
    answerA:"",
    answerB:""
}

let valid = false;

const submitHandler = ()=>{
    
    // validate question
    valid = fields.question.trim().length <5 || fields.answerA.trim().length <1 || fields.answerB.trim().length <1 ? false:true;
    // Change errors object
    errors.question = fields.question.trim().length <5  ? "Questions should be longer than 5 characters":""
    errors.answerA = fields.answerA.trim().length <1 ? "Questions should be longer than 1 or more characters":""
    errors.answerB = fields.answerB.trim().length <1? "Questions should be longer than 1 or more characters":""
    // display valid results here
    let poll = valid ? {...fields,votesA:0, votesB:0, id:Math.random()}: console.log(errors,"error")
    // save poll to store
    PollStore.update(currentPolls =>{
        return [poll, ...currentPolls];
    })
    valid ? dispatch("add"):""
}
</script>

<form on:submit|preventDefault ={submitHandler}>
    <div class ="form-field">
        <label for="question">Poll Question:</label>
        <input type ="text" id="question" bind:value={fields.question}/>
        <div class ="error">{errors.question}</div>
    </div>
    <div class ="form-field">
        <label for="answer-a">Answer A:</label>
        <input type ="text" id ="answer-a" bind:value ={fields.answerA}/>
        <div class ="error">{errors.answerA}</div>
    </div>
    <div class ="form-field">
        <label for="answer-b">Answer B:</label>
        <input type ="text" id ="answer-b" bind:value ={fields.answerB} />
        <div class ="error">{errors.answerB}</div>
    </div>
    <Button type ="secondary" flat ={true}> Add Poll</Button>
</form>



<style>
form{
    width:400px;
    margin: 0 auto;
    text-align:center;
}
.form-field{
    margin: 18px auto;
}
input{
    width: 100%;
    border-radius: 6px;
}
label{
    margin:10px auto;
    text-align:left;
}
.error{
    color:red;
    font-weight: bold;
    font-size:16px;

}
</style>