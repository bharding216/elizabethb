<svelte:head>
	<title>Inquire</title>
	<meta name="description" content="Contact us" />
</svelte:head>

<script>
    let formData = {
        name: '',
        email: '',
        message: '',
        phone: '',
        city: '',
        projectType: '',
        projectBudget: '',
        panda: ''
    };

    let confirmationMessage = '';

    async function handleSubmit(event) {
        event.preventDefault();

        if (formData.panda.toLowerCase() !== 'white') {
            console.log("Answer was not white")
            return;
        }

        const form = new FormData(event.target);

        let name = form.get('name');
        let email = form.get('email');
        let message = form.get('message');

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
            window.scrollTo({
                top: 0,
                behavior: 'smooth'
            });
        } else {
            confirmationMessage = 'Error sending email';
            console.error('Error sending email');
        }
    }
</script>

<div>
    <h1 class="pb-4">Let's Design Your Dream Space Together</h1>

    {#if confirmationMessage}
        <p class="confirmation">{confirmationMessage}</p>
    {/if}

    <form on:submit={handleSubmit}>
        <div class="form-floating mb-3 col-md-12 col-lg-6">
            <input type="text" class="form-control" bind:value={formData.name} id="name" name="name"
                placeholder="Name" autocomplete="off" required>
            <label for="name">Name *</label>
        </div>

        <div class="form-floating mb-3 col-md-12 col-lg-6">
            <input type="email" class="form-control" bind:value={formData.email} id="email" name="email"
                placeholder="Email" autocomplete="off" required>
            <label for="email">Email *</label>
        </div>

        <div class="form-floating mb-3 col-md-12 col-lg-6">
            <input type="phone" class="form-control" bind:value={formData.phone} id="phone" name="phone"
                placeholder="Phone" autocomplete="off" required>
            <label for="phone">Phone *</label>
            </div>
        
            <div class="form-floating mb-3 col-md-12 col-lg-6">
            <input type="text" class="form-control" bind:value={formData.city} id="city" name="city"
                placeholder="City" autocomplete="off">
            <label for="city">City</label>
            </div>

            <div class="form-floating mb-3 col-md-12 col-lg-6">
            <label for="projectType" style="display: none;">Project Type</label>
            <select bind:value={formData.projectType} id="projectType" name="projectType" class="form-select" style="padding-top: 10px;">
                <option value="" disabled>Select Project Type</option>
                <option value="new-construction">New Construction</option>
                <option value="renovation">Renovation</option>
            </select>
            </div>
        
        <p>Project budget:</p>
        <div class="form-check mb-3 col-md-12">
            <div>
                <input type="radio" class="form-check-input" id="low_budget" name="projectBudget" value="50" bind:group={formData.projectBudget}>
                <label class="form-check-label" for="low_budget">&lt;$50k</label>
            </div>
            
            <div>
                <input type="radio" class="form-check-input" id="med_budget" name="projectBudget" value="50_to_150" bind:group={formData.projectBudget}>
                <label class="form-check-label" for="med_budget">$50k - $150k</label>
            </div>
            
            <div>
                <input type="radio" class="form-check-input" id="high_budget" name="projectBudget" value="150" bind:group={formData.projectBudget}>
                <label class="form-check-label" for="high_budget">$150k+</label>
            </div>
        </div>

        <div class="form-floating mb-3 col-md-12 col-lg-6">
            <textarea class="form-control" bind:value={formData.message} id="message" name="message"
                placeholder="Message" style="height: 100px;"></textarea>
            <label for="message">Message</label>
        </div>   

        <p class="m-0 pb-1" style="color: #808080; font-size: 14px;">To verify you're a human:</p>
        <div class="form-floating mb-3 col-md-12 col-lg-6">
            <input type="text" class="form-control" bind:value={formData.panda} id="panda" name="panda"
                placeholder="Pandas are black and:" required>
            <label for="panda">Pandas are black and:</label>
        </div>
    
        <button type="submit" class="btn btn-secondary">Submit</button>

    </form>
</div>


<style>
    .confirmation {
        color: rgb(0, 0, 184)
    }
</style>