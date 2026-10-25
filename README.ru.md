# CanvasLink для Android

Управление окном CanvasTTY с телефона или планшета по локальной сети.

**Экспериментальная alpha · Android 8+**. Предыдущий прототип проверен пользователем
на Mac с Android-планшетом. Сборки Windows и Linux проходят CI; управление с
реального Android на этих системах ещё не принято.

[Скачать APK 0.3.0-alpha.1](https://github.com/teo-nex/CanvasLink/releases/tag/v0.3.0-alpha.1) · [English](README.md)

[Отчёт: проверка APK, восемь успешных заданий CI и оставшиеся ограничения](VERIFICATION.md).

Это репозиторий распространения APK и инструкций. Исходники находятся в
[CanvasTTY, PR #166](https://github.com/howdeploy/CanvasTTY/pull/166) и
[ветке автора интеграции](https://github.com/teo-nex/CanvasTTY/tree/feat/canvaslink-android-lan/integrations/canvaslink).
В официальный стабильный CanvasTTY интеграция **пока не включена**.

## Установка

Нужны Android 8+, USB-кабель с передачей данных и сборка CanvasTTY из PR #166,
в которой есть **Настройки → CanvasLink**. Если раздела нет, одна установка APK
не добавит поддержку на компьютере. Отдельное приложение CanvasLink для ПК не нужно.

1. На Android включите режим разработчика и **отладку по USB**, подключите кабель.
2. Разблокируйте Android и подтвердите RSA-запрос доверия этому компьютеру.
   Это действие выполняет владелец устройства.
3. Скопируйте [промпт установки](AGENT-PROMPT.ru.txt) своему агенту на компьютере.
   В новых настройках CanvasTTY есть кнопка **«Скопировать промпт агенту»**.
4. Агент проверит подключённое устройство, скачает APK, сверит SHA-256 и установит
   через `adb -s SERIAL install -r PATH_TO_APK` с сохранением данных.
5. Откройте CanvasLink на Android. Подключите оба устройства к одной домашней
   Wi-Fi/LAN-сети. В CanvasTTY включите **Настройки → CanvasLink → Включить доступ**.
   На Android выберите найденный компьютер и введите показанный одноразовый код.

USB нужен только для установки. IP обычно вводить не нужно. Коснитесь терминала,
чтобы вызвать клавиатуру; Enter выполняет команду. Доступ распространяется на
**всё текущее окно CanvasTTY**, включая настройки и видимые терминалы.
После перезапуска компьютера доступ включается заново; отключить доступ или
забыть устройство можно в настройках. У очков Even G2 отдельное подключение.

### Установка вручную

Скачайте [APK](https://github.com/teo-nex/CanvasLink/releases/download/v0.3.0-alpha.1/CanvasLink-0.3.0-alpha.1.apk)
и сверьте SHA-256 с [SHA256SUMS](SHA256SUMS). Затем откройте файл на Android,
подтвердив установку из выбранного браузера или файлового менеджера.
Разрешения на установку другим приложениям не нужны.

Либо используйте ADB из [Google Platform-Tools](https://developer.android.com/tools/releases/platform-tools):

```sh
adb devices -l
adb -s SERIAL install -r CanvasLink-0.3.0-alpha.1.apk
adb -s SERIAL shell am start -n io.nexcore.canvaslink/.MainActivity
```

Вместо SERIAL укажите нужное авторизованное устройство. Статус `unauthorized`
означает, что нужно подтвердить запрос на Android. При `offline` сначала исправьте подключение.

### Если уже установлен тестовый CanvasLink

У этой alpha постоянная подпись для последующих обновлений. Старые локальные
и CI-сборки подписаны другими ключами; Android может вернуть
`INSTALL_FAILED_UPDATE_INCOMPATIBLE`. Агент должен остановиться и объяснить причину.
**Не удаляйте старое приложение и не очищайте его данные автоматически.**
Переход согласуется с владельцем устройства. Следующие версии с этой подписью
и увеличенным versionCode смогут обновлять alpha обычным способом.

## Что опубликовано и проверено

[release.json](release.json) содержит точную версию, ссылку, SHA-256, открытый
отпечаток сертификата, исходный коммит и происхождение APK из CI.
Код APK взят из [CI CanvasTTY](https://github.com/howdeploy/CanvasTTY/actions/runs/40235936427),
коммит [`eba7baf`](https://github.com/teo-nex/CanvasTTY/commit/eba7baf1f3db716b6600a605f1fda07c39e9119f).
После переподписи все ZIP-записи вне `META-INF` сверены побайтно.
Закрытый ключ хранится отдельно и не публикуется. Тестовая Android-инструментация в APK не входит.

Это предварительная версия сообщества. Восемь проверок исходного PR прошли,
включая APK и CI для Mac, Windows и Linux. Это не заменяет проверку управления,
GPU-захвата, IME и сети на реальных устройствах. Новый подписанный APK и порт
в исходники не наследуют автоматически ручную приёмку прототипа.

Плавные 30 FPS не обещаются: резервный режим захвата у прототипа давал примерно
3–6 FPS. Изоляция клиентов Wi-Fi может мешать обнаружению; тогда есть ручной
ввод частного IPv4. Используются TCP 3499 и mDNS, облачного ретранслятора нет.
Порт в Интернет не пробрасывайте.

[Подробная документация](https://github.com/teo-nex/CanvasTTY/blob/feat/canvaslink-android-lan/docs/canvaslink.ru.md)
и [границы проверки](https://github.com/teo-nex/CanvasTTY/blob/feat/canvaslink-android-lan/docs/canvaslink-verification.md).

MIT; шрифт Onest — SIL OFL 1.1. Лицензии: [LICENSE](LICENSE),
[THIRD_PARTY_NOTICES.md](THIRD_PARTY_NOTICES.md), [FONT-LICENSE.txt](FONT-LICENSE.txt).
