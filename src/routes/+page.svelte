<script lang="ts">
    import QuestionPanel from "./QuestionPanel.svelte";
    import { fade, fly } from "svelte/transition";
    let questions = [{
            "q": "What is the Capital of France?",
            "a": ["Paris", "Taris", "Patricks", "Tartarus"]// First answer provided here is the right answer; Order will be randomised inside QuestionPanel.
        },
        {
            "q": "What is 1 + 6?",
            "a": ["7", "21", "Paris", "Math"]
        },
        {
            "q": "What is 5 - 3?",
            "a": ["2", "8", "15", "1"]
        },
        {
            "q": "Which is not the capital of France?",
            "a": ["Berlin", "Paris", "Paris", "Paris"]
        },
        {
            "q": "Which god is known as the god of fire and forge in Rome?",
            "a": ["Vulcan", "Hephaestus", "Mars", "Neptune"]
        },
        {
            "q": "Which god is known as the goddess of fire in Greece?",
            "a": ["Hestia", "Hephaestus", "Poseidon", "Neptune"]
        },
        {
            "q": "Which god is known as the god of knowledge, with a different name in Greece?",
            "a": ["Minerva", "Hermes", "Mars", "Neptune"]
        }
    ]
    let curQuestion = $state(0);
    let score = $state(0);

    import { elasticOut } from 'svelte/easing';

	function overlyDramaticTransition(node: HTMLElement, { duration }: { duration: number }) {
		return {
			duration,
			css: (t: number, u: number) => {
				const eased = elasticOut(t);

				return `
					transform: scale(${eased}) rotate(${eased * 1080}deg);
					color: hsl(
						${Math.trunc(t * 360)},
						${Math.min(100, 1000 * u)}%,
						${Math.min(50, 500 * u)}%
					);`
			}
		};
	}
</script>

{#each questions as question, index}
    {#if index === curQuestion}
        <div in:fly={{ duration: 600, x: 70 }} out:fly={{ duration: 600, x: -70 }} style="position: absolute;">
            <QuestionPanel
                question={question.q}
                rightAnswer={question.a[0]}
                wrongAnswers={question.a.slice(1)}
                answeredCallback={(correct: boolean) => {
                    if (correct) {
                        score++;
                    }
                    curQuestion++;
                }}
            />
        </div>
    {/if}
{/each}

{#if curQuestion >= questions.length}
    <div transition:overlyDramaticTransition={{ duration: 10000 }} style="position: absolute;">
        <h2>Quiz Completed!</h2>
        <p>Your score: {score}/{questions.length}</p>
    </div>
{/if}

