---
title: Comandos com parâmetros com comandos de computação intermediários | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- data shaping [ADO], parameterized commands
- parameterized commands [ADO]
- APPEND clause [ADO]
- COMPUTE command [ADO]
ms.assetid: 732f624f-8900-4608-9815-194302d22e8b
author: rothja
ms.author: jroth
ms.openlocfilehash: 6f66bde29a5036ed671f9af17bf5aab1df4acbca
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2020
ms.locfileid: "82764777"
---
# <a name="parameterized-commands-with-intervening-compute-commands"></a>Comandos parametrizados com comandos COMPUTE de intervenção
Um comando típico de acrescentar forma com parâmetros tem uma cláusula que cria um **conjunto de registros** pai com um comando de consulta e outra cláusula que cria um **conjunto de registros** filho com um comando de consulta parametrizada, ou seja, um comando que contém um espaço reservado de parâmetro (um ponto de interrogação, "?"). O conjunto de **registros** moldado resultante tem dois níveis, nos quais o pai ocupa o nível superior e o filho ocupa o nível inferior.  
  
 A cláusula que cria o **conjunto de registros** filho agora pode ser um número arbitrário de comandos de computação de forma aninhada, em que o comando aninhado mais profundamente contém a consulta parametrizada. O conjunto de **registros** moldado resultante tem vários níveis, nos quais o pai ocupa o nível superior, o filho ocupa o nível lowermost e um número arbitrário de **conjuntos de registros**s gerados pelos comandos de computação de forma ocupam os níveis intermediários.  
  
 O uso típico para esse recurso é invocar a função de agregação e agrupar capacidades de comandos shapeCOMPUTE para criar objetos de **conjunto de registros** intermediários com informações analíticas sobre o **conjunto de registros**filho. Além disso, como esse é um comando de forma com parâmetros, cada vez que uma coluna de capítulo do pai é acessada, um novo **conjunto de registros** filho pode ser recuperado. Como os níveis intermediários são derivados do filho, eles também serão recomputados.  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo de data shaping](../../../ado/guide/data/data-shaping-example.md)
