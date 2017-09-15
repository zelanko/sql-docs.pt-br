---
title: "Fechando objetos quando não estiver em uso | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: ce8f9b35-c761-4b0c-9a46-985eef2c2e0b
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: e742eeca533633d1055315a14b1c4f76c061be81
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="closing-objects-when-not-in-use"></a>Fechando os objetos quando não estão em uso
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Quando você trabalha com objetos de [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)], particularmente o [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) ou uma instrução como objetos [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md), [SQLServerPreparedStatement ](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) ou [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md), você deverá fechá-los explicitamente usando os métodos fechar quando eles não são mais necessários. Isto melhora o desempenho liberando recursos de driver e servidor o mais cedo possível, em vez de esperar que o coletor de lixo da Máquina Virtual Java faça isto para você.  
  
 Fechar objetos é particularmente crucial para manter uma boa simultaneidade no servidor quando você está usando bloqueios de rolagem. Os bloqueios de rolagem no último buffer de busca acessado são mantidos até que o conjunto de resultados seja fechado. Da mesma forma, os identificadores de instrução preparados são mantidos até que a instrução seja fechada. Se você estiver reutilizando uma conexão para várias instruções, fechar as instruções antes de deixá-las saírem de escopo permitirá que o servidor limpe os identificadores preparados mais cedo.  
  
## <a name="see-also"></a>Consulte também  
 [Melhorando o desempenho e a confiabilidade com o JDBC Driver](../../connect/jdbc/improving-performance-and-reliability-with-the-jdbc-driver.md)  
  
  
