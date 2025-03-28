# DA-in-GameDev-lab4
# Отчет по лабораторной работе #4 выполнил(а):
- Аржавицин Захар Денисович
- НМТ-233929

## Отметка о выполнении заданий (заполняется студентом):

| Задание | Выполнение | Баллы |
| ------ | ------ | ------ |
| Задание 1 | * | 60 |
| Задание 2 | * | 20 |
| Задание 3 | * | 20 |

Знак "*" - задание выполнено; знак "#" - задание не выполнено;

Работу проверили:
- к.т.н., доцент Денисов Д.В.
- к.э.н., доцент Панов М.А.
- ст. преп., Фадеев В.О.
- 
---

## Цель работы

Ознакомиться с основами работы с Unity и реализацией простейшего перцептрона.

---

## Задание 1
### Создание пустого проекта в Unity и добавление объекта Perceptron

Шаги выполнения:
1. Создан новый проект в Unity.
2. Добавлен пустой GameObject с именем `Perceptron`.
3. Создан и подключен скрипт `Perceptron.cs`.

---

## Задание 2
### Реализация и обучение перцептрона
Код реализации:
```csharp
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

[System.Serializable]
public class TrainingSet
{
    public double[] input;
    public double output;
}

public class Perceptron : MonoBehaviour
{

    public TrainingSet[] ts;
    double[] weights = { 0, 0 };
    double bias = 0;
    double totalError = 0;

    double DotProductBias(double[] v1, double[] v2)
    {
        if (v1 == null || v2 == null)
            return -1;

        if (v1.Length != v2.Length)
            return -1;

        double d = 0;
        for (int x = 0; x < v1.Length; x++)
        {
            d += v1[x] * v2[x];
        }

        d += bias;

        return d;
    }

    double CalcOutput(int i)
    {
        double dp = DotProductBias(weights, ts[i].input);
        if (dp > 0) return (1);
        return (0);
    }

    void InitialiseWeights()
    {
        for (int i = 0; i < weights.Length; i++)
        {
            weights[i] = Random.Range(-1.0f, 1.0f);
        }
        bias = Random.Range(-1.0f, 1.0f);
    }

    void UpdateWeights(int j)
    {
        double error = ts[j].output - CalcOutput(j);
        totalError += Mathf.Abs((float)error);
        for (int i = 0; i < weights.Length; i++)
        {
            weights[i] = weights[i] + error * ts[j].input[i];
        }
        bias += error;
    }

    double CalcOutput(double i1, double i2)
    {
        double[] inp = new double[] { i1, i2 };
        double dp = DotProductBias(weights, inp);
        if (dp > 0) return (1);
        return (0);
    }

    void Train(int epochs)
    {
        InitialiseWeights();

        for (int e = 0; e < epochs; e++)
        {
            totalError = 0;
            for (int t = 0; t < ts.Length; t++)
            {
                UpdateWeights(t);
                Debug.Log("W1: " + (weights[0]) + " W2: " + (weights[1]) + " B: " + bias);
            }
            Debug.Log("TOTAL ERROR: " + totalError);
        }
    }

    void Start()
    {
        Train(8);
        Debug.Log("Test 0 0: " + CalcOutput(0, 0));
        Debug.Log("Test 0 1: " + CalcOutput(0, 1));
        Debug.Log("Test 1 0: " + CalcOutput(1, 0));
        Debug.Log("Test 1 1: " + CalcOutput(1, 1));
    }

    void Update()
    {

    }
}
```

---

## Задание 3
### Оформление отчета на GitHub

Ссылка на репозиторий: https://github.com/FUploZE/DA-in-GameDev-lab4

---

## Выводы
В ходе выполнения лабораторной работы:
- Был создан новый проект в Unity.
- Был реализован простой перцептрон, обучающийся на примере логической функции AND.
- Перцептрон успешно обучился, и результаты тестов показали корректную работу модели.
- Отчет оформлен в виде документации на GitHub с использованием Markdown.
