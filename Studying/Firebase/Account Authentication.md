
---
# On Button Click
As soon as the "Continue with Email" button has been clicked it validates the email. If the email is valid then it submits the email to `/api/auth/continue-email` API endpoint and the response is either if onboarding is true or false. If the onboarding is true then it proceeds to "Getting user info onboarding pages" which changes the page states, otherwise  `pageState = 'confirm'`  followed by `authHandler.continueWithEmail(result.data.email);` which handles the authentication methods.

```typescript
onclick={async () => {
	continueWithEmailLoading = true;
	const EmailSchema = z.object({ email: z.email({ message: 'Invalid email address' }) .min(1, { message: 'Email is required' }) });
	// Validate email
	const result: ZodSafeParseResult<{ email: string }> = EmailSchema.safeParse({ email: email });

	// If email is valid
	if (result.success) {
		// Submits the email to the API endpoint and retrieves a response
		const response = await fetch('/api/auth/continue-email', {
			method: 'POST',
			headers: {
				'Content-Type': 'application/json'
			},
			body: JSON.stringify({ email })
		});

		// Use the response to check if onboarding is true or false
		// This is done to check if the user is new or exists.
		const data = await response.json();
		if (data.onboarding) {
			// Changes page state to continue getting basic info from the user in the onboarding state
			pageState = 'boardProfileType';
		} else {
			pageState = 'confirm';
			// Calls the firebase `continueWithEmail` function
			authHandler.continueWithEmail(result.data.email);
		}

		continueWithEmailLoading = false;
	} else {
		emailError = result.error;
		continueWithEmailLoading = false;
	}
}}
```

