# coffee-vote — Голосование ПЧК

Форма голосования за концепцию упаковки ароматизированного кофе.

## Ссылка (после активации)
`https://andmanuylov-ftc.github.io/coffee-vote`

---

## Шаг 1 — Включить GitHub Pages

1. Открой репозиторий → **Settings** → **Pages**
2. Source: **Deploy from a branch**
3. Branch: **main** / **root** → **Save**

Через 1–2 минуты появится рабочая ссылка.

---

## Шаг 2 — Настроить Supabase (сохранение голосов)

1. Зайди на [supabase.com](https://supabase.com) → новый проект
2. **SQL Editor** → выполни:

```sql
create table votes (
  id uuid default gen_random_uuid() primary key,
  concept_id int not null,
  voter_name text,
  comment text,
  created_at timestamptz default now()
);
alter table votes enable row level security;
create policy "insert" on votes for insert with check (true);
create policy "select" on votes for select using (true);
```

3. **Settings → API** → скопируй:
   - **Project URL** → вставь в `index.html` вместо `YOUR_SUPABASE_URL`
   - **anon public key** → вместо `YOUR_SUPABASE_ANON_KEY`

---

## Шаг 3 — Добавить файлы дизайнов

1. Загрузи файлы в папки `designs/concept1/`, `designs/concept2/`, `designs/concept3/`
2. В `index.html` в блоке `CONCEPTS` укажи пути к файлам:

```js
files: [
  'designs/concept1/page1.jpg',
  'designs/concept1/page2.pdf',
]
```

Поддерживаемые форматы: JPG, PNG, PDF, PPTX, DOCX и любые другие.
PDF отображается как миниатюра первой страницы.
Несколько файлов листаются стрелками внутри карточки.

---

## Просмотр результатов

- Кнопка **«Показать результаты»** на странице голосования
- Полный список: Supabase → **Table Editor → votes**
