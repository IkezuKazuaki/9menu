# 9menu 

Webでメニュー管理する何かを作ってます。  
Next.js + Supabaseで構成中。

##Tech Stack

- **Next.js**
- **Supabase**
- **TypeScript**
- **Tailwind CSS** 
- **Node.js v22.14.0**

## 🚀 Getting Started

```bash
git clone https://github.com/IkezuKazuaki/9menu.git
cd frontend
npm install
npm run dev

## 🧱 Database Schema（2025年4月版）

### 👤 users
| column       | type     | description                           |
|--------------|----------|---------------------------------------|
| id           | uuid     | AuthユーザーID（auth.usersと連携）      |
| username     | text     | 表示名                                 |
| created_at   | timestamp | 登録日時                              |
| updated_at   | timestamp | 更新日時                              |
| deleted_at   | timestamp | 論理削除用                            |

---

### 🍜 restaurants
| column       | type     | description                              |
|--------------|----------|------------------------------------------|
| id           | serial   | 主キー                                   |
| name         | text     | 店名                                     |
| location     | text     | 建物・エリア詳細                          |
| description  | text     | 説明文                                   |
| category     | text     | ジャンル（ラーメン・カフェなど）           |
| zone         | text     | `center` / `west` / `east` のどれか      |
| created_at   | timestamp | 作成日時                                |
| updated_at   | timestamp | 更新日時                                |
| deleted_at   | timestamp | 論理削除用                              |

---

### 🕒 hours（通常営業時間）
| column       | type     | description                       |
|--------------|----------|-----------------------------------|
| id           | serial   | 主キー                            |
| restaurant_id| int      | 店ID（restaurants.id）            |
| day_of_week  | int      | 0=日曜, 1=月曜, ... 6=土曜        |
| open_time    | time     | 開店時間                          |
| close_time   | time     | 閉店時間                          |
| note         | text     | 備考                              |
| created_at   | timestamp |                                  |
| updated_at   | timestamp |                                  |
| deleted_at   | timestamp |                                  |

---

### 📅 special_hours（特別営業時間）
| column       | type     | description                                |
|--------------|----------|--------------------------------------------|
| id           | serial   | 主キー                                      |
| restaurant_id| int      | 店ID（restaurants.id）                      |
| date         | date     | 特定の日付                                  |
| open_time    | time     | 開店時間（なければnull）                     |
| close_time   | time     | 閉店時間（なければnull）                     |
| is_closed    | boolean  | 臨時休業かどうか                             |
| note         | text     | 備考（例：監視員不在）                        |
| created_at   | timestamp |                                            |
| updated_at   | timestamp |                                            |
| deleted_at   | timestamp |                                            |

---

### 💬 comments
| column       | type     | description                            |
|--------------|----------|----------------------------------------|
| id           | serial   | 主キー                                  |
| restaurant_id| int      | 店ID（restaurants.id）                  |
| user_id      | uuid     | ユーザーID（users.id）                   |
| content      | text     | コメント内容                             |
| rating       | int      | 評価（1〜5）                             |
| created_at   | timestamp |                                        |
| updated_at   | timestamp |                                        |
| deleted_at   | timestamp |                                        |

---

### 💡 共通事項
- 全テーブルで `deleted_at` に値が入っていれば論理削除された扱い

