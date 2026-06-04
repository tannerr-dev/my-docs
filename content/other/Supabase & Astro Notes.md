
[[supabase]]
[[astro]]


---
I cannot seem to figure out how to have the OTP/magic link  log in the user, it always redirects out. 

ive done this, and this part (simple auth) works fine:
[astro supabase docs](https://docs.astro.build/en/guides/backend/supabase/)

i cannot get the magic link to log me in though...

ive done this
[supabase ssr docs](https://supabase.com/docs/guides/auth/server-side/creating-a-client?queryGroups=framework&framework=astro&queryGroups=environment&environment=astro-server)


for this ([magic link docs](https://supabase.com/docs/guides/auth/auth-email-passwordless?queryGroups=language&language=js)):
- ive changed the email emplate and created an `auth/comfirm` endpoint
- where does the function code go?

function i do not know where to put...
```js
async function signInWithEmail() {
  const { data, error } = await supabase.auth.signInWithOtp({
    email: 'valid.email@supabase.io',
    options: {
      // set this to false if you do not want the user to be automatically signed up
      shouldCreateUser: false,
      emailRedirectTo: 'https://example.com/welcome',
    },
  })
}
//where do i put this? is this implicit flow only?
```



endpoint:
```js
import { supabase } from "../../../lib/supabase.ts";
export async function GET({url, redirect}){
  let token_hash = url.searchParams.get('token_hash');
  let type = url.searchParams.get('type');
  console.log(token_hash, type);
  const { error } = await supabase.auth.verifyOtp({ token_hash, type })
  console.log(error);
  return redirect('/dashboard')
}
```

../lib/supabase.ts
```js
```

trying this [pkce flow](https://supabase.com/docs/guides/auth/sessions/pkce-flow)
- where do i put this?
- what type of localstorage do i need?
```js
const customStorageAdapter: SupportedStorage = {
    getItem: (key) => {
    if (!supportsLocalStorage()) {
        // Configure alternate storage
        return null
    }
    return globalThis.localStorage.getItem(key)
    },
    setItem: (key, value) => {
    if (!supportsLocalStorage()) {
        // Configure alternate storage here
        return
    }
    globalThis.localStorage.setItem(key, value)
    },
    removeItem: (key) => {
    if (!supportsLocalStorage()) {
        // Configure alternate storage here
        return
    }
    globalThis.localStorage.removeItem(key)
    },
}

```


ok i switched the client creation to the ssr code but i also used the code from the endpoint becaue i was getting an error because of the Astro 
- still didn't work, throwing errors

i feel like tthis is getting closer, using context to access the url.params but now the redirect  isn't defined.. how do i define it?


im so close, i just need to set the cookies right and then we are good...
not sure how to set up the storage adapter


## Success

manually setting the cookie worked outside of the storage config,
also need to set the cookie config with path etc

### testing
- cookie config must me initialized when creating supabaseServerClient
- 