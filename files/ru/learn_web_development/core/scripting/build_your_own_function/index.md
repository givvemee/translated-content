---
title: Создаём свою функцию
slug: Learn_web_development/Core/Scripting/Build_your_own_function
---

{{LearnSidebar}}{{PreviousMenuNext("Learn/JavaScript/Building_blocks/Functions","Learn/JavaScript/Building_blocks/Return_values", "Learn/JavaScript/Building_blocks")}}

Эта статья призвана дать практический опыт на основе теоретических знаний приведённых в [предыдущей статье](/ru/docs/Learn_web_development/Core/Scripting/Functions). Попутно мы также объясним некоторые важные детали работы с функциями.

| Предпосылки: | Базовая компьютерная грамотность, базовое понимание HTML и CSS, [первые шаги в JavaScript](/ru/docs/conflicting/Learn_web_development/Core/Scripting), [Функции — блоки кода используемые многократно](/ru/docs/Learn_web_development/Core/Scripting/Functions). |
| ------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Задача:      | Научить создавать пользовательской функции и объяснить ещё несколько полезных деталей.                                                                                                                                                                           |

## Активное обучение: построение функции

Пользовательская функция, которую мы собираемся построить, будет называться `displayMessage()`. Она отобразит настраиваемое окно сообщения на веб-странице и будет действовать как настраиваемая замена встроенной в браузер функции [alert()](/ru/docs/Web/API/Window/alert). Мы видели эту функцию раньше. Введите следующую команду в консоли JavaScript браузера на любой странице:

```js
alert("This is a message");
```

Функция `alert` принимает один аргумент - строку, которая отображается в окне сообщения на веб-странице Попробуйте изменить строку, чтобы изменить сообщение.

Функция `alert` ограничена: вы можете изменить текст сообщения, но не получится изменить его стиль, например, цвет, значок или что-то ещё. Создадим сообщение, более интересное по стилю.

> [!NOTE]
> Этот пример будет работать во всех современных браузерах, но стиль может выглядеть немного смешным в более старых браузерах. Мы рекомендуем вам выполнять это упражнение в современном браузере, таком как Firefox, Opera или Chrome.

## Основная функция

Для начала давайте соберём основную функцию.

> [!NOTE]
> Для согласований имён функций нужно следовать тем же правилам, что и [правила именования переменных](/ru/docs/Learn_web_development/Core/Scripting/Variables#правила_именования_переменных). Отличить имена функций от имён переменных просто: после имён функций указываются круглые скобки, а после имён переменных их нет.

1. Откройте файл [function-start.html](https://github.com/mdn/learning-area/blob/master/javascript/building-blocks/functions/function-start.html) и скопируйте его себе на компьютер. Код HTML в нем предельно прост: body содержит только одну кнопку. Также здесь представлен базовый CSS для создания настраиваемого окна сообщений и пустой элемент {{htmlelement ("script")}} для размещения нашего JavaScript.
2. Затем добавьте строку внутри элемента `<script>`:

   ```js
   function displayMessage() {}
   ```

   Мы начинаем с ключевого слова `function`, что означает, что мы определяем функцию. За ним следует имя, которое мы хотим дать нашей функции, набор круглых скобок и набор фигурных скобок. Любые параметры, которые мы хотим задать нашей функции, заключают в круглые скобки, а код, который запускается при вызове функции, находится внутри фигурных скобок.

3. Наконец, добавьте следующий код внутри фигурных скобок:

   ```js
   var html = document.querySelector("html");

   var panel = document.createElement("div");
   panel.setAttribute("class", "msgBox");
   html.appendChild(panel);

   var msg = document.createElement("p");
   msg.textContent = "This is a message box";
   panel.appendChild(msg);

   var closeBtn = document.createElement("button");
   closeBtn.textContent = "x";
   panel.appendChild(closeBtn);

   closeBtn.onclick = function () {
     panel.parentNode.removeChild(panel);
   };
   ```

Рассмотрим этот код по строкам (прим. - в оригинале статьи: "bit by bit").

В первой строке используется функция DOM API под именем {{domxref ("document.querySelector()")}} для выбора элемента {{htmlelement ("html")}}, сохраняющая ссылку на него в переменной `html`, чтобы позже мы могли с ней что-то сделать:

```js
var html = document.querySelector("html");
```

В следующем разделе используется другая функция DOM API, называемая {{domxref ("Document.createElement()")}}, применяется для создания элемента {{htmlelement ("div")}} и сохраняет ссылку на него в переменной, называемой `panel`. Этот элемент будет внешним контейнером нашего окна сообщений.

Затем мы используем ещё одну функцию DOM API, называемую {{domxref ("Element.setAttribute()")}}, чтобы установить атрибут `class` на нашей панели со значением `msgBox`. Это упрощает стилизацию элемента. Если вы посмотрите на CSS на странице, вы увидите, что мы используем селектор класса `.msgBox` для стилизации окна сообщения и его содержимого.

Наконец, мы вызываем функцию DOM с именем {{domxref ("Node.appendChild()")}} в переменной `html`, которую мы сохранили ранее, которая вкладывает один элемент в другой как его дочерний элемент. Указываем панель `<div>` как дочерний элемент, который мы хотим вложить внутрь элемента `<html>`. То есть, когда мы создаём какой-то элемент, он не просто будет отображаться на странице сам по себе, нам нужно указать, куда его поместить.

```js
var panel = document.createElement("div");
panel.setAttribute("class", "msgBox");
html.appendChild(panel);
```

В следующих двух разделах используются те же функции `createElement()` и `appendChild()`, которые мы уже видели, чтобы создать два новых элемента: {{htmlelement ("p")}} и {{htmlelement ("button")}}, и вставить их на страницу, как дочерних элементов панели `<div>`. Мы используем свойство {{domxref ("Node.textContent")}}, которое представляет текстовое содержимое элемента, для вставки сообщения внутри абзаца и символ «x» внутрь кнопки. Нажатие/активация этой кнопки будет закрывать окно сообщения.

```js
var msg = document.createElement("p");
msg.textContent = "This is a message box";
panel.appendChild(msg);

var closeBtn = document.createElement("button");
closeBtn.textContent = "x";
panel.appendChild(closeBtn);
```

В заключении мы используем обработчик событий {{domxref ("GlobalEventHandlers.onclick")}}, чтобы при нажатии кнопки был запущен некоторый код для удаления всей панели со страницы, т.е. для закрытия окна сообщения.

Вкратце, обработчик `onclick` — это свойство, доступное для кнопки (или, фактически, для любого элемента страницы), которое можно установить в функцию, чтобы указать, какой код следует запускать при нажатии кнопки. Вы узнаете об этом больше в нашей статье о последующих событиях. Мы делаем обработчик `onclick` равным анонимной функции, которая содержит код, запускаемый при нажатии кнопки. Строка внутри функции использует функцию {{domxref ("Node.removeChild()")}} DOM API, чтобы указать, что мы хотим удалить определённый дочерний элемент внутри HTML — в данном случае панель `<div>`.

```js
closeBtn.onclick = function () {
  panel.parentNode.removeChild(panel);
};
```

В принципе, весь этот блок кода генерирует блок HTML, который выглядит так и вставляет его на страницу:

```html
<div class="msgBox">
  <p>This is a message box</p>
  <button>x</button>
</div>
```

Вам не обязательно запоминать сейчас, как работает каждый элемент во всем этом коде. Основная задача — понять структуру и использование функции, при этом мы хотели показать что-то интересное для этого примера.

## Вызов функции

Теперь у вас есть определение функции, написанное в вашем элементе `<script>`, но оно ничего не будет делать в том виде, в каком оно есть.

1. Попробуйте написать следующую строку под своей функцией, чтобы вызвать её:

   ```js
   displayMessage();
   ```

   Эта строка вызывает функцию, немедленно запуская её. Когда вы сохраните код и перезагрузите его в браузере, вы увидите, что небольшое окно сообщения появляется сразу и только один раз.

2. Теперь откройте инструменты разработчика браузера на странице примера, перейдите в консоль JavaScript и снова введите эту строку. Вы увидите, что окно появится снова! Теперь у нас есть функция многократного использования, которую мы можем вызвать в любое время.

   Но мы, вероятно, хотим, чтобы оно появлялось в ответ на действия пользователя и системы. В реальном приложении такое окно сообщения, вероятно, будет вызвано в ответ на доступность новых данных или, если произошла ошибка, или, например, если пользователь пытается удалить свой профиль («вы уверены в этом?»), или если пользователь добавляет новый контакт и операция успешно завершена и т. д.

   В этой демонстрации мы получим окно сообщения, когда пользователь нажимает кнопку.

3. Удалите предыдущую добавленную строку.
4. Затем мы выберем кнопку и сохраним ссылку на неё в переменной. Добавьте следующую строку в свой код, над определением функции:

   ```js
   var btn = document.querySelector("button");
   ```

5. Наконец, добавьте следующую строку ниже предыдущей:

   ```js
   btn.onclick = displayMessage;
   ```

   Аналогично нашей строке `closeBtn.onclick...` внутри функции здесь мы вызываем некоторый код в ответ на нажатие кнопки. Но в этом случае вместо вызова анонимной функции, содержащей некоторый код, мы вызываем имя нашей функции напрямую.

6. Сохраните и обновите страницу. Теперь вы должны увидеть окно с сообщением, когда вы нажимаете кнопку.

Возможно, вам интересно, почему мы не включили круглые скобки после имени функции. Это связано с тем, что нам нужно не сразу вызвать функцию, а только после нажатия кнопки. Если вы попытаетесь изменить строку на

```js
btn.onclick = displayMessage();
```

сохраните и перезагрузите страницу, вы увидите, что окно сообщения появляется без нажатия кнопки! Скобки в этом контексте иногда называют «оператором вызова функции». Вы используете их только в том случае, если хотите немедленно запустить функцию в текущей области. В этом же отношении код внутри анонимной функции не запускается сразу, так как он находится внутри области функций.

Если вы пробовали последний эксперимент, перед тем, как продолжить, обязательно отмените последнее изменение.

## Улучшение функции с параметрами

В нынешнем виде функция по-прежнему не очень полезна — мы не хотим показывать одно и то же сообщение по умолчанию каждый раз. Давайте улучшим нашу функцию, добавив некоторые параметры, позволяющие нам называть её различными вариантами.

1. Прежде всего, обновите первую строку функции:

   ```js
   function displayMessage() {
   ```

   к этому:

   ```js
   function displayMessage(msgText, msgType) {
   ```

   Теперь, когда мы вызываем функцию, мы можем предоставить два значения переменных в круглых скобках, чтобы указать сообщение для отображения в окне сообщения, а также тип сообщения.

2. Чтобы использовать первый параметр, обновите следующую строку внутри своей функции:

   ```js
   msg.textContent = "This is a message box";
   ```

   к этому:

   ```js
   msg.textContent = msgText;
   ```

3. И последнее, но не менее важное: теперь вам нужно обновить вызов функции, чтобы включить в него обновлённый текст сообщения. Измените следующую строку:

   ```js
   btn.onclick = displayMessage;
   ```

   к этому блоку:

   ```js
   btn.onclick = function () {
     displayMessage("Woo, this is a different message!");
   };
   ```

   Если мы хотим указать параметры в круглых скобках для вызываемой нами функции, то мы не можем назвать её напрямую, нам нужно поместить её в анонимную функцию, чтобы она не находилась непосредственно в области видимости и, следовательно, не вызывалась немедленно. Теперь она не будет вызываться до нажатия кнопки.

4. Перезагрузите и протестируйте код ещё раз, и вы увидите, что он по-прежнему работает, только теперь вы также можете изменять сообщение внутри параметра, чтобы отображать разные сообщения в окне.

### Более сложный параметр

Переход к следующему параметру. Это потребует немного больше работы. Установим его так, чтобы в зависимости от того, какой параметр `msgType` установлен, функция отображала другой значок и другой цвет фона.

1. Для начала, загрузите значки, необходимые для этого упражнения ([warning](https://raw.githubusercontent.com/mdn/learning-area/master/javascript/building-blocks/functions/icons/warning.png) и [chat](https://raw.githubusercontent.com/mdn/learning-area/master/javascript/building-blocks/functions/icons/chat.png) \[тут чёрные иконки на чёрном фоне... тролли на GitHub]) из GitHub. Сохраните их в новой папке `icons` в том же месте, что и ваш HTML-файл.

   > [!NOTE]
   > Иконки были найдены на [iconfinder.com](https://www.iconfinder.com/), и разработаны [Nazarrudin Ansyari](https://www.iconfinder.com/nazarr). Спасибо! (Фактические страницы значков были перемещены или удалены.)

2. Затем найдите CSS внутри вашего HTML-файла. Мы сделаем несколько изменений, чтобы освободить место для иконок. Во-первых, обновите ширину `.msgBox`:

   ```css
   width: 200px;
   ```

   измените на:

   ```css
   width: 242px;
   ```

3. Затем добавьте следующие строки в правило `.msgBox p { ... }` :

   ```css
   padding-left: 82px;
   background-position: 25px center;
   background-repeat: no-repeat;
   ```

4. Теперь нам нужно добавить код в нашу функцию `displayMessage()` для обработки отображений значков. Добавьте следующий блок чуть выше закрывающей фигурной скобки "`}`" вашей функции:

   ```js
   if (msgType === "warning") {
     msg.style.backgroundImage = "url(icons/warning.png)";
     panel.style.backgroundColor = "red";
   } else if (msgType === "chat") {
     msg.style.backgroundImage = "url(icons/chat.png)";
     panel.style.backgroundColor = "aqua";
   } else {
     msg.style.paddingLeft = "20px";
   }
   ```

   Здесь, если параметр `msgType` установлен как `'warning'`, отображается значок предупреждения, а цвет фона панели устанавливается красным. Если для него установлено значение`'chat'`, отображается значок чата, а цвет фона панели становится голубым. Если параметр `msgType` не задан вообще (или задано что-то другое), тогда вступает в действие `else {...}`, а абзацу просто присваиваются заданные по умолчанию отступы, нет никакого значка, при этом не задаётся цвет фона окна сообщения. Это обеспечивает состояние по умолчанию, если не указан параметр `msgType`, что означает, что это необязательный параметр!

5. Давайте протестируем нашу обновлённую функцию, попробуем обновить вызов displayMessage () из этого:

   ```js
   displayMessage("Woo, this is a different message!");
   ```

   к одному из них:

   ```js
   displayMessage("Your inbox is almost full — delete some mails", "warning");
   displayMessage("Brian: Hi there, how are you today?", "chat");
   ```

   Вот, насколько полезной становится наша (теперь не очень) маленькая функция.

> [!NOTE]
> Если у вас возникли проблемы с запуском примера, не стесняйтесь проверять свой код на готовой версии [GitHub](https://github.com/mdn/learning-area/blob/master/javascript/building-blocks/functions/function-stage-4.html) (см. также [в режиме реального времени](https://mdn.github.io/learning-area/javascript/building-blocks/functions/function-stage-4.html)) или обратитесь к нам за помощью.

## Вывод

В этой статье мы познакомились со всем процессом создания практической пользовательской функции, которую с небольшими доработками можно перенести в реальный проект. В следующей статье мы рассмотрим ещё одну важную концепцию — возвращаемые значения функций.

{{PreviousMenuNext("Learn/JavaScript/Building_blocks/Functions","Learn/JavaScript/Building_blocks/Return_values", "Learn/JavaScript/Building_blocks")}}
