# prisma-kysely

> 🚧 **Library and README in progress...**

Do you like Prisma's migration flow, schema language and DX but not the limitations of the Prisma Client? Do you want to harness the raw power of SQL without losing the safety of the TypeScript type system? **Enter `prisma-kysely`**!

### Setup

1. Install `prisma-kysely` using your package manager of choice:

   ```sh
   yarn add prisma-kysely
   ```

2. Replace the default client generator in your `schema.prisma` file with the following:

   ```prisma
   generator kysely {
       provider = "prisma-kysely"

       // Optionally provide a destination directory for the generated file
       // and a filename of your choice
       output = "../src/db"
       fileName = "types.ts"
   }
   ```

### Motivation

`prisma-kysely` is meant as a more convenient alternative to `kysely-codegen` for those that use Prisma only for migrations. The package makes sure that Kysely's types are always up to date with the latest database schema. `prisma-kysely` also has better support for enums than `kysely-codegen` does. The author has used Prisma Migrate and Kysely together with Postgres and Cloudflare's D1 daily for a few months now and is really happy with the combo, but this has been the missing piece needed to make workflow super smooth.

### Config

| Key                      | Description                                                                                                                                                                                                                                                                                                                                                                         |
| ------------------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `output`                 | The directory where generated code will be saved                                                                                                                                                                                                                                                                                                                                    |
| `fileName`               | The filename for the generated file                                                                                                                                                                                                                                                                                                                                                 |
| `[typename]TypeOverride` | Allows you to override the resulting TypeScript type for any Prisma type. Useful when targeting a different environment than Node (e.g. WinterCG compatible runtimes that use UInt8Arrays instead of Buffers for binary types etc.) Check out the [config validator](https://github.com/valtyr/prisma-kysely/blob/main/src/utils/validateConfig.ts) for a complete list of options. |

### Contributions

OMG you actually want to contribute? I'm so thankful! Development is super easy.

1. Fork and pull the repository
2. Run `yarn install` and `yarn dev` to start `tsc` in watch mode.
3. Make changes to the source code
4. Test your changes by editing `prisma/schema.prisma`, running `yarn prisma generate` and checking the output in `prisma/types.ts`.
5. Create a pull request! If your changes make sense, I'll try my best to review and merge them quickly.

I'm not 100% sure the [type maps](https://github.com/valtyr/prisma-kysely/blob/main/src/helpers/generateFieldType.ts) are correct for every dialect, so any and all contributions on that front would be greatly appreciated. The same goes for any bug you come across or improvement you can think of.

```diff
+ 🥹 Make Codd proud!
```
