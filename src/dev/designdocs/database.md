# Database
## Schema

> [!NOTE]  
> `!foo` = primary key  
> `<foo>` = foreign key  
> `[foo]` = optional (nullable) field

- **Jokes**
  - `!id`: string - UUID
  - `type`: string - enum ["single", "multipart"]
  - `text`: string[]
  - `categories`: string[] - enum (TODO / see categories.json)
  - `flags`: string[] - enum (TODO / see flags.json)
  - `locale`: string - enum (TODO / see languages.json and countries.json)
  - `<author>`: string - UUID
  - `created_at`: timestamp
  - `accepted_at`: timestamp
  - `[updated_at]`: timestamp
  - `[deleted_at]`: timestamp
- **Submissions**
  - `!id`: string - UUID
  - `status`: string - enum ["pending", "accepted", "rejected"]
  - `type`: string - enum ["single", "multipart"]
  - `text`: string[]
  - `categories`: string[] - enum (TODO / see categories.json)
  - `flags`: string[] - enum (TODO / see flags.json)
  - `locale`: string - enum (TODO / see languages.json and countries.json)
  - `<author>`: string - UUID
  - `[<recreation_of>]`: string - UUID
  - `created_at`: timestamp
  - `[updated_at]`: timestamp
  - `[deleted_at]`: timestamp
- **Users**
  - `!id`: string - UUID
  - `username`: string
  - `email`: string - unique
  - `created_at`: timestamp
  - `[updated_at]`: timestamp
  - `[deleted_at]`: timestamp
  - `tier`: string - enum ["free", "pro", "enterprise"]
  - `roles`: string[] - enum ["user", "moderator", "admin"]
  - `<settings>`: string - UUID
  - `[<billing>]`: string - UUID
  - `<connections>`: string[] - UUIDs
- **User settings**
  - `!id`: string - UUID
  - `notifications`: object
    - `important_info`: boolean
    - `api_updates`: boolean
    - `submission_updates`: boolean
- **Billing info**
  - `!id`: string - UUID
  - `type`: string - enum ["stripe", "paypal"]
  - `billing_data`: TODO
  - `cycle`: string - enum ["monthly", "yearly"]
  - `next_billed_at`: timestamp
  - `<invoices_id>`: string[] - UUIDs
- **Invoices**
  - `!id`: string - UUID
  - `amount`: number
  - `paid_at`: timestamp
- **(OAuth) Connections**
  - `!id`: string - UUID
  - `provider`: string - enum ["github", "google", "discord"]
  - `connection_data`: TODO
- **Reports**
  - `!id`: string - UUID
  - `type`: string - enum ["joke", "submission", "user"]
  - `reason`: string
  - `<author>`: string - UUID
  - `<notes>`: string[] - UUIDs
  - `created_at`: timestamp
  - `[updated_at]`: timestamp
  - `[deleted_at]`: timestamp
- **Notes**
  - `!id`: string - UUID
  - `text`: string
  - `<author>`: string - UUID
  - `created_at`: timestamp
  - `[updated_at]`: timestamp
  - `[deleted_at]`: timestamp