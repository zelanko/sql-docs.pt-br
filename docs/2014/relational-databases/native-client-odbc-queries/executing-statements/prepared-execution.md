---
title: Execução preparada | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- deferred statement preparation
- prepared execution [ODBC]
- SQLPrepare function
- ODBC applications, statements
- SQLExecute function
- statements [ODBC], prepared execution
ms.assetid: f3a9d32b-6cd7-4f0c-b38d-c8ccc4ee40c3
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 01982222ba5a18086aeadbbec776cba222f0e235
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "68207055"
---
# <a name="prepared-execution"></a>Execução preparada
  A API do ODBC define a execução preparada como um modo de reduzir a sobrecarga de análise e compilação associada à execução repetida da instrução [!INCLUDE[tsql](../../../includes/tsql-md.md)]. O aplicativo compila uma cadeia de caracteres que contém uma instrução SQL e então a executa em duas fases. Ele chama a [função SQLPrepare](https://go.microsoft.com/fwlink/?LinkId=59360) uma vez para que a instrução seja analisada e compilada em um [!INCLUDE[ssDE](../../../includes/ssde-md.md)]plano de execução pelo. Em seguida, ele chama **SQLExecute** para cada execução do plano de execução preparado. Dessa forma, a sobrecarga de análise e compilação é salva em cada execução. A execução preparada geralmente é usada através de aplicativos para executar a mesma instrução SQL com parâmetros várias vezes.  
  
 Para a maioria dos bancos de dados, a execução preparada é mais rápida que a direta para instruções executadas mais de três ou quatro vezes primariamente, pois a instrução é compilada somente uma vez, enquanto instruções executadas diretamente são compiladas sempre que ocorrem. A execução preparada também pode fornecer uma redução no tráfego de rede, pois o driver pode enviar um identificador do plano de execução e os valores de parâmetro, em vez de toda uma instrução SQL, para a fonte de dados sempre que a instrução for executada.  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]reduz a diferença de desempenho entre a execução direta e preparada por meio de algoritmos aprimorados para detectar e reutilizar planos de execução de **SQLExecDirect**. Isso torna alguns dos benefícios de desempenho da execução preparada disponíveis para instruções executadas diretamente. Para obter mais informações, consulte [execução direta](direct-execution.md).  
  
 O [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] também oferece suporte nativo para execução preparada. Um plano de execução é criado em **SQLPrepare** e executado posteriormente quando **SQLExecute** é chamado. Como [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] o não é necessário para criar procedimentos armazenados temporários em **SQLPrepare**, não há nenhuma sobrecarga extra nas tabelas do sistema em **tempdb**.  
  
 Por motivos de desempenho, a preparação da instrução é adiada até que **SQLExecute** seja chamado ou uma operação de metapropriedade (como [SQLDescribeCol](../../native-client-odbc-api/sqldescribecol.md) ou [SQLDescribeParam](../../native-client-odbc-api/sqldescribeparam.md) no ODBC) seja executada. Esse é o comportamento padrão. Não são conhecidos erros na instrução que está sendo preparada até que ela seja executada ou uma operação de metapropriedade seja executada. Definir o atributo da instrução específica do driver ODBC do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client SQL_SOPT_SS_DEFER_PREPARE como SQL_DP_OFF pode desativar esse comportamento padrão.  
  
 No caso da preparação adiada, chamar **SQLDescribeCol** ou **SQLDescribeParam** antes de chamar **SQLExecute** gera um ida e volta extra para o servidor. No **SQLDescribeCol**, o driver remove a cláusula WHERE da consulta e a envia ao servidor com SET FMTONLY on para obter a descrição das colunas no primeiro conjunto de resultados retornado pela consulta. No **SQLDescribeParam**, o driver chama o servidor para obter uma descrição das expressões ou colunas referenciadas por quaisquer marcadores de parâmetro na consulta. Esse método também tem algumas restrições, como não poder resolver parâmetros em subconsultas.  
  
 O uso excessivo de **SQLPrepare** com [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] o driver ODBC do Native Client degrada o desempenho, especialmente quando conectado a versões anteriores do SQL Server. A execução preparada não deve ser usada para instruções executadas uma única vez. A execução preparada é mais lenta que a direta para uma única execução de instrução, pois ela requer uma viagem de ida e volta extra do cliente ao servidor. Em versões anteriores do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], ela também gera um procedimento armazenado temporário.  
  
 As instruções preparadas não podem ser usadas para criar objetos temporários no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 Alguns aplicativos ODBC iniciais usaram **SQLPrepare** sempre que [SQLBindParameter](../../native-client-odbc-api/sqlbindparameter.md) foi usado. **SQLBindParameter** não requer o uso de **SQLPrepare**, ele pode ser usado com **SQLExecDirect**. Por exemplo, use **SQLExecDirect** com **SQLBindParameter** para recuperar o código de retorno ou os parâmetros de saída de um procedimento armazenado que é executado apenas uma vez. Não use o **SQLPrepare** com **SQLBindParameter** , a menos que a mesma instrução seja executada várias vezes.  
  
## <a name="see-also"></a>Consulte Também  
 [Executando instruções &#40;&#41;ODBC](executing-statements-odbc.md)  
  
  
