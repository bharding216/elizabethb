<script>
    let name = '';
    let email = '';
    let message = '';
    let confirmationMessage = '';

    async function handleSubmit(event) {
        event.preventDefault();
        const formData = new FormData(event.target);
        name = formData.get('name');
        email = formData.get('email');
        message = formData.get('message');

        // http://127.0.0.1:3000/inquire
        const response = await fetch('https://2jealshrq3ogi6nfghzshfj5a40kdokp.lambda-url.us-east-2.on.aws/', {
            method: 'POST',
            headers: {
                'Content-Type': 'application/json',
            },
            body: JSON.stringify({
                name: name,
                email: email,
                message: message,
            }),
        });
        
        if (response.ok) {
            const responseData = await response.json();
            confirmationMessage = responseData.message;
        } else {
            confirmationMessage = 'Error sending email';
            console.error('Error sending email');
        }
    }
</script>

<div class=container>
    <div>
        <h1 class="pb-4">Let's Design Your Dream Space Together</h1>

        {#if confirmationMessage}
            <p>{confirmationMessage}</p>
        {/if}

        <form on:submit={handleSubmit}>
            <div class="form-floating mb-3 col-md-12 col-lg-6">
                <input type="text" class="form-control" id="name" name="name"
                    placeholder="Name" autocomplete="off" required>
                <label for="name">Name</label>
            </div>

            <div class="form-floating mb-3 col-md-12 col-lg-6">
                <input type="email" class="form-control" id="email" name="email"
                    placeholder="Email" autocomplete="off" required>
                <label for="email">Email</label>
            </div>

            <div class="form-floating mb-3 col-md-12 col-lg-6">
                <textarea class="form-control" id="message" name="message"
                    placeholder="Message" style="height: 100px;" required></textarea>
                <label for="message">Message</label>
            </div>   
            
            <div>
                <p>Other things to include:</p>
                <ul>
                    <li>Phone</li>
                    <li>City</li>
                    <li>Project type: (new construction or renovation)</li>
                    <li>Project budget: (under 50k, 50-100, 100+)</li>
                    <li>phone</li>
                </ul>
            </div>

            <button type="submit" class="btn btn-secondary">Submit</button>

        </form>
    </div>
</div>
