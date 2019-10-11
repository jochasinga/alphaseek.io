# alphaseek.io

Developer-friendly, light-weight, customizable cloud referral engine.

## What it is

Referral programs out there are too complex for non-marketers and founders

They charge expensive fees, include too much, and gear toward full-fledged marketing package only company's marketing with budget can get behind. **It scares most people away thinking it's too early to start a referral campaign**.

### But...

launching a landing page is a pivotal moment. Getting users excited and sharing your page shouldn't be too early, too complex and too expensive. It's very important to detect your [early adopters](https://www.interaction-design.org/literature/article/understanding-early-adopters-and-customer-adoption-patterns) who are willing to advocate for your product.

I've been there, that's why I wrote my own referral engine, and I'd like to share with you.

## What is Alphaseek?
**Alphaseek** is a simple yet reliable backend service that does exactly these:

- Create referral links for your users to share
- Track how users refer/invite friends to join/subscribe to your product.
- Keep track of a generic simple point system that's easy for founders and developers to understand.

## Is it for you?

If you are one or more of the following:

- Know a bit of HTML/JS
- Have a developer who knows HTML/JS
- Already have a signup form on a landing page
- Want to create incentive for your users to invite other users
to sign up and use your product

All it takes is a few lines of code added to your page.

**Interested? Scroll down or share this with your developer!**

## How to use

[Contact us](+13476092126) or [leave your contact here](https://alphaseek.typeform.com/to/kBUVWb).

Once you have retrieved your access token for your product from us, you can start making calls to our API.

Here is how you can send a request to our API in JavaScript:

### Creating a referring link

```javascript

// For example only, don't use this.
const accessToken = '1e6acc57-95f4-4928-997a-32f0571cc933'
const productId = 'awesomeapp-1234'

async function getAlphaseekUrlFor(userEmail) {
  const res = await fetch(`https://api.alphaseek.io/v0/${productId}/users`, {
    method: 'POST',
    headers: new Headers({
      'Authorization': 'Bearer ' + accessToken,
      'Content-Type': 'application/json'
    }),
    body: JSON.stringify({
      // Your user's email. This is required.
      email: userEmail,
      // Where you want the referral link to bring the referred user to.
      redirectTo: 'https://yourawesomeapp.com/signup',
    }),
  });

  res.then((res) {
    return res.json();
  }).catch((err) {
    log.error(err);
  });
}

```

If you're using React, then you'll likely place this function call in a method of the signup form component:

```javascript

class SignupForm extends React.Component {
  // ...
  state = {
    email: '',
  };

  onFormSubmit() {

    // Save your user to your database.

    // Call to get your user his/her referral link.
    const data = getAlphaseekUrlfor(this.state.email);
    // You get a url like 'https://alphaseek.io/invite/32e0542'
    window.alert(`Thank you for signing up, here is your link to invite friends: ${data.url}`);
  }

  handleEmail = (e: any) => {
    this.setState({
      email: e.target.value,
    });
  }

  render() {
    return (
      <div>
        <form action="" onSubmit={this.onFormSubmit}>
          <input
            type="email"
            placeholder="Your email"
            onChange={this.handleEmail}
            value={this.state.email}
          />
        </form>
      </div>
    );
  }
}

```

### Getting user data

To get user's referral data:

```javascript

async function getUser(userEmail) {
  const res = await fetch(`https://api.alphaseek.io/v0/${productId}/users/${userEmail}`, {
    method: 'GET',
    headers: new Headers({
      'Authorization': 'Bearer ' + accessToken,
      'Content-Type': 'application/json'
    }),
  });

  res.then((res) {
    return res.json();
  }).catch((err) {
    log.error(err);
  });
}

```

Here is a JSON data you will get:

```json

{
  data: {
    user: {
      email: "janedoe@gmail.com",
      referredBy: "mikhaela@gmail.com",
      referredTo: ["johndoe@gmail.com", "elonmusk@space.x"],
      points: 2
    }
  }
}

```

You can also request users sorted based on points:

```javascript

async function getFirstTenUsers() {
  const res = await fetch(`https://api.alphaseek.io/v0/${productId}/users?page_size=10&sort=desc`, {
    method: 'GET',
    headers: new Headers({
      'Authorization': 'Bearer ' + accessToken,
      'Content-Type': 'application/json'
    }),
  });
  res.then((res) {
    return res.json();
  }).catch((err) {
    log.error(err);
  });
}

```

### Announce your invitation campaign

Now this is where the fun begins as you start thinking about your offering strategy to provide incentives to users to cross the friction gap to sign up and use your product. It could be a secretive invite-only beta access if you have a [VIP product](https://superhuman.com/) or some credit offering if you have a [social product](https://help.uber.com/partners/article/referring-drivers-and-riders?nodeId=03db9e2b-270b-4fdb-95a7-afce7c6b4b3b).

## Don't waste time writing referral logic that's not core to your business

We did that when we were building other thing and it took us a lot of time out of what mattered.

Now we can take care of that so you won't repeat that mistake and just focus on the what's important--getting users and validating ideas.

## [Sign up](https://alphaseek.typeform.com/to/kBUVWb) or [contact us](+13476092126) to set up.