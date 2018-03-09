---
title: Executando procedimentos armazenados | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-odbc-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- ODBC, stored procedures
- stored procedures [ODBC], running
- SQL Server Native Client ODBC driver, stored procedures
- stored procedures [ODBC], executing
ms.assetid: 866b6dd3-2acd-4dfb-aeca-a0352b2d4c6a
caps.latest.revision: "36"
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 5deaa43466320e4900b8247cd9e80ef997401e69
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/25/2018
---
# <a name="running-stored-procedures"></a>Executando procedimentos armazenados
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Um procedimento armazenado é um objeto executável armazenado em um banco de dados. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] oferece suporte a:  
  
-   Procedimentos armazenados:  
  
     Uma ou mais instruções SQL pré-compiladas em um único procedimento executável.  
  
-   Procedimentos armazenados estendidos:  
  
     DLLs (bibliotecas de vínculo dinâmico) C ou C++ escritas para a API Open Data Services do SQL Server para procedimentos armazenados estendidos. A API Open Data Services estende os recursos de procedimentos armazenados para incluir código C ou C++.  
  
 Ao executar instruções, chamar um procedimento armazenado na fonte de dados (em vez de executar ou preparar diretamente uma instrução no aplicativo cliente) pode oferecer:  
  
-   Maior desempenho  
  
     Instruções SQL são analisadas e compiladas quando procedimentos são criados. Esta sobrecarga é então salva quando os procedimentos são executados.  
  
-   Menor sobrecarga da rede  
  
     A execução de um procedimento em vez de enviar consultas complexas pela rede pode reduzir o tráfego de rede. Se um aplicativo ODBC usa a sintaxe ODBC { CALL } para executar um procedimento armazenado, o driver ODBC faz otimizações adicionais que eliminam a necessidade de converter dados de parâmetros.  
  
-   Maior consistência  
  
     Se as regras de uma organização forem implementadas em um recurso central, como um procedimento armazenado, elas poderão ser codificadas, testadas e depuradas de uma vez. Programadores individuais podem então usar os procedimentos armazenados testados em vez de desenvolver suas próprias implementações.  
  
-   Maior exatidão  
  
     Como geralmente os procedimentos armazenados são desenvolvidos por programadores experientes, existe a tendência de que sejam mais eficientes e tenham menos erros que o código desenvolvido várias vezes por programadores com diversos níveis de habilidade.  
  
-   Maior funcionalidade  
  
     Os procedimentos armazenados estendidos podem usar recursos do C e do C++ não disponíveis em instruções [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
     Para obter um exemplo de como chamar um procedimento armazenado, consulte [processar códigos de retorno e parâmetros de saída &#40; ODBC &#41;](../../relational-databases/native-client-odbc-how-to/running-stored-procedures-process-return-codes-and-output-parameters.md).  
  
## <a name="in-this-section"></a>Nesta seção  
  
-   [Chamando um procedimento armazenado](../../relational-databases/native-client-odbc-stored-procedures/calling-a-stored-procedure.md)  
  
-   [Processando em lote as chamadas de procedimento armazenado](../../relational-databases/native-client-odbc-stored-procedures/batching-stored-procedure-calls.md)  
  
-   [Processando resultados do procedimento armazenado](../../relational-databases/native-client-odbc-stored-procedures/processing-stored-procedure-results.md)  
  
## <a name="see-also"></a>Consulte também  
 [Cliente nativo do SQL Server &#40; ODBC &#41;](../../relational-databases/native-client/odbc/sql-server-native-client-odbc.md)   
 [Execução armazenados tópicos de instruções de procedimentos &#40; ODBC &#41;](http://msdn.microsoft.com/library/c2220182-a23d-4475-b353-77a77ab613d6)  
  
  
