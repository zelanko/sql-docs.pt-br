---
title: Suporte do SQL Server Integration Services para OLTP in-memory | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine-imoltp
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: ea82a9b9-e9ed-4d6f-b3fd-917f6c687ae3
caps.latest.revision: 12
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: d08caf561e3eb0703f9f21cc607d2100d845cea8
ms.contentlocale: pt-br
ms.lasthandoff: 06/22/2017

---
# <a name="sql-server-integration-services-support-for-in-memory-oltp"></a>Suporte do SQL Server Integration Services para OLTP na memória
  Você pode usar uma tabela com otimização de memória, uma exibição que faça referência a tabelas com otimização de memória ou um procedimento armazenado compilado de modo nativo como a origem ou o destino de seu pacote SSIS ( [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] ). É possível usar [ADO NET Source](../../integration-services/data-flow/ado-net-source.md), [OLE DB Source](../../integration-services/data-flow/ole-db-source.md)ou [ODBC Source](../../integration-services/data-flow/odbc-source.md) no fluxo de dados de um pacote SSIS e configurar o componente de origem para recuperar dados de uma tabela com otimização de memória ou uma exibição, ou especificar uma instrução SQL para executar um procedimento armazenado compilado de modo nativo. Da mesma forma, é possível usar [ADO NET Destination](../../integration-services/data-flow/ado-net-destination.md), [OLE DB Destination](../../integration-services/data-flow/ole-db-destination.md)ou [ODBC Destination](../../integration-services/data-flow/odbc-destination.md) para carregar dados em uma tabela com otimização de memória ou em uma exibição, ou especificar uma instrução SQL para executar um procedimento armazenado compilado de modo nativo.  
  
 É possível configurar os componentes de origem e destino mencionados acima em um pacote SSIS para ler e gravar nas tabelas com otimização de memória e em exibições da mesma forma que em outras tabelas e exibições do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . No entanto, é preciso estar ciente dos pontos importantes na seção a seguir ao usar procedimentos armazenados nativamente compilados.  
  
## <a name="invoking-a-natively-compiled-stored-procedure-from-an-ssis-package"></a>Invocando um procedimento armazenado nativamente compilado de um pacote SSIS  
 Para invocar um procedimento armazenado compilado nativamente de um pacote SSIS, é recomendável usar uma Origem ODBC ou um Destino ODBC com uma instrução SQL no formato: **\<nome do procedimento>** sem a palavra-chave **EXEC**. Se você usar a palavra-chave EXEC na instrução SQL, será exibida uma mensagem de erro, pois o gerenciador de conexões ODBC interpreta o texto do comando SQL como uma instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] , e não como um procedimento armazenado, e usa cursores, que não têm suporte para execução de procedimentos armazenados nativamente compilados. O gerenciador de conexões trata a instrução SQL sem a palavra-chave EXEC como uma chamada de procedimento armazenado e não usará um cursor.  
  
 Você também pode usar a Origem ADO .NET e a Origem OLE DB para invocar um procedimento armazenado nativamente compilado, mas é recomendável usar a Origem ODBC. Se você configurar a Origem ADO .NET para executar um procedimento armazenado nativamente compilado, será exibida uma mensagem de erro, pois o provedor de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (SqlClient), que a Origem ADO .NET usa por padrão, não oferece suporte à execução de procedimentos armazenados compilados nativamente. É possível configurar a Origem ADO .NET para usar o Provedor de Dados ODBC, Provedor OLE DB para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]ou [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client. No entanto, observe que a Origem ODBC é mais bem executada do que a Origem ADO .NET com o Provedor de Dados ODBC.  
  
## <a name="see-also"></a>Consulte também  
 [Suporte ao SQL Server para OLTP na memória](../../relational-databases/in-memory-oltp/sql-server-support-for-in-memory-oltp.md)  
  
  
