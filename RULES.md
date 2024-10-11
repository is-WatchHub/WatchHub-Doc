# Правила работы в команде

---

## Правила именования веток

ветки должны именоваться следующим образом: <название ветки>(<номер задачи>)

пример:

```
git branch rules(#2)
```

__rules__ - название ветки
__#2__ - номер задачи

---

## Правила именования коммитов

коммиты должны именоваться следующим образом: (<номер задачи>) <действие>:<что было сделано>

<действие> может быть одним из следующих состояний:
+ add - что-то добавили новое
+ update - обновили что-то
+ delete - что-то удалили
+ fix - что-то исправили (ошибку)

пример:

```
git commit -m "(#2) add: RULES.md"
```

__#2__ - номер задачи
__add__ - действие
__RULES.md__ - что было сделано, может быть любой информативный текст

## Примечание

старайтесь чаще коммитить, так чтобы коммиты наиболее точно отражали то что вы сделали