# QuarkCoppersmith/waRDOGS-SeTup-DiSCOrd_ZAPrEt

Форк [QuarkCoppersmith/waRDOGS-SeTup-DiSCOrd_ZAPrEt](https://github.com/QuarkCoppersmith/waRDOGS-SeTup-DiSCOrd_ZAPrEt), заранее настроенный так, чтобы работали **War Dogs** и **Discord** одновременно.

Главное отличие от оригинала — файл **`AUTO-PICK-ZAPRET.bat`**: он сам перебирает стратегии и останавливается на той, что работает сегодня. Руками по одной запускать больше не нужно.

## Как пользоваться

1. Скачать репозиторий: зелёная кнопка **Code → Download ZIP**
2. ПКМ по архиву → **Свойства** → галочка **«Разблокировать»** → ОК
3. Распаковать в путь **без кириллицы и пробелов** — например `C:\zapret`
4. ПКМ по **`AUTO-PICK-ZAPRET.bat`** → **«Запуск от имени администратора»**

Скрипт перебирает стратегии и на каждой проверяет три адреса Discord — сайт, gateway и CDN. Останавливается на первой, где отвечают все три, и оставляет её работать. Занимает от нескольких секунд до пары минут.

Доступность античита War Dogs проверяется отдельно и **на выбор стратегии не влияет** — почему, см. ниже.

Первой всегда пробуется `general (ALT11)` — она подтверждённо работает с War Dogs.

Результат последнего запуска пишется в `auto-pick-last-run.txt`.

## Что уже настроено

| Настройка | Значение | Зачем |
|---|---|---|
| Game Filter | `enabled (UDP)` | War Dogs использует UDP на портах выше 1023 |
| IPSet Filter | `any` | под фильтр попадает любой IP игры |
| `lists/list-general.txt` | 105 строк | штатные домены + Cloudflare + `codefusion.technology` (античит) |
| `lists/list-exclude.txt` | 129 строк | штатные исключения + Яндекс, Teams и прочее |

Списки — **надстройка** над оригинальными: все домены Discord и YouTube из штатной сборки на месте, ничего не удалено. Поэтому Discord не ломается.

### Почему античит не влияет на выбор стратегии

Все 8 доменов античита (`ac-*.codefusion.technology`) присутствуют **одновременно** в `list-general.txt` и в `list-exclude.txt`. В winws исключения имеют приоритет над списком обхода, поэтому zapret пропускает этот трафик нетронутым — при любой стратегии.

Скорее всего так и задумано: вмешиваться в трафик античита — плохая идея. Но следствие важно понимать: **по доступности античита нельзя отличить одну стратегию от другой**, результат будет одинаковым хоть с обходом, хоть без него. Поэтому `AUTO-PICK` выбирает стратегию по Discord, а античит показывает справочно — если он не отвечает, менять стратегию бессмысленно, проблема в сети.

Если захотите, чтобы античит всё же обходился, удалите строки `codefusion` из `lists/list-exclude.txt`. Конфиг из Discord-гайда я оставил как есть, потому что он у вас рабочий.

## Если не работает

- **Ни одна стратегия не прошла** — скрипт напишет, какая была лучшей, и запустит её. Часто этого достаточно.
- **`winws.exe` не стартует** — почти всегда антивирус забрал `WinDivert`. Добавьте папку в исключения или отключите детект PUA.
- **Нет прав администратора** — без них WinDivert не загрузится, обход не заработает в принципе.
- **Голосовой чат Discord висит на «подключении»** — нужны записи в `hosts`: запустите `service.bat` → пункт **9. Update Hosts File**. На машине, где диск откатывается после сессии, это придётся делать каждый раз.
- **Тормозят посторонние сайты** — это цена режима `IPSet any`. Вернуть: `service.bat` → **5. IPSet Filter**. Полный список лежит в `lists/ipset-all.txt.backup`.

## Ручной режим

Автоподбор ничего не ломает в оригинальной сборке — все штатные файлы на месте. Если хочется по-старому, просто запускайте `general (ALT11).bat` или любой другой напрямую, как раньше.

## Откуда взялся конфиг

Связку «ALT11 + Game Filter UDP + IPSet any + подменённые списки» подсказали на официальном Discord-сервере War Dogs. Стратегии со временем перестают работать и зависят от провайдера — поэтому и нужен автоподбор.

## Лицензия и происхождение

Оригинальный README сохранён рядом — [README-UPSTREAM.md](README-UPSTREAM.md), там полная документация по всем стратегиям и настройкам.

Оригинальный проект — [QuarkCoppersmith/waRDOGS-SeTup-DiSCOrd_ZAPrEt](https://github.com/QuarkCoppersmith/waRDOGS-SeTup-DiSCOrd_ZAPrEt), лицензия MIT. Бинарники в `bin/` взяты из [bol-van/zapret-win-bundle](https://github.com/bol-van/zapret-win-bundle) — их можно сверить по контрольным суммам с оригиналом.

Отдельная благодарность [bol-van](https://github.com/bol-van) — автору [zapret](https://github.com/bol-van/zapret).

---
<p align="center">
  <a href="https://github.com/QuarkCoppersmith/waRDOGS-SeTup-DiSCOrd_ZAPrEt/releases/tag/1.10.3" target="_blank">
    <img src="https://img.shields.io/github/downloads/QuarkCoppersmith/waRDOGS-SeTup-DiSCOrd_ZAPrEt/total.svg?style=for-the-badge&label=Downloads&logo=github" alt="Downloads">
  </a>
  <a href="https://github.com/QuarkCoppersmith/waRDOGS-SeTup-DiSCOrd_ZAPrEt/releases/latest" target="_blank">
    <img src="https://img.shields.io/github/v/release/QuarkCoppersmith/waRDOGS-SeTup-DiSCOrd_ZAPrEt?style=for-the-badge&label=Latest" alt="Latest Release">
  </a>
  <a href="https://github.com/QuarkCoppersmith/waRDOGS-SeTup-DiSCOrd_ZAPrEt/blob/main/LICENSE.txt" target="_blank">
    <img src="https://img.shields.io/github/license/QuarkCoppersmith/waRDOGS-SeTup-DiSCOrd_ZAPrEt?style=for-the-badge&label=License" alt="License">
  </a>
</p>

<p align="center">
  <a href="https://github.com/QuarkCoppersmith/waRDOGS-SeTup-DiSCOrd_ZAPrEt/issues" target="_blank">
    <img src="https://img.shields.io/github/issues-raw/QuarkCoppersmith/waRDOGS-SeTup-DiSCOrd_ZAPrEt?style=for-the-badge&label=Open%20Issues&logo=github" alt="Open Issues">
  </a>
  <a href="https://github.com/QuarkCoppersmith/waRDOGS-SeTup-DiSCOrd_ZAPrEt/contributors" target="_blank">
    <img src="https://img.shields.io/github/contributors/QuarkCoppersmith/waRDOGS-SeTup-DiSCOrd_ZAPrEt?style=for-the-badge&label=Contributors&logo=github" alt="Contributors">
  </a>
</p>

---

## NEW

**War Dogs** — игра, требующая стабильного интернет-соединения. Разработчики используют **Zapret** для обхода блокировок, которые могут повлиять на игровой процесс. Этот репозиторий предлагает **преднастроенную сборку Zapret** специально для War Dogs и Discord, что позволяет использовать оба сервиса одновременно без потери качества.

### 🚀 Ключевые особенности:

*   **Автоматический подбор стратегии:** Файл `AUTO-PICK-ZAPRET.bat` самостоятельно находит рабочую конфигурацию Zapret, устраняя необходимость ручного выбора.
*   **Совместимость с War Dogs:** Оптимизированные списки доменов и настройки сети обеспечивают стабильную работу игры.
*   **Поддержка Discord:** Одновременная работа с Discord, включая голосовой чат.
*   **Гибкость настроек:** Возможность ручного выбора стратегии или изменения параметров через `service.bat`.

---

## ФЕЙКИ

В данном репозитории используются техники **подмены TLS-сертификатов** (TLS Client Hello) для обхода блокировок. Файлы вроде `tls_clienthello_4pda_to.bin`, `tls_clienthello_max_ru.bin`, `tls_clienthello_www_google_com.bin` содержат "фейковые" данные, имитирующие легитимные соединения, чтобы трафик не блокировался. Это позволяет сохранить доступ к нужным ресурсам, обходя ограничения.

---

## АНТИВИРУСЫ

<div class="admonition warning">
<p class="admonition-title">⚠️ Внимание!</p>
<p>Некоторые антивирусы могут детектировать компоненты Zapret (особенно **WinDivert**) как потенциально нежелательное ПО (PUA) или даже вредоносное. Это связано с тем, что WinDivert является низкоуровневым сетевым драйвером, который может использоваться для перехвата и модификации сетевого трафика. Для корректной работы Zapret рекомендуется добавить папку с распакованными файлами в исключения вашего антивируса.</p>
</div>

---

## Поддержка проекта

Если вы столкнулись с проблемами или хотите внести свой вклад в развитие проекта, пожалуйста, используйте следующие ресурсы:

*   **Issues:** [https://github.com/QuarkCoppersmith/waRDOGS-SeTup-DiSCOrd_ZAPrEt/issues](https://github.com/QuarkCoppersmith/waRDOGS-SeTup-DiSCOrd_ZAPrEt/issues)
*   **Upstream README:** [README-UPSTREAM.md](README-UPSTREAM.md)
*   **Оригинальный проект:** [QuarkCoppersmith/waRDOGS-SeTup-DiSCOrd_ZAPrEt](https://github.com/QuarkCoppersmith/waRDOGS-SeTup-DiSCOrd_ZAPrEt)

---

<p align="center">
  © 2023 QuarkCoppersmith. Все права защищены.
</p>