---
title: Usando instruções com procedimentos armazenados | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: jdbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 0041f9e1-09b6-4487-b052-afd636c8e89a
caps.latest.revision: 20
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: bab034ca928d3896328d6c410aed868945241b6f
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="using-statements-with-stored-procedures"></a>Usando instruções com procedimentos armazenados
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Um procedimento armazenado é um procedimento de banco de dados, semelhante a um procedimento em outras linguagens de programação e que está contido no próprio banco de dados. Em [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], procedimentos armazenados podem ser criados usando [!INCLUDE[tsql](../../includes/tsql_md.md)], ou usando o common language runtime (CLR) e outra do Visual Studio linguagens de programação como Visual Basic ou c#. Em geral, [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] procedimentos armazenados podem fazer o seguinte:  
  
-   Aceitar parâmetros de entrada e retornar vários valores no formulário de parâmetros de saída para o procedimento de chamada ou lote.  
  
-   Conter instruções de programação que executam operações no banco de dados, inclusive chamar outros procedimentos.  
  
-   Retornar um valor de status a um procedimento de chamada ou lote para indicar êxito ou falha (e o motivo da falha).  
  
> [!NOTE]  
>  Para obter mais informações sobre [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] procedimentos armazenados, consulte "Compreendendo os procedimentos armazenados" [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Manuais Online.  
  
 Para trabalhar com dados em um [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] banco de dados usando um procedimento armazenado, o [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] fornece o [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md), [SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md), e [ SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) classes. A classe que você vai usar depende da necessidade do parâmetro IN (entrada) ou OUT (saída) para o procedimento armazenado. Se não houver em requer que o procedimento armazenado ou parâmetros de saída, você pode usar a classe SQLServerStatement. Se o procedimento armazenado será chamado várias vezes ou requerer apenas parâmetros IN, você pode usar a classe SQLServerPreparedStatement. Se o procedimento armazenado requer IN e parâmetros de saída, você deve usar a classe SQLServerCallableStatement. É somente quando o procedimento armazenado requer parâmetros de saída que você precisa da sobrecarga de uso da classe SQLServerCallableStatement.  
  
> [!NOTE]  
>  Os procedimentos armazenados também podem retornar contagens de atualização e vários conjuntos de resultados. Para obter mais informações, consulte [usando um procedimento armazenado com uma contagem de atualização](../../connect/jdbc/using-a-stored-procedure-with-an-update-count.md) e [usando vários conjuntos de resultados](../../connect/jdbc/using-multiple-result-sets.md).  
  
 Quando você usa o driver JDBC para chamar um procedimento armazenado com parâmetros, você deve usar o `call` sequência de escape SQL junto com o [prepareCall](../../connect/jdbc/reference/preparecall-method-sqlserverconnection.md) método o [SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md) classe. A sintaxe completa para o `call` sequência de escape é da seguinte maneira:  
  
 `{[?=]call procedure-name[([parameter][,[parameter]]...)]}`  
  
> [!NOTE]  
>  Para obter mais informações sobre o `call` e outros SQL sequências de escape, consulte [usando sequências de Escape SQL](../../connect/jdbc/using-sql-escape-sequences.md).  
  
 Os tópicos nesta seção descrevem as maneiras que você pode chamar [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] procedimentos armazenados usando o driver JDBC e `call` sequência de escape do SQL.  
  
## <a name="in-this-section"></a>Nesta seção  
  
|Tópico|Description|  
|-----------|-----------------|  
|[Usando um procedimento armazenado sem parâmetros](../../connect/jdbc/using-a-stored-procedure-with-no-parameters.md)|Descreve como usar o driver JDBC para executar procedimentos armazenados que não contêm parâmetros de entrada ou saída.|  
|[Usando um procedimento armazenado com parâmetros de entrada](../../connect/jdbc/using-a-stored-procedure-with-input-parameters.md)|Descreve como usar o driver JDBC para executar procedimentos armazenados que contêm parâmetros de entrada.|  
|[Usando um procedimento armazenado com parâmetros de saída](../../connect/jdbc/using-a-stored-procedure-with-output-parameters.md)|Descreve como usar o driver JDBC para executar procedimentos armazenados que contêm parâmetros de saída.|  
|[Usando um procedimento armazenado com um status de retorno](../../connect/jdbc/using-a-stored-procedure-with-a-return-status.md)|Descreve como usar o driver JDBC para executar procedimentos armazenados que contêm valores de status de retorno.|  
|[Usando um procedimento armazenado com uma contagem de atualização](../../connect/jdbc/using-a-stored-procedure-with-an-update-count.md)|Descreve como usar o driver JDBC para executar procedimentos armazenados que retornam contagens de atualização.|  
  
## <a name="see-also"></a>Consulte também  
 [Usando instruções com o JDBC Driver](../../connect/jdbc/using-statements-with-the-jdbc-driver.md)  
  
  
