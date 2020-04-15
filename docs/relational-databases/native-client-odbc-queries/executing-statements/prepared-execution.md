---
title: Execução Preparada | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
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
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 8265ed80028d5d8ac9696853a29474552f401f3e
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81297910"
---
# <a name="prepared-execution"></a>Execução preparada
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  A API do ODBC define a execução preparada como um modo de reduzir a sobrecarga de análise e compilação associada à execução repetida da instrução [!INCLUDE[tsql](../../../includes/tsql-md.md)]. O aplicativo compila uma cadeia de caracteres que contém uma instrução SQL e então a executa em duas fases. Ele chama [sqlprepare function](https://go.microsoft.com/fwlink/?LinkId=59360) uma vez para ter a declaração [!INCLUDE[ssDE](../../../includes/ssde-md.md)]analisado e compilado em um plano de execução pelo . Em seguida, ele chama **SQLExecute** para cada execução do plano de execução preparado. Dessa forma, a sobrecarga de análise e compilação é salva em cada execução. A execução preparada geralmente é usada através de aplicativos para executar a mesma instrução SQL com parâmetros várias vezes.  
  
 Para a maioria dos bancos de dados, a execução preparada é mais rápida que a direta para instruções executadas mais de três ou quatro vezes primariamente, pois a instrução é compilada somente uma vez, enquanto instruções executadas diretamente são compiladas sempre que ocorrem. A execução preparada também pode fornecer uma redução no tráfego de rede, pois o driver pode enviar um identificador do plano de execução e os valores de parâmetro, em vez de toda uma instrução SQL, para a fonte de dados sempre que a instrução for executada.  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]reduz a diferença de desempenho entre execução direta e preparada através de algoritmos aprimorados para detectar e reutilizar planos de execução do **SQLExecDirect**. Isso torna alguns dos benefícios de desempenho da execução preparada disponíveis para instruções executadas diretamente. Para obter mais informações, consulte [Execução Direta](../../../relational-databases/native-client-odbc-queries/executing-statements/direct-execution.md).  
  
 O [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] também oferece suporte nativo para execução preparada. Um plano de execução é construído no **SQLPrepare** e posteriormente executado quando **o SQLExecute** é chamado. Como [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] não é necessário construir procedimentos armazenados temporários no **SQLPrepare,** não há sobrecarga extra nas tabelas do sistema em **tempdb**.  
  
 Por razões de desempenho, a preparação da declaração é adiada até que **o SQLExecute** seja chamado ou uma operação de metapropriedade (como [SQLDescribeCol](../../../relational-databases/native-client-odbc-api/sqldescribecol.md) ou [SQLDescribeParam](../../../relational-databases/native-client-odbc-api/sqldescribeparam.md) no ODBC) seja realizada. Esse é o comportamento padrão. Não são conhecidos erros na instrução que está sendo preparada até que ela seja executada ou uma operação de metapropriedade seja executada. Definir o atributo da instrução específica do driver ODBC do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client SQL_SOPT_SS_DEFER_PREPARE como SQL_DP_OFF pode desativar esse comportamento padrão.  
  
 Em caso de preparação diferida, ligar para **SQLDescribeCol** ou **SQLDescribeParam** antes de ligar para o **SQLExecute** gera uma ida e volta extra para o servidor. No **SQLDescribeCol,** o driver remove a cláusula WHERE da consulta e envia-a para o servidor com SET FMTONLY ON para obter a descrição das colunas no primeiro conjunto de resultados retornado pela consulta. No **SQLDescribeParam**, o driver chama o servidor para obter uma descrição das expressões ou colunas referenciadas por quaisquer marcadores de parâmetro na consulta. Esse método também tem algumas restrições, como não poder resolver parâmetros em subconsultas.  
  
 O uso excessivo do **SQLPrepare** com o driver ODBC do Cliente Nativo degrada o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] desempenho, especialmente quando conectado às versões anteriores do SQL Server. A execução preparada não deve ser usada para instruções executadas uma única vez. A execução preparada é mais lenta que a direta para uma única execução de instrução, pois ela requer uma viagem de ida e volta extra do cliente ao servidor. Em versões anteriores do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], ela também gera um procedimento armazenado temporário.  
  
 As instruções preparadas não podem ser usadas para criar objetos temporários no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 Alguns dos primeiros aplicativos ODBC usavam **SQLPrepare** sempre que [o SQLBindParameter](../../../relational-databases/native-client-odbc-api/sqlbindparameter.md) era usado. **SQLBindParameter** não requer o uso de **SQLPrepare,** ele pode ser usado com **SQLExecDirect**. Por exemplo, use **SQLExecDirect** com **SQLBindParameter** para recuperar o código de retorno ou os parâmetros de saída de um procedimento armazenado que é executado apenas uma vez. Não use **SQLPrepare** com **SQLBindParameter,** a menos que a mesma declaração seja executada várias vezes.  
  
## <a name="see-also"></a>Consulte Também  
 [Execução de Declarações &#40;&#41;Da ODBC](../../../relational-databases/native-client-odbc-queries/executing-statements/executing-statements-odbc.md)  
  
  
