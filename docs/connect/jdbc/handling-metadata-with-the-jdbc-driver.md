---
title: Como tratar metadados com o JDBC Driver | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 5cfb35d4-ddcd-40a2-8091-f29cddc32552
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 859932404e14a9ab1216665d211e1b6734ca9726
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80924685"
---
# <a name="handling-metadata-with-the-jdbc-driver"></a>Tratando metadados com o JDBC Driver
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  O [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] pode ser usado para trabalhar com metadados em um banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de diversas formas. O driver JDBC pode ser usado para obter metadados sobre o banco de dados, um conjunto de resultados ou parâmetros.  
  
 O driver JDBC fornece três classes para recuperar metadados de um banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  
  
-   [SQLServerDatabaseMetaData](../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md), que é usado para retornar informações sobre o banco de dados que está conectado atualmente.  
  
-   [SQLServerResultSetMetaData](../../connect/jdbc/reference/sqlserverresultsetmetadata-class.md), que é usado para retornar informações sobre o conjunto de resultados.  
  
-   [SQLServerParameterMetaData](../../connect/jdbc/reference/sqlserverparametermetadata-class.md), que é usado para retornar informações sobre os parâmetros de instruções preparadas e chamáveis.  
  
 Os tópicos nesta seção descrevem como você pode usar cada uma das três classes de metadados para trabalhar com metadados em um banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
> [!NOTE]  
>  Os métodos de metadados discutidos nesta seção são geralmente caros em termos de desempenho de aplicativo; portanto, tome cuidado com o seu uso.  
  
## <a name="in-this-section"></a>Nesta seção  
  
|Tópico|DESCRIÇÃO|  
|-----------|-----------------|  
|[Como usar metadados de banco de dados](../../connect/jdbc/using-database-metadata.md)|Descreve como recuperar informações de metadados sobre o banco de dados conectado atualmente.|  
|[Como usar metadados do conjunto de resultados](../../connect/jdbc/using-result-set-metadata.md)|Descreve como recuperar informações de metadados sobre o conjunto de resultados atual.|  
|[Como usar metadados de parâmetro](../../connect/jdbc/using-parameter-metadata.md)|Descreve como recuperar informações de metadados sobre os parâmetros de instruções preparadas e chamáveis.|  
  
## <a name="see-also"></a>Confira também  
 [Visão geral do JDBC Driver](../../connect/jdbc/overview-of-the-jdbc-driver.md)  
  
  
