---
title: Usando instruções com procedimentos armazenados | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 0041f9e1-09b6-4487-b052-afd636c8e89a
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 2dd4ead601700baefaf356840fba4184ab427ef2
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66798551"
---
# <a name="using-statements-with-stored-procedures"></a>Usando instruções com procedimentos armazenados

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

Um procedimento armazenado é um procedimento de banco de dados, semelhante a um procedimento em outras linguagens de programação e que está contido no próprio banco de dados. No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], os procedimentos armazenados podem ser criados com o uso de [!INCLUDE[tsql](../../includes/tsql-md.md)] ou CLR (Common Language Runtime) e uma das linguagens de programação do Visual Studio, como Visual Basic ou C#. Em geral, os procedimentos armazenados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] podem fazer o seguinte:  
  
- Aceitar parâmetros de entrada e retornar vários valores no formulário de parâmetros de saída para o procedimento de chamada ou lote.  
  
- Conter instruções de programação que executam operações no banco de dados, inclusive chamar outros procedimentos.  
  
- Retornar um valor de status a um procedimento de chamada ou lote para indicar êxito ou falha (e o motivo da falha).  
  
> [!NOTE]  
> Para obter mais informações sobre os procedimentos armazenados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], veja "Compreendendo os procedimentos armazenados" nos Manuais Online do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
Para trabalhar com os dados em um banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando um procedimento armazenado, o [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] fornece as classes [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md), [SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) e [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md). A classe que você vai usar depende da necessidade do parâmetro IN (entrada) ou OUT (saída) para o procedimento armazenado. Se o procedimento armazenado não exigir o parâmetro IN ou OUT, você poderá usar a classe SQLServerStatement; se o procedimento armazenado será chamado várias vezes, ou se ele exigir apenas parâmetros IN, você poderá usar a classe SQLServerPreparedStatement. Se o procedimento armazenado requer IN e os parâmetros de saída, você deve usar a classe SQLServerCallableStatement. Somente quando o procedimento armazenado requer parâmetros OUT você precisará da sobrecarga de usar a classe SQLServerCallableStatement.  
  
> [!NOTE]  
> Os procedimentos armazenados também podem retornar contagens de atualização e vários conjuntos de resultados. Para obter mais informações, consulte [usando um procedimento armazenado com uma contagem de atualização](../../connect/jdbc/using-a-stored-procedure-with-an-update-count.md) e [usando vários conjuntos de resultados](../../connect/jdbc/using-multiple-result-sets.md).  
  
Ao usar o driver JDBC para chamar um procedimento armazenado com parâmetros, você deve usar a sequência de escape do SQL `call` junto com o método [prepareCall](../../connect/jdbc/reference/preparecall-method-sqlserverconnection.md) da classe [SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md). A sintaxe completa da sequência de escape `call` é a seguinte:  
  
 `{[?=]call procedure-name[([parameter][,[parameter]]...)]}`  
  
> [!NOTE]  
> Para obter mais informações sobre o `call` e outro SQL sequências de escape, consulte [sequências de Escape de SQL usando](../../connect/jdbc/using-sql-escape-sequences.md).  
  
Os tópicos desta seção descrevem as maneiras de chamar procedimentos armazenados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando o driver JDBC e a sequência de escape `call` do SQL.  
  
## <a name="in-this-section"></a>Nesta seção  
  
|Tópico|Descrição|  
|-----------|-----------------|  
|[Usando um procedimento armazenado sem parâmetros](../../connect/jdbc/using-a-stored-procedure-with-no-parameters.md)|Descreve como usar o driver JDBC para executar procedimentos armazenados que não contêm parâmetros de entrada ou saída.|  
|[Usando um procedimento armazenado com parâmetros de entrada](../../connect/jdbc/using-a-stored-procedure-with-input-parameters.md)|Descreve como usar o driver JDBC para executar procedimentos armazenados que contêm parâmetros de entrada.|  
|[Usando um procedimento armazenado com parâmetros de saída](../../connect/jdbc/using-a-stored-procedure-with-output-parameters.md)|Descreve como usar o driver JDBC para executar procedimentos armazenados que contêm parâmetros de saída.|  
|[Usando um procedimento armazenado com um status de retorno](../../connect/jdbc/using-a-stored-procedure-with-a-return-status.md)|Descreve como usar o driver JDBC para executar procedimentos armazenados que contêm valores de status de retorno.|  
|[Usando um procedimento armazenado com uma contagem de atualização](../../connect/jdbc/using-a-stored-procedure-with-an-update-count.md)|Descreve como usar o driver JDBC para executar procedimentos armazenados que retornam contagens de atualização.|  
  
## <a name="see-also"></a>Consulte Também

[Usando instruções com o JDBC Driver](../../connect/jdbc/using-statements-with-the-jdbc-driver.md)  
