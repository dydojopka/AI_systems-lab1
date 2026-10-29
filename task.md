Необходимо реализовать онтологию предметной области компьютерной игры Dota 2 в формате RDF/OWL. Онтология должна демонстрировать классы, иерархию классов, объектные свойства, свойства данных, ограничения, экземпляры и связи между экземплярами.

## 1. Общая структура онтологии

Создать корневой пользовательский класс:

Dota2Entity

Все основные сущности предметной области должны быть подклассами Dota2Entity.

Основные классы:

* Game
* Match
* Player
* Team
* Hero
* Ability
* Item
* Building
* Resource
* Map
* Role

Иерархия должна иметь следующий общий вид:

owl:Thing
└── Dota2Entity
├── Game
├── Match
├── Player
├── Team
├── Hero
├── Ability
├── Item
├── Building
├── Resource
├── Map
└── Role

## 2. Иерархия классов

### Match

Создать подклассы:

* RankedMatch
* NormalMatch

Иерархия:

Match
├── RankedMatch
└── NormalMatch

### Hero

Создать подклассы:

* StrengthHero
* AgilityHero
* IntelligenceHero
* UniversalHero

Иерархия:

Hero
├── StrengthHero
├── AgilityHero
├── IntelligenceHero
└── UniversalHero

### Ability

Создать подклассы:

* ActiveAbility
* PassiveAbility
* UltimateAbility

Иерархия:

Ability
├── ActiveAbility
├── PassiveAbility
└── UltimateAbility

### Item

Создать подклассы:

* BasicItem
* ComponentItem
* ConsumableItem

Иерархия:

Item
├── BasicItem
├── ComponentItem
└── ConsumableItem

### Building

Создать подклассы:

* Tower
* Barracks
* Ancient

Иерархия:

Building
├── Tower
├── Barracks
└── Ancient

Для Tower дополнительно создать:

Tower
├── Tier1Tower
├── Tier2Tower
├── Tier3Tower
└── Tier4Tower

Для Barracks:

Barracks
├── MeleeBarracks
└── RangedBarracks

### Resource

Создать подклассы:

* Gold
* Experience
* Health
* Mana

Иерархия:

Resource
├── Gold
├── Experience
├── Health
└── Mana

### Map

Создать подклассы:

* Lane
* Jungle
* River
* Base

Для Lane:

Lane
├── TopLane
├── MidLane
└── BottomLane

### Role

Создать подклассы:

* Carry
* Midlaner
* Offlaner
* SoftSupport
* HardSupport

## 3. Объектные свойства

Создать следующие owl:ObjectProperty.

### controls

Domain:
Player

Range:
Hero

Смысл:
игрок управляет героем.

### belongsTo

Domain:
Player

Range:
Team

Смысл:
игрок принадлежит команде.

### participatesIn

Domain:
Player

Range:
Match

Смысл:
игрок участвует в матче.

### hasAbility

Domain:
Hero

Range:
Ability

Смысл:
герой обладает способностью.

### usesItem

Domain:
Hero

Range:
Item

Смысл:
герой использует предмет.

### hasRole

Domain:
Hero

Range:
Role

Смысл:
герой выполняет определённую игровую роль.

### hasResource

Domain:
Hero

Range:
Resource

Смысл:
герой связан с игровым ресурсом.

### takesPlaceOn

Domain:
Match

Range:
Map

Смысл:
матч проходит на игровой карте.

### attacks

Domain:
Hero

Range:
Building

Смысл:
герой может атаковать игровое сооружение.

### defends

Domain:
Team

Range:
Building

Смысл:
команда защищает сооружение.

### contains

Domain:
Map

Range:
Building

Смысл:
игровая карта содержит сооружения.

### memberOfTeam

Domain:
Hero

Range:
Team

Смысл:
герой в конкретном матче относится к определённой команде.

## 4. Свойства данных

Создать следующие owl:DatatypeProperty.

### hasName

Range:
xsd:string

Используется для текстового названия сущности.

### hasCost

Range:
xsd:integer

Применяется прежде всего к Item.

### hasHealth

Range:
xsd:integer

Применяется к Hero и при необходимости Building.

### hasMana

Range:
xsd:integer

Применяется к Hero.

### hasLevel

Range:
xsd:integer

Применяется к Hero.

### hasDamage

Range:
xsd:integer

Применяется к Hero, Ability или Building, если это необходимо для демонстрации модели.

### hasGold

Range:
xsd:integer

Применяется к Hero.

### hasExperience

Range:
xsd:integer

Применяется к Hero.

## 5. Ограничения классов

Добавить OWL-ограничения, демонстрирующие семантические связи.

Для Hero:

Hero SubClassOf:
hasAbility some Ability

Hero SubClassOf:
usesItem some Item

Hero SubClassOf:
hasRole some Role

То есть каждый рассматриваемый экземпляр Hero в рамках модели должен быть связан как минимум с некоторой Ability, Item и Role.

Для Player:

Player SubClassOf:
controls some Hero

Player SubClassOf:
belongsTo some Team

Player SubClassOf:
participatesIn some Match

Для Match:

Match SubClassOf:
takesPlaceOn some Map

## 6. Экземпляры

Создать набор owl:NamedIndividual для демонстрации работы онтологии.

### Герои

Создать:

* Pudge
* Juggernaut
* Invoker
* CrystalMaiden

Типизация:

Pudge rdf:type StrengthHero

Juggernaut rdf:type AgilityHero

Invoker rdf:type IntelligenceHero

CrystalMaiden rdf:type IntelligenceHero

### Игроки

Создать:

* Player001
* Player002

Тип:

Player

### Команды

Создать:

* TeamRadiant
* TeamDire

Тип:

Team

При желании добавить строковые названия:

TeamRadiant hasName "Radiant"

TeamDire hasName "Dire"

### Матч

Создать:

Match001

Тип:

Match

Дополнительно допустимо:

Match001 rdf:type RankedMatch

### Карта

Создать:

Dota2Map

Тип:

Map

### Роли

Создать:

* CarryRole
* MidRole
* OfflaneRole
* SoftSupportRole
* HardSupportRole

Типизировать соответственно классами:

CarryRole rdf:type Carry
MidRole rdf:type Midlaner
OfflaneRole rdf:type Offlaner
SoftSupportRole rdf:type SoftSupport
HardSupportRole rdf:type HardSupport

### Способности

Создать минимум несколько экземпляров:

* MeatHook
* BladeFury
* Quas
* CrystalNova

Типизировать подходящими подклассами Ability.

Например:

MeatHook rdf:type ActiveAbility
BladeFury rdf:type ActiveAbility
Quas rdf:type ActiveAbility
CrystalNova rdf:type ActiveAbility

### Предметы

Создать минимум:

* Tango
* HealingSalve
* BootsOfSpeed
* BlinkDagger

Типизировать соответствующими подклассами Item.

Например:

Tango rdf:type ConsumableItem
HealingSalve rdf:type ConsumableItem
BootsOfSpeed rdf:type BasicItem
BlinkDagger rdf:type Item

## 7. Связи между экземплярами

Добавить демонстрационные утверждения.

Player001:

* controls Pudge
* belongsTo TeamRadiant
* participatesIn Match001

Player002:

* controls Invoker
* belongsTo TeamDire
* participatesIn Match001

Match001:

* takesPlaceOn Dota2Map

Pudge:

* hasAbility MeatHook
* hasRole OfflaneRole
* usesItem BlinkDagger
* memberOfTeam TeamRadiant

Invoker:

* hasAbility Quas
* hasRole MidRole
* usesItem BootsOfSpeed
* memberOfTeam TeamDire

Juggernaut:

* hasAbility BladeFury
* hasRole CarryRole

CrystalMaiden:

* hasAbility CrystalNova
* hasRole HardSupportRole

## 8. Значения свойств данных

Добавить демонстрационные значения.

Например:

Pudge:

* hasName "Pudge"
* hasLevel 10
* hasHealth 1500
* hasMana 700
* hasGold 2500
* hasExperience 5000

Invoker:

* hasName "Invoker"
* hasLevel 10
* hasHealth 1000
* hasMana 1200
* hasGold 3000
* hasExperience 5500

BlinkDagger:

* hasName "Blink Dagger"
* hasCost 2250

BootsOfSpeed:

* hasName "Boots of Speed"

Значения нужны прежде всего для демонстрации работы datatype properties и не обязаны отражать конкретное текущее состояние баланса Dota 2.

## 9. Связанные онтологии

Для выполнения требования о 3–4 связанных онтологиях разделить предметную область на четыре модуля.

### Dota2Core.rdf

Базовая онтология.

Содержит основные сущности:

* Dota2Entity
* Game
* Match
* Player
* Team
* Hero
* Map

Также содержит наиболее общие свойства и базовые отношения.

### Dota2Heroes.rdf

Импортирует Dota2Core.rdf.

Содержит:

* Hero и специализированные типы героев
* Ability
* ActiveAbility
* PassiveAbility
* UltimateAbility
* Role
* игровые роли
* связи hasAbility и hasRole
* экземпляры героев и способностей

### Dota2Gameplay.rdf

Импортирует Dota2Core.rdf.

Содержит:

* Match
* Map
* Lane
* Jungle
* River
* Base
* Building
* Tower
* Barracks
* Ancient
* игровые отношения между командами, героями, картой и сооружениями

### Dota2Items.rdf

Импортирует Dota2Core.rdf.

Содержит:

* Item
* BasicItem
* ComponentItem
* ConsumableItem
* Resource
* Gold
* Experience
* Health
* Mana
* свойства hasCost, hasGold, hasExperience, hasHealth, hasMana
* экземпляры предметов

Связь между модулями реализовать через owl:imports.

Не создавать циклические импорты.

## 10. Пространства имён

Использовать единообразные URI для всех онтологий.

Пример базового пространства имён:

http://example.org/dota2#

Для отдельных модулей допустимо использовать:

http://example.org/dota2/core#
http://example.org/dota2/heroes#
http://example.org/dota2/gameplay#
http://example.org/dota2/items#

URI онтологий должны быть согласованы с owl:imports.

## 11. Семантическая корректность

Не использовать один и тот же URI одновременно как случайно созданный класс, свойство и экземпляр, если это не является осознанным OWL-моделированием.

Все ObjectProperty должны иметь корректные ссылки на ресурсы.

Все DatatypeProperty должны содержать литеральные значения соответствующего XSD-типа.

Все используемые классы должны быть объявлены как owl:Class.

Все экземпляры должны быть объявлены как owl:NamedIndividual.

Все объектные свойства должны быть объявлены как owl:ObjectProperty.

Все свойства данных должны быть объявлены как owl:DatatypeProperty.

Иерархию классов реализовать через rdfs:subClassOf.

Domain реализовать через rdfs:domain.

Range реализовать через rdfs:range.

Импорты реализовать через owl:imports.

Экзистенциальные ограничения вида "some" реализовать через owl:Restriction с:

* owl:onProperty
* owl:someValuesFrom

## 12. Проверка результата

После редактирования RDF необходимо убедиться, что файлы:

1. являются синтаксически корректными RDF/XML;
2. корректно открываются как OWL-онтологии;
3. содержат заявленную иерархию классов;
4. содержат Object Properties и Datatype Properties;
5. содержат Domain и Range;
6. содержат экземпляры;
7. содержат связи между экземплярами;
8. содержат OWL Restrictions;
9. корректно используют owl:imports;
10. не содержат битых URI и ссылок на несуществующие локальные сущности;
11. позволяют OWL reasoner обработать онтологию без обнаружения непреднамеренной логической противоречивости.

Итогом должны быть 4 связанных RDF/OWL-файла:

Dota2Core.rdf
Dota2Heroes.rdf
Dota2Gameplay.rdf
Dota2Items.rdf

Онтология должна быть достаточно наполненной, чтобы при открытии в Protégé можно было продемонстрировать иерархию классов, свойства, ограничения, экземпляры, связи между экземплярами и результат логического вывода.
