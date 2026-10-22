<script lang="ts">
    let {
        question,
        rightAnswer,
        wrongAnswers,
        answeredCallback,
    } = $props();
    
    function shuffle(array: Array<any>) {
        let currentIndex = array.length;

        while (currentIndex != 0) {

            let randomIndex = Math.floor(Math.random() * currentIndex);
            currentIndex--;

            [array[currentIndex], array[randomIndex]] = [array[randomIndex], array[currentIndex]];
        }
    }

    let answers = $derived.by(() => {
        let ans = [rightAnswer, ...wrongAnswers];
        ans[0] = {"correct": true, "text": ans[0]}
        for(let i = 1; i < ans.length; ++i)
            ans[i] = {"correct": false, "text": ans[i]};
        shuffle(ans);
        return ans;
    });
</script>

<div class="container">
    <h3>{question}</h3>
    {#each answers as answer}
        <button class="answer-btn" onclick={answer.correct ? () => answeredCallback(true) : () => answeredCallback(false)}>{answer.text}</button>
    {/each}
</div>

<style>
* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}

.container {
    background-color: white;
    border-radius: 8px;
    box-shadow: 0px 5px 15px rgba(0,0,0,0.1);
    max-width: 400px;
    width: 100%;
    padding: 30px;
    overflow: hidden;
}

h3 {
    text-align: center;
    margin-bottom: 1.2rem;
}

.answer-btn {
    width: 100%;
    padding: 12px 16px;
    margin-bottom: 10px;
    border: none;
    border-radius: 7px;
    background-color: #c7d7f7;
    color: #111827;
    font-size: 1rem;
    font-weight: 600;
    cursor: pointer;
    transition: background-color 0.2s ease, transform 0.2s ease;
}

.answer-btn:hover {
    background-color: #3b82f6;
    color: white;
    transform: translateY(-2px);
}
</style>
