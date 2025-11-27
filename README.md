# amnezia-vpn-android-autoconnect
Automatic AmneziaVPN autoconnect on Android/Android TV using MacroDroid and ADB (optional)

**Цель - загрузить GUI AmneziaVPN при перезагрузке TV-Box и нажать кнопку "Подключиться"**

1. Устанавливаем [MacroDroid](https://play.google.com/store/search?q=macrodroid&c=apps&hl=ru) (в тесте v5.57.6)
2. Включаем на приставке `Специальные возможности` - `Все сервисы MacroDroid`
3. Расчитываем координаты кнопки на экране

```
> adb shell wm size
Physical size: 1280x720
```
Экран: 1280×720 пикселей

Кнопка: горизонтально по центру (`X`), вертикально — центр верхней четверти экрана (`Y`)

### Расчёт координат
1. Горизонтальная координата X (по центру):
X=1280 ÷ 2 = 640 пикселей

2. Вертикальная координата Y (центр верхней четверти):

**Верхняя четверть:** 720 ÷ 4 = 180 пикселей

**Центр этой четверти:** 180 ÷ 2 = 90 пикселей

**Итого координаты для MacroDroid:** `X` = 640, `Y` = 90

**Примечание:** Если есть подключение по ADB координаты кнопки можно расчитать однострочником
```
let x=$(adb shell wm size | awk -F'[: x]+' '{print $3}')/2; let y=$(adb shell wm size | awk -F'[: x]+' '{print $4}')/8; echo X=$x; echo Y=$y
```
Импортируем в MacroDroid [amnezia-clickbtn1.mdr](https://github.com/AKotov-dev/amnezia-vpn-android-autoconnect/blob/main/amnezia-clickbtn1.mdr)  
  
В макросе `click-button` ставим значения `X` и `Y`, расчитанные для своего экрана, сохраняем.

![](https://github.com/AKotov-dev/amnezia-vpn-android-autoconnect/blob/main/macro-screenshot.png)

Перезагружаем TV-Box и получаем автоподключение VPN при перезагрузке.
