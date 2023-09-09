import { Selector } from 'testcafe';

fixture`Login Test`
    .page`https://dtthon.deepthought.education/login?share_redirect=true&url=/dtthon/applicant/dashboard`; // Replace with your actual login page URL

test('Login with valid credentials', async t => {
    // Selectors for login form elements
    const usernameInput = Selector('#username');
    const passwordInput = Selector('#password');
    const loginButton = Selector('button[type="submit"]');

    // Test data (replace with actual test data)
    const username = 'your-username';
    const password = 'your-password';

    // Fill in the login form and submit
    await t
        .typeText(usernameInput, username)
        .typeText(passwordInput, password)
        .click(loginButton);

    // Assertions - Replace with your actual success page URL or element selectors
    const successPageUrl = 'https://your-application-url.com/dashboard'; // Replace with your actual success page URL
    await t.expect(Selector('body').innerText).contains('Welcome to Dashboard');
    await t.expect(t.eval(() => window.location.href)).eql(successPageUrl);
});

test('Login with invalid credentials', async t => {
    // Selectors for login form elements
    const usernameInput = Selector('#username/email');
    const passwordInput = Selector('#password');
    const loginButton = Selector('button[type="submit"]');

    // Test data for invalid login (replace with incorrect credentials)
    const invalidUsername = 'invalid-username';
    const invalidPassword = 'invalid-password';

    // Fill in the login form with invalid credentials and submit
    await t
        .typeText(usernameInput, invalidUsername)
        .typeText(passwordInput, invalidPassword)
        .click(loginButton);

    // Assertions for error message - Replace with your actual error message or element selector
    await t.expect(Selector('.error-message').innerText).contains('Invalid username or password');
});
