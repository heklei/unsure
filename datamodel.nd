

---

# 📊 LoreQuest: Data Model

---

## 🧑 User

| Field            | Type                                 | Description                     |
| ---------------- | ------------------------------------ | ------------------------------- |
| user\_id         | UUID (PK)                            | Unique identifier               |
| email            | String                               | User email (login credential)   |
| username         | String                               | Public-facing handle            |
| display\_name    | String                               | Optional name                   |
| avatar\_url      | String                               | URL of avatar image             |
| created\_at      | DateTime                             | Account creation date           |
| privacy\_setting | Enum (public, friends-only, private) | Default lore visibility         |
| xp               | Integer                              | User experience points          |
| level            | Integer                              | Calculated from XP              |
| bio              | Text                                 | Personal description/lore blurb |

---

## 🧙 Character

| Field                 | Type      | Description                                      |
| --------------------- | --------- | ------------------------------------------------ |
| character\_id         | UUID (PK) | Unique identifier                                |
| user\_id              | UUID (FK) | Belongs to user                                  |
| class                 | String    | User-defined or from presets (e.g., Bard, Rogue) |
| alignment             | Enum      | RPG-style morality system                        |
| backstory             | Text      | Custom character bio                             |
| avatar\_customization | JSON      | Stores look details (hair, color, clothes, etc.) |

---

## 📖 Lore\_Entry

| Field      | Type           | Description                           |
| ---------- | -------------- | ------------------------------------- |
| lore\_id   | UUID (PK)      | Unique lore item                      |
| user\_id   | UUID (FK)      | Creator                               |
| title      | String         | Title of entry                        |
| content    | Text           | Rich-text content                     |
| lore\_type | Enum           | (Quest, Memory, Boss, Artifact, etc.) |
| difficulty | Enum           | (Easy, Normal, Hard, Legendary)       |
| media\_url | String         | Optional attachment                   |
| tags       | Array\[String] | User-defined or system tags           |
| timestamp  | DateTime       | Event time or creation date           |
| visibility | Enum           | public, friends-only, private         |

---

## 🧩 Quest\_Participation

| Field                    | Type                | Description                                    |
| ------------------------ | ------------------- | ---------------------------------------------- |
| quest\_participation\_id | UUID (PK)           | Unique participation ID                        |
| lore\_id                 | UUID (FK)           | Tied to a quest lore entry                     |
| participant\_id          | UUID (FK: user\_id) | Friend or self                                 |
| role                     | Enum                | (Main, Ally, Mentor, Rival)                    |
| status                   | Enum                | (Active, Completed, Abandoned)                 |
| xp\_awarded              | Integer             | XP given on completion                         |
| contribution             | Text                | Optional user notes on their part in the quest |

---

## 🏆 Achievement

| Field           | Type      | Description                                     |
| --------------- | --------- | ----------------------------------------------- |
| achievement\_id | UUID (PK) | Unique achievement                              |
| user\_id        | UUID (FK) | Earner                                          |
| title           | String    | Title (e.g., "Defeated Procrastination Dragon") |
| description     | Text      | Flavor text                                     |
| badge\_icon     | String    | Path to badge image                             |
| date\_earned    | DateTime  | When earned                                     |

---

## 🤝 Friendship

| Field               | Type      | Description                        |
| ------------------- | --------- | ---------------------------------- |
| friendship\_id      | UUID (PK) | Unique relationship                |
| user\_a\_id         | UUID (FK) | One side of friendship             |
| user\_b\_id         | UUID (FK) | The other user                     |
| status              | Enum      | (pending, accepted, blocked)       |
| relationship\_type  | Enum      | (Party Member, Rival, NPC, Mentor) |
| friendship\_started | DateTime  | When accepted                      |

---

## 💬 Message\_Thread

| Field        | Type         | Description                  |
| ------------ | ------------ | ---------------------------- |
| thread\_id   | UUID (PK)    | Chat thread                  |
| user\_ids    | Array\[UUID] | Participants                 |
| thread\_type | Enum         | (Private, Group, Party Chat) |
| created\_at  | DateTime     | Start date                   |

## 💬 Message

| Field       | Type                | Description   |
| ----------- | ------------------- | ------------- |
| message\_id | UUID (PK)           | Unique ID     |
| thread\_id  | UUID (FK)           | Thread parent |
| sender\_id  | UUID (FK: user\_id) | Sender        |
| content     | Text                | Message body  |
| timestamp   | DateTime            | Sent time     |

---

## 📅 Timeline\_View

| Field            | Type         | Description                          |
| ---------------- | ------------ | ------------------------------------ |
| view\_id         | UUID (PK)    | Unique view session                  |
| user\_id         | UUID (FK)    | Viewer                               |
| target\_user\_id | UUID (FK)    | Whose timeline is being viewed       |
| start\_date      | DateTime     | Optional filter                      |
| end\_date        | DateTime     | Optional filter                      |
| synced\_with     | Array\[UUID] | Friends included in timeline overlay |

---

## 🛡 Reputation

| Field            | Type      | Description                                    |
| ---------------- | --------- | ---------------------------------------------- |
| rep\_id          | UUID (PK) | Unique record                                  |
| source\_user\_id | UUID (FK) | Who gave the rep                               |
| target\_user\_id | UUID (FK) | Who received it                                |
| rep\_type        | Enum      | (Loyalty, Chaos, Wisdom, Inspiration, Support) |
| value            | Integer   | +1 to +10 scale                                |
| comment          | Text      | Optional                                       |
| date             | DateTime  | Given when                                     |

---

## 📲 Notification

| Field            | Type      | Description                                                   |
| ---------------- | --------- | ------------------------------------------------------------- |
| notification\_id | UUID (PK) | Unique                                                        |
| user\_id         | UUID (FK) | Recipient                                                     |
| type             | Enum      | (Friend\_Request, Lore\_Tagged, XP\_Awarded, Event\_Reminder) |
| message          | Text      | Notification body                                             |
| is\_read         | Boolean   | Read status                                                   |
| timestamp        | DateTime  | Created at                                                    |

---

## 📦 Draft\_Lore

| Field          | Type      | Description            |
| -------------- | --------- | ---------------------- |
| draft\_id      | UUID (PK) | Unique ID              |
| user\_id       | UUID (FK) | Owner                  |
| draft\_data    | JSON      | Saved lore in progress |
| last\_modified | DateTime  | Timestamp of save      |

---

## ERD (Entity Relationship Summary)

* `User` ↔ 1\:N ↔ `Character`
* `User` ↔ 1\:N ↔ `Lore_Entry`
* `Lore_Entry` ↔ N\:M ↔ `User` via `Quest_Participation`
* `User` ↔ N\:M ↔ `User` via `Friendship`
* `User` ↔ 1\:N ↔ `Achievement`
* `User` ↔ N\:M ↔ `Message_Thread` ↔ 1\:N ↔ `Message`
* `User` ↔ N\:M ↔ `User` via `Reputation`
* `User` ↔ 1\:N ↔ `Notification`
* `User` ↔ 1\:N ↔ `Draft_Lore`

---


