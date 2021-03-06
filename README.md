# supabase-workers 👷

This codebase is a proof-of-concept for making API requests to [Supabase](https://supabase.com) inside of a [Cloudflare Workers](https://workers.cloudflare.com) serverless function.

Supabase's [JavaScript client](https://github.com/supabase/supabase-js) doesn't work directly in Workers without using Webpack's `externals` feature to replace `cross-fetch` with the native `fetch` API in Workers, as seen [here](https://github.com/signalnerve/supabase-workers-proxy/blob/main/webpack.config.js).

You can see an example of this API at `https://supabase-workers.riteshpuvvada.workers.dev`:

- `https://supabase-workers.riteshpuvvada.workers.dev/users`: select all users
- `https://supabase-workers.riteshpuvvada.workers.dev/users/:id`: query for a user by id
- `https://supabase-workers.riteshpuvvada.workers.dev/*`: all other requests are redirected to this GitHub project

To deploy your own version, clone or fork the project, replace the `account_id` value in `wrangler.toml` with your own, and then set two secrets using `wrangler secret put`:

- `SUPABASE_API_KEY`: anon/public key available in your Supabase project's "API settings"
- `SUPABASE_URL`: RESTful endpoint URL available in your Supabase project's "API settings"

This project is built on TypeScript using [`itty-router`](https://itty-router.dev) and could easily be extended to provide a RESTful interface to your Supabase data, without needing to expose any API credentials.
