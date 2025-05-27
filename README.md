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
   ```json
   - "version": "0.0.2"
   + "version": "0.0.3"
   ```

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
   
