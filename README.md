# АНАЛИЗ ДАННЫХ И ИСКУССТВЕННЫЙ ИНТЕЛЛЕКТ [in GameDev]
Отчет по лабораторной работе #4 выполнил:
- Колчанов Константин Викторович
- РИ-110949
Отметка о выполнении заданий (заполняется студентом):

| Задание | Выполнение | Баллы |
| ------ | ------ | ------ |
| Задание 1 | * | 60 |
| Задание 2 | * | 20 |
| Задание 3 | # | 20 |


## Цель работы
Познакомиться с перцептроном и реализовать его в проекте Unity.

## Задание 1
### В проекте Unity реализовать перцептрон, который умеет производить вычисления: OR, AND, NAND, XOR. Дать комментарии о корректности работы.

### 1. Создан новый проект.
![Unity](https://sun9-north.userapi.com/sun9-82/s/v1/ig2/F6un6RUpRiSiQ6OS1jAR-Dq-3808gIcGtmQFIkPYqd2kALIwNAbbvhE85MX1FbmEoEYG-CdHGLoyYA1th747EvLM.jpg?size=1031x592&quality=96&type=album)

### 2. Подключен Perceptron.cs.
![Perceptron](https://sun9-west.userapi.com/sun9-11/s/v1/ig2/un4NsVya9A7H5Bk166WmWAFLNFe2FWfYuAb1DY_iM2iSHZ1i-MEkOg4XrGAW7_ymcGS6sYRzSIRbc0zF61GKHR7Y.jpg?size=1280x720&quality=96&type=album)

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

public class Perceptron : MonoBehaviour {

	public TrainingSet[] ts;
	double[] weights = {0,0};
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
		double dp = DotProductBias(weights,ts[i].input);
		if(dp > 0) return(1);
		return (0);
	}

	void InitialiseWeights()
	{
		for(int i = 0; i < weights.Length; i++)
		{
			weights[i] = Random.Range(-1.0f,1.0f);
		}
		bias = Random.Range(-1.0f,1.0f);
	}

	void UpdateWeights(int j)
	{
		double error = ts[j].output - CalcOutput(j);
		totalError += Mathf.Abs((float)error);
		for(int i = 0; i < weights.Length; i++)
		{			
			weights[i] = weights[i] + error*ts[j].input[i]; 
		}
		bias += error;
	}

	double CalcOutput(double i1, double i2)
	{
		double[] inp = new double[] {i1, i2};
		double dp = DotProductBias(weights,inp);
		if(dp > 0) return(1);
		return (0);
	}

	void Train(int epochs)
	{
		InitialiseWeights();
		
		for(int e = 0; e < epochs; e++)
		{
			totalError = 0;
			for(int t = 0; t < ts.Length; t++)
			{
				UpdateWeights(t);
				Debug.Log("W1: " + (weights[0]) + " W2: " + (weights[1]) + " B: " + bias);
			}
			Debug.Log("TOTAL ERROR: " + totalError);
		}
	}

	void Start () {
		Train(8);
		Debug.Log("Test 0 0: " + CalcOutput(0,0));
		Debug.Log("Test 0 1: " + CalcOutput(0,1));
		Debug.Log("Test 1 0: " + CalcOutput(1,0));
		Debug.Log("Test 1 1: " + CalcOutput(1,1));		
	}
	
	void Update () {
		
	}
}

```

### 3. OR.
После настройки Input и Output потребовалось 4 эпохи для полного обучения.
![OR](https://sun9-east.userapi.com/sun9-25/s/v1/ig2/Ao5wXX9c5t7QDiK-BYT2UF4Uj-iKL4UVgAzGDT63ybvwXkvbKMil6qNvBBJ9TGZ7q3D723vSeEpgEBvvzLYxbIRy.jpg?size=1280x691&quality=96&type=album)


### 4. AND.
Обучение заняло 5 эпох, что превышает значение оператора or.
![AND](https://sun9-north.userapi.com/sun9-80/s/v1/ig2/QnoOLPESbOOIZqgV4W6l8HiJyycqfHwtnLL2HEbduQ-xNg2Zd057BMP-is0V7jaUi3Y28iS26aBYmDKMQnwaSBdg.jpg?size=1915x1035&quality=96&type=album)

### 5. NAND.
Обучение безошибочной работе произошло на 7 эпохе.
![NAND](https://sun9-west.userapi.com/sun9-38/s/v1/ig2/X4HMIsQzRc6u-OaZl96132xkdcZY9NlrboPI2QhhKDo6-sFKXznd3_dy2CqQZlM7QrqGEU3zdEbzx-sahjk6uJTw.jpg?size=1917x1038&quality=96&type=album)

### 6. XOR.
За 8 эпох безошибочного результата не произошло, что привело к увеличению показателя Train с 8 до 1000. На 1000 эпохе значение Total Error по прежнему 4.
![XOR](https://sun9-west.userapi.com/sun9-70/s/v1/ig2/j3b1gFIBquoAx0gCTjT2ulQ7FBdNF8bnR4N-fGXYIRUQd4gKyaZX-JKQJ0a23jimXbPLnSWHHH6A_i7qtXr9KcJ8.jpg?size=1917x1040&quality=96&type=album)
![XOR1000]https://sun9-west.userapi.com/sun9-1/s/v1/ig2/nUzlAASTsW3ZMWxCXiJKUOYI6OYnM0IO9E6nqnq9R6qd9FJU3kZXdlnFDBCDY97teCdSZxKHmic5xeLCWS0dpGtf.jpg?size=1917x1037&quality=96&type=album)
![XOR1000](https://sun9-west.userapi.com/sun9-8/s/v1/ig2/3Ef5UTekijLhXQvrT78OxMWmGREEU0rdAmDY-dqYUGOza0bLIzOgl4XfljtnHSaw8PxsoV_zY7MVEfkd49pHUfbe.jpg?size=417x196&quality=96&type=album)


## Задание 2
### Построить графики зависимости количества эпох от ошибки обучения. Указать от чего зависит необходимое количество эпох обучения. 
Для построения используется средний показатель Total Error для каждой эпохи из 4 попыток обучения:

### 1. OR.

![OR](https://sun9-north.userapi.com/sun9-88/s/v1/ig2/ct1dY0zyt3w27X8UNJb6tbNA8eco88GFtjYhsZNyllZZUbV8MRdgEOu9bmTCoAiz5EWjZjt9zFT6m9cd8eEANjdL.jpg?size=1433x757&quality=96&type=album)

### 2. AND.

![AND](https://sun9-east.userapi.com/sun9-25/s/v1/ig2/OLHsq_sWrP-CXTgIYJI9tLpQHAE72PEQV2owquvj9u5SlWOxc3J3KhWzYltS-7ABvug35fOnbO8fTWOcanx_lEuP.jpg?size=1434x755&quality=96&type=album)

### 3. NAND.

![NAND](https://sun9-west.userapi.com/sun9-15/s/v1/ig2/aeqpF8-yNFLFHErl_2oQRa5zvmbIKi-Avfw9fzKZriLBCI2BnKSlumPxsVsp9URuaq4BOhx7FPM1zJvNNFw-_Qmy.jpg?size=1432x750&quality=96&type=album)

### 4. XOR.

![XOR](https://sun9-east.userapi.com/sun9-59/s/v1/ig2/SmERP_ivMLpK07dUN_HNCBLwlgC3m6uOp4P6hUsE3rXCtEgApB4iiy9z8ekHQR1n0P6KlS5glKfgncgdn-Evdwb_.jpg?size=1434x756&quality=96&type=album)

Для обучения операции or потребовалось гораздо меньше эпох, чем and, nand, или же xor. Следовательно количество эпох зависит от сложности операции.


## Задание 3
### Построить визуальную модель работы перцептрона на сцене Unity.


## Выводы
В результате данной лабораторной работы мы ознакомиться с принципами работы перцептрона. Реализовали его в проекте Unity, а также спроектировали визуализацию принципов работы перцептрона при помощи построения графиков зависимости.
