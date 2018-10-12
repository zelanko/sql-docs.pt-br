---
title: Fechando os objetos quando não estiver em uso | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: ce8f9b35-c761-4b0c-9a46-985eef2c2e0b
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 47ad0a6d69ccf19b34ff0e15e7afa39b2dfcce41
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47687415"
---
# <a name="closing-objects-when-not-in-use"></a>Fechando os objetos quando não estão em uso
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Ao trabalhar com objetos do [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)], particularmente o [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) ou um dos objetos Statement como [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md), [SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) ou [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md), você deverá fechá-los explicitamente usando seus métodos de fechar quando não forem mais necessários. Isto melhora o desempenho liberando recursos de driver e servidor o mais cedo possível, em vez de esperar que o coletor de lixo da Máquina Virtual Java faça isto para você.  
  
 Fechar objetos é particularmente crucial para manter uma boa simultaneidade no servidor quando você está usando bloqueios de rolagem. Os bloqueios de rolagem no último buffer de busca acessado são mantidos até que o conjunto de resultados seja fechado. Da mesma forma, os identificadores de instrução preparados são mantidos até que a instrução seja fechada. Se você estiver reutilizando uma conexão para várias instruções, fechar as instruções antes de deixá-las saírem de escopo permitirá que o servidor limpe os identificadores preparados mais cedo.  
  
## <a name="see-also"></a>Consulte Também  
 [Melhorando o desempenho e a confiabilidade com o JDBC Driver](../../connect/jdbc/improving-performance-and-reliability-with-the-jdbc-driver.md)  
  
  
