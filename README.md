# Crate Ideas

## `rover` / `derive-http-client`
Proc macros for behavior-driven HTTP client generation. There is no winning "Http client" pattern in the rust community, and I could see something like [refit] being really cool for the rust ecosystem.

for example, if there was a REST API `https://dominos.com/api` with `GET, PATCH, POST, PUT` on `/users` this may look like:

```rust
#[rover(json, route = "users")]
pub trait DominosApiUsers {
  #[rover(GET)]
  fn get_users(&self) -> Result<Vec<User>, RoverError>;

  #[rover(GET, route = "{id}")]
  fn get_user(&self, id: String) -> Result<Option<User>, RoverError>;

  #[rover(POST, body = user)]
  fn create_user(&self, user: User) -> Result<User, RoverError>;

  #[rover(PATCH, body = user_patch)]
  fn update_user(&self, user_patch: UserPatch) -> Result<User, RoverError>;
}

#[rover(impl = DominosApiUsers)]
pub struct DominosApi {
  #[rover(base_url)]
  base_url: String,
}
```

[refit]: https://github.com/reactiveui/refit
