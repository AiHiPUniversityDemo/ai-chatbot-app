<script>
    let prompt = '';
    let aiResponse = '';

    async function handleSubmit(event) {
        event.preventDefault();
        aiResponse = "Loading...";
        try {
            const response = await fetch('https://ai-chatbot-app-server.onrender.com', {
                method: 'POST',
                headers: { 'Content-Type': 'application/json' },
                body: JSON.stringify({ prompt }),
            });
            let data = await response.json();
            aiResponse = data.ai;
        } catch (error) {
            console.error(error);
            aiResponse = "Error communicating with AI. Please try again later.";
        }
    }
</script>

<div>
    <form on:submit={handleSubmit}>
        <input bind:value={prompt} placeholder="Enter your prompt here" />
        <button type="submit">Submit</button>
    </form>
    <h2>User prompt: {prompt}</h2>
    <h2>AI response: {aiResponse}</h2>
</div>

    