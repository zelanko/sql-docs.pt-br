---
title: Execução de instruções (ODBC) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: native-client-odbc-queries
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client ODBC driver, statements
- statements [ODBC]
- ODBC applications, statements
- statements [ODBC], executing
ms.assetid: 063fc40d-ff81-490d-9c9b-2faefb729f37
caps.latest.revision: 33
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 7521f18d4ac934bd05b6922f8e48bcb18d31a4c8
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/04/2018
ms.locfileid: "34707814"
---
# <a name="executing-statements-odbc"></a>Executando instruções (ODBC)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  O [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] driver ODBC Native Client oferece várias formas de executar instruções SQL em um [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] banco de dados:  
  
-   Execução direta  
  
-   Execução preparada  
  
 Execução direta envolve compilar uma cadeia de caracteres contendo um [!INCLUDE[tsql](../../../includes/tsql-md.md)] instrução e enviá-lo para execução com o **SQLExecDirect** função. A execução preparada envolve a compilação de uma cadeia de caracteres contendo uma instrução [!INCLUDE[tsql](../../../includes/tsql-md.md)] e a execução em dois estágios. O primeiro estágio usa a [função SQLPrepare](http://go.microsoft.com/fwlink/?LinkId=59360) para analisar e compilar o plano de execução da instrução no [!INCLUDE[ssDE](../../../includes/ssde-md.md)]. O segundo estágio usa a **SQLExecute** função para executar o plano de execução preparado anteriormente. Dessa forma, a sobrecarga de análise e compilação é salva em cada execução. A execução preparada geralmente é usada através de aplicativos para executar a mesma instrução SQL com parâmetros várias vezes.  
  
 As execuções direta e preparada podem executar uma única instrução [!INCLUDE[tsql](../../../includes/tsql-md.md)] ou um lote de instruções SQL, ou elas podem chamar um procedimento armazenado.  
  
## <a name="in-this-section"></a>Nesta seção  
  
-   [Execução direta](../../../relational-databases/native-client-odbc-queries/executing-statements/direct-execution.md)  
  
-   [Execução preparada](../../../relational-databases/native-client-odbc-queries/executing-statements/prepared-execution.md)  
  
-   [Procedimentos](../../../relational-databases/native-client-odbc-queries/executing-statements/procedures.md)  
  
-   [Lotes de instruções](../../../relational-databases/native-client-odbc-queries/executing-statements/batches-of-statements.md)  
  
-   [Efeitos das opções ISO](../../../relational-databases/native-client-odbc-queries/executing-statements/effects-of-iso-options.md)  
  
## <a name="see-also"></a>Consulte também  
 [Executando consultas &#40;ODBC&#41;](../../../relational-databases/native-client-odbc-queries/executing-queries-odbc.md)  
  
  
