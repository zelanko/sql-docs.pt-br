---
title: "Fórmulas em consultas de modelo de relatório (Construtor de Relatórios e SSRS) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: report-design
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: "10151"
ms.assetid: fbf68c59-7afc-4afe-bfcd-40ce84629af0
caps.latest.revision: "9"
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 498047a984da8c40cc7b935bf134ee2af2a648f3
ms.sourcegitcommit: 7e117bca721d008ab106bbfede72f649d3634993
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/09/2018
---
# <a name="formulas-in-report-model-queries-report-builder-and-ssrs"></a>Fórmulas em consultas de modelo de relatório (Construtor de Relatórios e SSRS)
  Fórmulas são cálculos executados em valores em um relatório que usam um modelo de relatório como uma fonte de dados. Você define fórmulas na **Caixa de Diálogo Definir Forma** no Designer de Consultas de Modelo de Relatório quando define uma consulta para uma fonte de dados de modelo de relatório. Uma fórmula pode conter funções, operadores, constantes e referências a campos ou entidades. As fórmulas permitem combinar, agregar, filtrar e avaliar dados numéricos e de texto. É possível criar fórmulas e salvá-las como novos campos ou modificar as fórmulas de campos existentes.  
  
 Fórmulas não são expressões RDL e não começam com um sinal de igual (=). Para obter mais informações sobre expressões RDL, consulte [Expressões &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/expressions-report-builder-and-ssrs.md).  
  
 As fórmulas podem ser parecidas com uma das seguintes:  
  
-   **Sum Line Total**  
  
-   6+12  
  
-   **SUM**(**IF**(**Finished Goods Flag**, "Finished", "Unfinished"))  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="references"></a>Referências  
 Uma referência é um nome de campo. Pode ser um nome de campo existente dentro da entidade ou um nome de campo calculado que você criou e adicionou à lista Campos. A referência indica ao Construtor de Relatórios onde procurar os valores ou dados a serem usados em uma fórmula. Você pode consultar campos dentro da entidade de contexto e em outras entidades dentro de uma fórmula, ou usar o valor de um campo em várias fórmulas.  
  
 Quando você usa referências, o processador de relatórios executa a fórmula para cada valor dentro do campo. Por exemplo, suponha que um campo contenha o total de vendas anual dos últimos cinco anos. Esse campo contém cinco valores, cada um representando o total de vendas para um determinado ano. Se a fórmula contiver uma referência para esse campo, ela calculará o novo valor usando cada valor individual.  
  
## <a name="operators"></a>Operadores  
 Os operadores especificam o tipo de cálculo que você deseja realizar nos valores de uma fórmula. Há três tipos diferentes de operadores de cálculo: aritmético, de comparação e de texto. Os operadores são indicados usando símbolos, como o sinal de mais (+).  
  
 **Operadores Aritméticos.** Os operadores aritméticos realizam operações matemáticas básicas, como soma, subtração ou multiplicação, combinam números e produzem resultados numéricos.  
  
 **Operadores de Comparação.** É possível comparar dois valores usando os operadores de comparação. Quando dois valores são comparados usando esses operadores, o resultado é um valor lógico TRUE ou FALSE.  
  
 **Operador de Concatenação de Texto.** Use o E comercial (&) para unir ou concatenar uma ou mais cadeias de caracteres de texto para produzir um só texto.  
  
##  <a name="Constants"></a> Constantes  
 Uma constante é um valor que não é calculado e, assim, não se altera. O Construtor de Relatórios usa as seguintes constantes: **True**, **False**e **Empty**. Essas constantes são usadas para avaliar campos Boolianos. Por exemplo, suponha que exista um campo chamado IsDiscontinued. Os únicos valores válidos para esse campo são True, False ou Empty (" ").  
  
##  <a name="Functions"></a> Funções  
 Funções são fórmulas predefinidas que realizam cálculos usando valores específicos, chamados de *argumentos*, especificados em um pedido específico. Os argumentos podem ser valores literais ou campos, ou combinações de ambos. Quando são usados campos em fórmulas, o nome do campo representa cada instância do campo. Se o argumento for um valor literal, é provável que seja necessário indicar que o argumento é um valor literal usando caracteres específicos.  
  
 Elas podem ser utilizadas para realizar cálculos simples ou complexos. A estrutura de uma função começa com seu nome, seguido de um parêntese de abertura, dos argumentos da função separados por vírgulas e de um parêntese de fechamento.  
  
 ![Um exemplo de uma função.] (../../reporting-services/report-design/media/functionexample.gif "Um exemplo de uma função.")  
  
 Os argumentos podem ser referências de campo, números, texto e valores lógicos, como **TRUE** ou **FALSE**. Eles também podem ser constantes, fórmulas ou outras funções. Os argumentos que você digita devem gerar um valor válido para o argumento. Por exemplo, se a fórmula multiplica dois inteiros, o resultado não pode ser uma cadeia de caracteres de texto.  
  
 O Construtor de Relatórios vem com as seguintes categorias de funções comumente usadas:  
  
|||  
|-|-|  
|Funções de agregação|**AVG**, **COUNT**, **COUNTDISTINCT**, **MAX**, **MIN**, **STDEV**, **STDEVP**, **SUM**, **VAR**, **VARP**|  
|Funções condicionais|**IF**, **IN**, **SWITCH**|  
|Funções de conversão|**INT**, **DECIMAL**, **FLOAT**, **TEXT**|  
|Funções de data e hora|**DATE**, **DATEADD**, **DATEDIFF**, **DATETIME**, **DATEONLY**, **DAY**, **DAYOFWEEK**, **DAYOFYEAR**, **HOUR**, **MINUTE**, **MONTH**, **NOW**, **QUARTER**, **SECOND**, **TIMEONLY**, **TODAY**, **WEEK**, **YEAR**|  
|Funções informativas|**GETUSERCULTURE**, **GETUSERID**|  
|Funções lógicas|**AND**, **NOT**, **OR**|  
|Funções matemáticas|**MOD**, **ROUND**, **TRUNC**|  
|Operadores|Adicionar (+), Dividir (/), Igual a (=), Exponenciação (^), Maior que (>;), Maior que ou igual a (>=), Menor que (<), Menor que ou igual a (<=), Multiplicar (*), Negar (-), Diferente de (<>), Subtrair (-)|  
|Funções de texto|**CONCAT**, **FIND**, **LEFT**, **LENGTH**, **LOWER**, **LTRIM**, **REPLACE**, **RIGHT**, **RTRIM**, **SUBSTRING**, **UPPER**|  
  
  
