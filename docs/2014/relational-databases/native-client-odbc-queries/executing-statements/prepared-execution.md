---
title: A execução preparada | Microsoft Docs
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
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "68207055"
---
# <a name="prepared-execution"></a>Execução preparada
  A API do ODBC define a execução preparada como um modo de reduzir a sobrecarga de análise e compilação associada à execução repetida da instrução [!INCLUDE[tsql](../../../includes/tsql-md.md)]. O aplicativo compila uma cadeia de caracteres que contém uma instrução SQL e então a executa em duas fases. Ele chama [SQLPrepare Function](https://go.microsoft.com/fwlink/?LinkId=59360) uma vez para que a instrução seja analisada e compilada no plano de execução pelo [!INCLUDE[ssDE](../../../includes/ssde-md.md)]. Em seguida, ele chama **SQLExecute** para cada execução do plano de execução preparada. Dessa forma, a sobrecarga de análise e compilação é salva em cada execução. A execução preparada geralmente é usada através de aplicativos para executar a mesma instrução SQL com parâmetros várias vezes.  
  
 Para a maioria dos bancos de dados, a execução preparada é mais rápida que a direta para instruções executadas mais de três ou quatro vezes primariamente, pois a instrução é compilada somente uma vez, enquanto instruções executadas diretamente são compiladas sempre que ocorrem. A execução preparada também pode fornecer uma redução no tráfego de rede, pois o driver pode enviar um identificador do plano de execução e os valores de parâmetro, em vez de toda uma instrução SQL, para a fonte de dados sempre que a instrução for executada.  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] reduz a diferença de desempenho entre execução preparada e a direta por meio de algoritmos aprimorados para detectar e reutilizar planos de execução de **SQLExecDirect**. Isso torna alguns dos benefícios de desempenho da execução preparada disponíveis para instruções executadas diretamente. Para obter mais informações, consulte [execução direta](direct-execution.md).  
  
 O [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] também oferece suporte nativo para execução preparada. Um plano de execução se baseia **SQLPrepare** e depois executado quando **SQLExecute** é chamado. Porque [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] não é necessário para criar procedimentos armazenados temporários no **SQLPrepare**, não há nenhuma sobrecarga extra nas tabelas do sistema **tempdb**.  
  
 Por motivos de desempenho, a preparação da instrução é adiada até **SQLExecute** é chamado ou uma operação de metapropriedade (como [SQLDescribeCol](../../native-client-odbc-api/sqldescribecol.md) ou [SQLDescribeParam](../../native-client-odbc-api/sqldescribeparam.md)no ODBC) é executada. Esse é o comportamento padrão. Não são conhecidos erros na instrução que está sendo preparada até que ela seja executada ou uma operação de metapropriedade seja executada. Definir o atributo da instrução específica do driver ODBC do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client SQL_SOPT_SS_DEFER_PREPARE como SQL_DP_OFF pode desativar esse comportamento padrão.  
  
 No caso de adiamento preparação, chamar **SQLDescribeCol** ou **SQLDescribeParam** antes de chamar **SQLExecute** gera uma ida e volta extra ao servidor. Na **SQLDescribeCol**, o driver remove a cláusula WHERE da consulta e o envia para o servidor com SET FMTONLY ON para obter a descrição das colunas no primeiro conjunto de resultados retornado pela consulta. Na **SQLDescribeParam**, o driver chama o servidor para obter uma descrição das expressões ou colunas referenciadas por qualquer marcador de parâmetro na consulta. Esse método também tem algumas restrições, como não poder resolver parâmetros em subconsultas.  
  
 Uso excessivo de **SQLPrepare** com o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] driver ODBC Native Client degrada o desempenho, especialmente quando conectado a versões anteriores do SQL Server. A execução preparada não deve ser usada para instruções executadas uma única vez. A execução preparada é mais lenta que a direta para uma única execução de instrução, pois ela requer uma viagem de ida e volta extra do cliente ao servidor. Em versões anteriores do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], ela também gera um procedimento armazenado temporário.  
  
 As instruções preparadas não podem ser usadas para criar objetos temporários no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 Alguns aplicativos de ODBC anteriores usados **SQLPrepare** qualquer momento [SQLBindParameter](../../native-client-odbc-api/sqlbindparameter.md) foi usado. **SQLBindParameter** não requer o uso de **SQLPrepare**, ele pode ser usado com **SQLExecDirect**. Por exemplo, use **SQLExecDirect** com **SQLBindParameter** para recuperar o código de retorno ou parâmetros de saída de um procedimento armazenado que é executado só uma vez. Não use **SQLPrepare** com **SQLBindParameter** , a menos que a mesma instrução será executada várias vezes.  
  
## <a name="see-also"></a>Consulte também  
 [Executar instruções &#40;ODBC&#41;](executing-statements-odbc.md)  
  
  
