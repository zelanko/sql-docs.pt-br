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
ms.openlocfilehash: 9e892aed72ba1d74f9bdafc319c71a39546f4402
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63302477"
---
# <a name="parameterized-commands-with-intervening-compute-commands"></a>Comandos parametrizados com comandos COMPUTE de intervenção
Uma forma com parâmetros típica comando APPEND tem uma cláusula que cria um pai **conjunto de registros** com um comando de consulta e outra cláusula que cria um filho **Recordset** com um comando de consulta parametrizada - ou seja, um comando que contém um espaço reservado de parâmetro (um ponto de interrogação, "?"). Em forma resultante **Recordset** tem dois níveis, no qual o pai ocupa o nível superior e o filho ocupa um nível inferior.  
  
 A cláusula que cria o filho **Recordset** pode agora ser um número arbitrário de forma aninhada comandos de computação, em que o comando mais profundamente aninhado contém a consulta parametrizada. Em forma resultante **conjunto de registros** tem vários níveis, na qual o pai ocupa o nível superior, o filho ocupa o nível mais baixo e um número arbitrário de **conjunto de registros**s gerado pelo comandos de computação de forma ocupam os níveis intermediários.  
  
 O uso típico para esse recurso é invocar a função de agregação e as capacidades de agrupamento dos shapeCOMPUTE comandos para criar de intervenção **conjunto de registros** objetos analíticos informações sobre o filho **conjunto de registros** . Além disso, como esse é um comando de forma com parâmetros, cada vez que uma coluna de capítulo do pai é acessada, um novo filho **Recordset** podem ser recuperadas. Como os níveis intermediários são derivados do filho, eles também serão ser recalculados.  
  
## <a name="see-also"></a>Consulte também  
 [Exemplo de data shaping](../../../ado/guide/data/data-shaping-example.md)
