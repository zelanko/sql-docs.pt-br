---
title: Comandos com os comandos de computação intermediários parametrizados | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f1675e80522feb0c0b2a46a89dfa6e3bba182198
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47851634"
---
# <a name="parameterized-commands-with-intervening-compute-commands"></a>Comandos parametrizados com comandos COMPUTE de intervenção
Uma forma com parâmetros típica comando APPEND tem uma cláusula que cria um pai **conjunto de registros** com um comando de consulta e outra cláusula que cria um filho **Recordset** com um comando de consulta parametrizada — ou seja, um comando que contém um espaço reservado de parâmetro (um ponto de interrogação, "?"). Em forma resultante **Recordset** tem dois níveis, no qual o pai ocupa o nível superior e o filho ocupa um nível inferior.  
  
 A cláusula que cria o filho **Recordset** pode agora ser um número arbitrário de forma aninhada comandos de computação, em que o comando mais profundamente aninhado contém a consulta parametrizada. Em forma resultante **conjunto de registros** tem vários níveis, na qual o pai ocupa o nível superior, o filho ocupa o nível mais baixo e um número arbitrário de **conjunto de registros**s gerado pelo comandos de computação de forma ocupam os níveis intermediários.  
  
 O uso típico para esse recurso é invocar a função de agregação e as capacidades de agrupamento dos shapeCOMPUTE comandos para criar de intervenção **conjunto de registros** objetos analíticos informações sobre o filho **conjunto de registros** . Além disso, como esse é um comando de forma com parâmetros, cada vez que uma coluna de capítulo do pai é acessada, um novo filho **Recordset** podem ser recuperadas. Como os níveis intermediários são derivados do filho, eles também serão ser recalculados.  
  
## <a name="see-also"></a>Consulte também  
 [Exemplo de data shaping](../../../ado/guide/data/data-shaping-example.md)
