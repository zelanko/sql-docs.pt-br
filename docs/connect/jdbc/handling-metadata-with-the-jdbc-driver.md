---
title: Tratando metadados com o Driver JDBC | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 5cfb35d4-ddcd-40a2-8091-f29cddc32552
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b6fbf435775709ec9890b1c26832b1730f8c6d31
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32829411"
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
  
  
