# LAB_02 - Data Flow e Componentes

> Informações sobre as atividades exigidas no laboratório neste [LINK](https://github.com/santanche/component2learn/tree/master/labs/02-data-flow_messages).

## :arrow_forward: Aluno
* Rafael Mardegan Marquini

## :hammer: Ferramentas e Tecnologias
* [JupyterNotebook](https://jupyter.org/)
* [Java 8](https://developers.redhat.com/products/openjdk/download)

---

# Tarefas

## Catálogo de Componentes

A entrega desta atividade compreende na resolução de 6 exercícios apresentados no notebook a seguir:
[components-01-catalog.ipynb](https://github.com/rmmarquini/engsoft-inf331-labs/blob/master/lab2/notebook/data-flow/s02catalog/components-01-catalog.ipynb); que apresenta o catálogo de componentes, o modo de conectá-los (visto pela perspectiva blackbox - externa) para montar uma composição.

> Instância do Binder com o notebook contendo os exercícios resolvidos

[![Binder](https://mybinder.org/badge_logo.svg)](https://mybinder.org/v2/gh/rmmarquini/engsoft-inf331-labs/master)

### Tarefa 1

```
import pt.c08componentes.s20catalog.s10ds.*;
import pt.c08componentes.s20catalog.s20console.*;
import pt.c08componentes.s20catalog.s30projection.*;

IDataSet dataset = new DataSetComponent();
dataset.setDataSource("../../../db/zombie/zombie-health-spreadsheet.csv");

IProjection projection = new ProjectionComponent();
projection.connect(dataset);
projection.setAttributes(new String[]{"name", "age"});

IConsole console = new ConsoleComponent();
console.connect(projection);

console.update();
```

* <strong>Resultados</strong>

```
=== Attributes ===
name, age

=== Instances ===
Rot Donnadd, 43
Pid Mught, 38
Thulk Lebbimp, 63
Bouvossam Damme, 71
Pirg Zall, 48
Nullon Rackindock, 23
Shor Splitturch, 35
Ger Ackeng, 66
Gleldo Shruck, 45
Nadross Pilch, 60
Sadrent Pemmir, 73
Read Rait, 55
Dallun Whadder, 15
Eapplar Thorg, 25
Blottork Patter, 68
Darrutt Bottall, 75
Gallir Shauch, 20
Dirpe Polnay, 39
Harrimp Fottiem, 65
```

### Tarefa 2

```
import pt.c08componentes.s20catalog.s10ds.*;
import pt.c08componentes.s20catalog.s20console.*;
import pt.c08componentes.s20catalog.s40selection.*;

IDataSet dataset = new DataSetComponent();
dataset.setDataSource("../../../db/zombie/zombie-health-spreadsheet.csv");

ISelection selection = new SelectionComponent();
selection.connect(dataset);
selection.setAttribute("diagnostic");
selection.setOperator("=");
selection.setValue("bacterial_infection");

IConsole console = new ConsoleComponent();
console.connect(selection);

console.update();
```

* <strong>Resultados</strong>

```
=== Attributes ===
name, age, paralysis, yellow_tong, member_loss, chest_pain, trembling_finger, severe_anger, history_bacteria, diagnostic, days_recovery, has_disease

=== Instances ===
Rot Donnadd, 43, t, t, f, f, f, f, f, bacterial_infection, 9, t
Pid Mught, 38, f, t, f, f, f, f, f, bacterial_infection, 7, t
Gleldo Shruck, 45, f, t, f, t, f, f, f, bacterial_infection, 8, t
Read Rait, 55, t, t, f, f, f, f, f, bacterial_infection, 9, t
Dirpe Polnay, 39, f, t, f, f, f, f, f, bacterial_infection, 7, t
```

### Tarefa 3

---
Made with :coffee: by Rafa Mardegan.