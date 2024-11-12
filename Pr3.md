# Практическое занятие №3. 

## Задача 1


Реализация на jsonnet

```
//1 
local student(name, age, group) ={
"age": age,
"name": name,
"group": group,
};
local groupN = "ИКБО-%g-%g";
{
groups: [
(groupN%[x,20]) for x in std.range(1,25)
], 
students:[ student("Иванов И.И.",19,"ИКБО-4-20"), 
student("Петров П.п.",18,"ИКБО-5-20"), 
student("Смирнов С.С.",19,"ИКБО-5-20"), 
student("Богачёва Б.А.",19,"ИКБО-68-23"), 
],
"subject": "Конфигурационное управление"
}
```
Json:

```
{
  "groups": [
    "ИКБО-1-20",
    "ИКБО-2-20",
    "ИКБО-3-20",
    "ИКБО-4-20",
    "ИКБО-5-20",
    "ИКБО-6-20",
    "ИКБО-7-20",
    "ИКБО-8-20",
    "ИКБО-9-20",
    "ИКБО-10-20",
    "ИКБО-11-20",
    "ИКБО-12-20",
    "ИКБО-13-20",
    "ИКБО-14-20",
    "ИКБО-15-20",
    "ИКБО-16-20",
    "ИКБО-17-20",
    "ИКБО-18-20",
    "ИКБО-19-20",
    "ИКБО-20-20",
    "ИКБО-21-20",
    "ИКБО-22-20",
    "ИКБО-23-20",
    "ИКБО-24-20",
    "ИКБО-25-20"
  ],
  "students": [
    {
      "age": 19,
      "group": "ИКБО-4-20",
      "name": "Иванов И.И."
    },
    {
      "age": 18,
      "group": "ИКБО-5-20",
      "name": "Петров П.п."
    },
    {
      "age": 19,
      "group": "ИКБО-5-20",
      "name": "Смирнов С.С."
    },
    {
      "age": 19,
      "group": "ИКБО-68-23",
      "name": "Дьячков А.А."
    }
  ],
  "subject": "Конфигурационное управление"
}
```

## Задача 2

Реализация на Dhall

```
let generate = https://prelude.dhall-lang.org/List/generate
let student = \(age: Natural) ->
\(group : Natural) -> \(name: Text) ->{
age = age,
group="ИКБО-"++ Natural/show group ++ "-23",
name = name} 
let group = \(n: Natural) -> "ИКБО-"
++ Natural/show n ++ "-20"
let groups = generate 25 Text group
let student=[
student 19 4 "Смирнов С.C.",
student 18 5 "Петров П.П.",
student 19 68 "Богачёва Б.А."]
let subject = "Конфигурационное управление"
in {groups, student, subject}
```
Json:

```
{
  "groups": [
    "ИКБО-0-20",
    "ИКБО-1-20",
    "ИКБО-2-20",
    "ИКБО-3-20",
    "ИКБО-4-20",
    "ИКБО-5-20",
    "ИКБО-6-20",
    "ИКБО-7-20",
    "ИКБО-8-20",
    "ИКБО-9-20",
    "ИКБО-10-20",
    "ИКБО-11-20",
    "ИКБО-12-20",
    "ИКБО-13-20",
    "ИКБО-14-20",
    "ИКБО-15-20",
    "ИКБО-16-20",
    "ИКБО-17-20",
    "ИКБО-18-20",
    "ИКБО-19-20",
    "ИКБО-20-20",
    "ИКБО-21-20",
    "ИКБО-22-20",
    "ИКБО-23-20",
    "ИКБО-24-20"
  ],
  "student": [
    {
      "age": 19,
      "group": "ИКБО-4-23",
      "name": "Смирнов С.C."
    },
    {
      "age": 18,
      "group": "ИКБО-5-23",
      "name": "Петров П.П."
    },
    {
      "age": 19,
      "group": "ИКБО-68-23",
      "name": "Богачёва Б.А."
    }
  ],
  "subject": "Конфигурационное управление"
}
```

## Задачи 3-5

```

import random


def parse_bnf(text):
    '''
    Преобразовать текстовую запись БНФ в словарь.
    '''
    grammar = {}
    rules = [line.split('=') for line in text.strip().split('\n')]
    for name, body in rules:
        grammar[name.strip()] = [alt.split() for alt in body.split('|')]
    return grammar


def generate_phrase(grammar, start):
    '''
    Сгенерировать случайную фразу.
    '''
    if start in grammar:
        seq = random.choice(grammar[start])
        return ''.join([generate_phrase(grammar, name) for name in seq])
    return str(start)

# Задание 3
# BNF = '''
# E = B | B E
# B = 0 | 1
# '''

# Задание 4
BNF = '''
E = P | C
P = ( E ) | ()
C = { E } | {}
'''

# Задание 5
# BNF = '''
# E = T | E "|" T
# T = F | T "&" F
# F = "~" F | "(" E ")" | VAR
# VAR = x | y | z
# '''

for i in range(10):
    print(generate_phrase(parse_bnf(BNF), 'E'))


```
