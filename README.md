
## Публикация и установка npm-пакета через GITRAILS (MTS)

> 🔗 **Доступ к пакетам**:  
> [https://gitlab.services.mts.ru/tabs/tabs-ui-kit/-/packages](https://gitlab.services.mts.ru/tabs/tabs-ui-kit/-/packages)

### Публикация изменений в npm-пакет

1. **Запушить свои изменения в тестовую ветку:**
   ```bash
   git checkout -b feature/your-feature
   git add .
   git commit -m "feat: описание изменений"
   git push origin feature/your-feature
   ```

2. **Настройка `.npmrc`:**

   Создайте свой персональный токен в gitlab:
   - Нажмите на иконку профиля в левом верхнем углу.
   - Выберите `Edit Profile`.
   - Выберите `Access Tokens`.
   - Создайте токен с названием `NPM_TOKEN` и галочкой - `api` (длительность токена на свое усмотрение).
   - Нажмите `Create Pesonal Access Token`.
   - Скопируйте получившийся токен и запомните его.

   Добавьте в `.npmrc` свой токен:

   ```ini
   @tabs:registry=https://gitlab.services.mts.ru/api/v4/projects/192337/packages/npm/
    //gitlab.services.mts.ru/api/v4/projects/192337/packages/npm/:_authToken="${NPM_TOKEN}"
   ```

3. **Обновите версию пакета вручную:**

   В файле `package.json` измените версию, например:
   ```diff
   - "version": "0.0.2"
   + "version": "0.0.3"
   ```
   ### Обновление версий UI Kit по стандарту SemVer

   Формат версий: `MAJOR.MINOR.PATCH` (z.y.x)
   
   | Компонент     | Когда увеличивается                                                                       | Пример            |
   |---------------|--------------------------------------------------------------------------------------------|-------------------|
   | **MAJOR (z)** | При внесении **несовместимых изменений** в UI Kit (удаление компонентов, изменение API) | `1.0.0` → `2.0.0` |
   | **MINOR (y)** | При **добавлении новых компонентов или фич**, совместимых с текущей реализацией         | `1.2.0` → `1.3.0` |
   | **PATCH (x)** | При **исправлении багов** или улучшениях, не затрагивающих публичный API                | `1.2.3` → `1.2.4` |
   
   Например:
   - Добавили новый компонент `Tabs` — увеличиваем `MINOR`
   - Переименовали проп `color` в `variant` — увеличиваем `MAJOR`
   - Пофиксили неправильный отступ у `Button` — увеличиваем `PATCH`

4. **Соберите проект перед публикацией:**
   ```bash
   npm run build
   ```

5. **Опубликуйте пакет:**
   ```bash
   npm publish
   ```

---

### Установка пакета в другом репозитории

1. **Добавьте в `.npmrc` следующую строку:**

   ```ini
   @tabs:registry=https://gitlab.services.mts.ru/api/v4/packages/npm/
   ```

2. **Установите пакет через терминал:**

   ```bash
   npm i @tabs/ui-kit-lib
   
