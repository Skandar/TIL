# Управление отображаемой клавиатурой с помощью атрибута `inputmode` 

Атрибут `inputmode` позволяет подсказать браузеру какую клавиатуру необходимо отобразить. Имеет выше приоритет чем атрибут `type`. Атрибут используется с элементами `input`, `textarea` и элементами у которых присутствует атрибут  `contenteditable`. [Demo](https://inputmodes.com/)

## Возможные значения

- **`none`** - не показывать клавиатуру (Chrome Android). В iOS 12.2 показывать клавиатуру по умолчанию.
- **`numeric`** - цифровая клавиатура. Хорошо подходит для случаев где необходимо вводить только цифры: пин-код, номер кредитной карты, почтовый код (для тех стран где используются числовые коды), количество, возраст и т.д. ![Значение numeric в Chrome Android (слева) и iOS 12.2 (справа)](https://res.cloudinary.com/css-tricks/image/upload/c_scale,w_1000,f_auto,q_auto/v1557186018/inputmode-01_k2m78v.png)
- **`tel`** - телефонная клавиатура. ![Значение tel в Chrome Android (слева) и iOS 12.2 (справа)](https://res.cloudinary.com/css-tricks/image/upload/c_scale,w_1000,f_auto,q_auto/v1557186061/inputmode-02_lulpoj.png)
- **`decimal`** - десятичная числовая клавиатура. Для Crome Android такая же как значение `numeric` для iOS похожа на телефонную с измененными символами **+*#** на **.**  ![Значение decimal в Chrome Android (слева) и iOS 12.2 (справа)](https://res.cloudinary.com/css-tricks/image/upload/c_scale,w_1000,f_auto,q_auto/v1557186084/inputmode-03_ikre04.png)
- **`email`** - стандартная клавиатура с заменённой кнопкой emoji на **@** (Chrome Android). Помимо поля ввода почтового адреса, так же возможно будет удобно для ввода поля ввода username в твитере и других случаях в которых часто используется **@** или в случае использования кастомной валидации поля ввода почтового адреса (не встроенной в браузер). ![Значение email в Chrome Android (слева) и iOS 12.2 (справа)](https://res.cloudinary.com/css-tricks/image/upload/c_scale,w_1000,f_auto,q_auto/v1557186105/inputmode-04_wp0kqb.png)
- **`url`** - добавляет на клавиатуру **/**, что удобно для ввод url.![Значение url в Chrome Android (слева) и iOS 12.2 (справа)](https://res.cloudinary.com/css-tricks/image/upload/c_scale,w_1000,f_auto,q_auto/v1557186130/inputmode-05_zevfop.png)
- **`search`** - меняет кнопку **Return** (iOS) на кнопку **Go**, в Ghrome Android меняет кнопку **Return** на кнопку **Enter**. Если нужно показывать вместо кнопки **Go** (iOS) и **Enter** (Chrome Android) кнопку “увеличительное стекло”, то лучше использовать атрибут `search`. ![Значение search в Chrome Android (слева) и iOS 12.2 (справа)](https://res.cloudinary.com/css-tricks/image/upload/c_scale,w_868,f_auto,q_auto/v1557186281/inputmode-06a_rdj810.png)



## Применение

- В формах где использования атрибута `type` для полей не подходит.
- В кастомных компонентах не содержащих элемент `input`.
- В любых элементах с атрибутом `contenteditable`, если текстовой клавиатуры по умолчанию не достаточно.

##  Ссылки

- [Everything You Ever Wanted to Know About inputmode](https://css-tricks.com/everything-you-ever-wanted-to-know-about-inputmode/)

- [MDN](https://developer.mozilla.org/en-US/docs/Web/HTML/Global_attributes/inputmode)