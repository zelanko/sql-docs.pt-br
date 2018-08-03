---
title: JDBC 4.3 conformidade para o JDBC Driver | Microsoft Docs
ms.custom: ''
ms.date: 07/24/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 36025ec0-3c72-4e68-8083-58b38e42d03b
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f529c88044444f3fb6e428b6c69f5a5cf5917251
ms.sourcegitcommit: 6fa72c52c6d2256c5539cc16c407e1ea2eee9c95
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/27/2018
ms.locfileid: "39278907"
---
# <a name="jdbc-43-compliance-for-the-jdbc-driver"></a>Conformidade do JDBC 4.3 com o JDBC Driver
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

    
> [!NOTE]  
>  As versões anteriores ao Microsoft JDBC Driver 6.4 para SQL Server estão em conformidade com as especificações da API do JDBC (Java Database Connectivity) 4.2. Esta seção não se aplica a versões anteriores à versão 6.4.  
  
 A partir da versão 6.4, Microsoft JDBC Driver para SQL Server é o JAVA 10 compatível, mas não é totalmente compatível com as especificações do JDBC 4.3 de API. O driver lançará SQLFeatureNotSupportedException para métodos não implementados. 
 
 Os seguintes métodos de API do JDBC 4.3 são implementados no Microsoft JDBC Driver 6.4 para SQL Server.
 
  **Classe SQLServerConnection**  
  
|Novos métodos|Descrição|Implementação notável|  
|-----------------|-----------------|-------------------------------|  
|void beginRequest()|Dicas para o driver que uma solicitação, uma unidade independente de trabalho, está começando nessa conexão. Para obter mais detalhes, veja [java.sql.Connection](https://docs.oracle.com/javase/9/docs/api/java/sql/Connection.html#beginRequest--).|Salva os valores dos campos de conexão que podem ser modificadas por meio de métodos de API públicos: `databaseAutoCommitMode`, `transactionIsolationLevel`, `networkTimeout`, `holdability`, `sendTimeAsDatetime`, `statementPoolingCacheSize`, `disableStatementPooling`, `serverPreparedStatementDiscardThreshold`, `enablePrepareOnFirstPreparedStatementCall `, `catalogName`, `sqlWarnings`, `useBulkCopyForBatchInsert `.|
|void endRequest()|Dicas para o driver que uma solicitação, uma unidade independente de trabalho, foi concluída. Para obter mais detalhes, confira [java.sql.Connection](https://docs.oracle.com/javase/9/docs/api/java/sql/Connection.html#endRequest--).|Fecha as instruções que são criadas durante a unidade de trabalho e reverte qualquer transação aberta. O método também reverterá as alterações para os campos de conexão que estão listados acima.|