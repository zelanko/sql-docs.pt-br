---
title: "Usando as instruções com o Driver JDBC | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 7f8f3e8f-841e-4449-9154-b5366870121f
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 5e4cbbfc9d2b73d0a7c79ebc2791f588a7c8f862
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="using-statements-with-the-jdbc-driver"></a>Usando instruções com o JDBC Driver
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  O [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] pode ser usado para trabalhar com dados em um [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] banco de dados de várias maneiras. O driver JDBC pode ser usado para executar instruções SQL no banco de dados ou pode ser usado para chamar procedimentos armazenados no banco de dados, usando parâmetros de entrada e saída. O driver JDBC também dá suporte ao uso de sequências de escape de SQL, contagens de atualização, chaves automaticamente geradas e realização de atualizações dentro de uma operação de lote.  
  
 O driver JDBC fornece três classes para recuperar dados de um [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] banco de dados:  
  
1.  [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md) - usado para executar instruções SQL sem parâmetros.  
  
2.  [SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) - (herdado de SQLServerStatement), usado para executar instruções SQL compiladas que podem conter parâmetros IN.  
  
3.  [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) - (herdado de SQLServerPreparedStatement), usado para executar procedimentos armazenados que podem conter parâmetros IN, parâmetros OUT ou ambos.  
  
 Os tópicos desta seção discutem como você pode usar cada uma das três classes de instrução para trabalhar com dados em um [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] banco de dados.  
  
## <a name="in-this-section"></a>Nesta seção  
  
|Tópico|Description|  
|-----------|-----------------|  
|[Usando instruções com SQL](../../connect/jdbc/using-statements-with-sql.md)|Descreve como usar instruções SQL com o driver JDBC para trabalhar com dados em um [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] banco de dados.|  
|[Usando instruções com procedimentos armazenados](../../connect/jdbc/using-statements-with-stored-procedures.md)|Descreve como usar procedimentos armazenados com o driver JDBC para trabalhar com dados em um [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] banco de dados.|  
|[Usando vários conjuntos de resultados](../../connect/jdbc/using-multiple-result-sets.md)|Descreve como usar o driver JDBC para recuperar dados de vários conjuntos de resultados.|  
|[Usando sequências de escape do SQL](../../connect/jdbc/using-sql-escape-sequences.md)|Descreve como usar sequências de escape de SQL, como literais e funções de data e hora.|  
|[Usando chaves geradas automaticamente](../../connect/jdbc/using-auto-generated-keys.md)|Descreve como usar chaves automaticamente geradas.|  
|[Executando operações em lote](../../connect/jdbc/performing-batch-operations.md)|Descreve como usar o driver JDBC para realizar operações em lote.|  
|[Tratando instruções complexas](../../connect/jdbc/handling-complex-statements.md)|Descreve como usar o driver JDBC para executar instruções complexas que realizam uma variedade de tarefas e podem retornar tipos diferentes de dados.|  
  
## <a name="see-also"></a>Consulte também  
 [Visão geral do JDBC Driver](../../connect/jdbc/overview-of-the-jdbc-driver.md)  
  
  
