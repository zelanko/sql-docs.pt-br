---
title: Tratando metadados com o Driver JDBC | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 5cfb35d4-ddcd-40a2-8091-f29cddc32552
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 63d691c8bef93ad734a7596532ba567708128a2d
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="handling-metadata-with-the-jdbc-driver"></a>Tratando metadados com o JDBC Driver
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  O [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] pode ser usado para trabalhar com metadados em um [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] banco de dados de várias maneiras. O driver JDBC pode ser usado para obter metadados sobre o banco de dados, um conjunto de resultados ou parâmetros.  
  
 O driver JDBC fornece três classes para recuperar metadados de um [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] banco de dados:  
  
-   [SQLServerDatabaseMetaData](../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md), que é usada para retornar informações sobre o banco de dados que está conectado no momento.  
  
-   [SQLServerResultSetMetaData](../../connect/jdbc/reference/sqlserverresultsetmetadata-class.md), que é usada para retornar informações sobre o conjunto de resultados.  
  
-   [SQLServerParameterMetaData](../../connect/jdbc/reference/sqlserverparametermetadata-class.md), que é usada para retornar informações sobre os parâmetros de instruções preparadas e chamáveis.  
  
 Os tópicos nesta seção descrevem como você pode usar cada uma das três classes de metadados para trabalhar com metadados em um [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] banco de dados.  
  
> [!NOTE]  
>  Os métodos de metadados discutidos nesta seção são geralmente caros em termos de desempenho de aplicativo; portanto, tome cuidado com o seu uso.  
  
## <a name="in-this-section"></a>Nesta seção  
  
|Tópico|Description|  
|-----------|-----------------|  
|[Usando metadados de banco de dados](../../connect/jdbc/using-database-metadata.md)|Descreve como recuperar informações de metadados sobre o banco de dados conectado atualmente.|  
|[Usando metadados de conjunto de resultados](../../connect/jdbc/using-result-set-metadata.md)|Descreve como recuperar informações de metadados sobre o conjunto de resultados atual.|  
|[Usando metadados de parâmetro](../../connect/jdbc/using-parameter-metadata.md)|Descreve como recuperar informações de metadados sobre os parâmetros de instruções preparadas e chamáveis.|  
  
## <a name="see-also"></a>Consulte também  
 [Visão geral do JDBC Driver](../../connect/jdbc/overview-of-the-jdbc-driver.md)  
  
  

