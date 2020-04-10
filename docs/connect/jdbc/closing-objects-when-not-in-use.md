---
title: Fechando os objetos quando não estão em uso | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: ce8f9b35-c761-4b0c-9a46-985eef2c2e0b
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f1f0c264a7752b296691f20f702ab345f18b1b37
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80922589"
---
# <a name="closing-objects-when-not-in-use"></a>Fechando os objetos quando não estão em uso
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Ao trabalhar com objetos do [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)], particularmente o [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) ou um dos objetos Statement como [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md), [SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) ou [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md), você deverá fechá-los explicitamente usando seus métodos de fechar quando não forem mais necessários. Isto melhora o desempenho liberando recursos de driver e servidor o mais cedo possível, em vez de esperar que o coletor de lixo da Máquina Virtual Java faça isto para você.  
  
 Fechar objetos é particularmente crucial para manter uma boa simultaneidade no servidor quando você está usando bloqueios de rolagem. Os bloqueios de rolagem no último buffer de busca acessado são mantidos até que o conjunto de resultados seja fechado. Da mesma forma, os identificadores de instrução preparados são mantidos até que a instrução seja fechada. Se você estiver reutilizando uma conexão para várias instruções, fechar as instruções antes de deixá-las saírem de escopo permitirá que o servidor limpe os identificadores preparados mais cedo.  
  
## <a name="see-also"></a>Confira também  
 [Melhorando o desempenho e a confiabilidade com o JDBC Driver](../../connect/jdbc/improving-performance-and-reliability-with-the-jdbc-driver.md)  
  
  
