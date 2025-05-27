## Публикация и установка npm-пакета через Artifactory (MTS)

### Публикация изменений в npm-пакет

1. **Запушить свои изменения в тестовую ветку:**
   ```bash
   git checkout -b feature/your-feature
   git add .
   git commit -m "feat: описание изменений"
   git push origin feature/your-feature
   ```

2. **Настройка `.npmrc`:**

   Перейдите по ссылке:  
   [https://artifactory.mts.ru/ui/repos/tree/General/npm-auto-p-npm-local](https://artifactory.mts.ru/ui/repos/tree/General/npm-auto-p-npm-local)

   Затем выполните:
   - Нажмите на иконку профиля в правом верхнем углу.
   - Выберите `Set Me Up`.
   - Выберите менеджер пакетов `npm`.
   - В списке репозиториев выберите `npm-auto-p-npm-local`.
   - Нажмите `Generate Token & Create Instructions`.
   - Скопируйте **authToken** из самого первого блока.

   Добавьте в `.npmrc` ваши данные:

   ```ini
   @tabs:registry=https://artifactory.mts.ru/artifactory/api/npm/npm-auto-p-npm-local/
   //artifactory.mts.ru/artifactory/api/npm/npm-auto-p-npm-local/:_authToken=ВАШ_ТОКЕН
   //artifactory.mts.ru/artifactory/api/npm/npm-auto-p-npm-local/:email=ВАША_ПОЧТА
   //artifactory.mts.ru/artifactory/api/npm/npm-auto-p-npm-local/:always-auth=true
   strict-ssl=false
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

4. **Опубликуйте пакет:**
   ```bash
   npm publish
   ```

---

### Установка пакета в другом репозитории

1. **Добавьте в `.npmrc` следующую строку:**

   ```ini
   @tabs:registry=https://artifactory.mts.ru/artifactory/api/npm/npm-auto-p-npm-local/
   ```

2. **Установите пакет через терминал:**

   ```bash
   npm install @tabs/ui-kit-lib
   
