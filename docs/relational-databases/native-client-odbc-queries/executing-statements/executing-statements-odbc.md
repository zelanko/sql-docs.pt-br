---
title: Execução de instruções (ODBC) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client ODBC driver, statements
- statements [ODBC]
- ODBC applications, statements
- statements [ODBC], executing
ms.assetid: 063fc40d-ff81-490d-9c9b-2faefb729f37
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 8955a2ab0cff12ec65340b6c5ebfb6ddeedef744
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37423845"
---
# <a name="executing-statements-odbc"></a>Executando instruções (ODBC)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  O [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] driver ODBC Native Client oferece várias formas para executar instruções SQL em um [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] banco de dados:  
  
-   Execução direta  
  
-   Execução preparada  
  
 Execução direta envolve compilar uma cadeia de caracteres contendo um [!INCLUDE[tsql](../../../includes/tsql-md.md)] instrução e enviá-lo para execução usando o **SQLExecDirect** função. A execução preparada envolve a compilação de uma cadeia de caracteres contendo uma instrução [!INCLUDE[tsql](../../../includes/tsql-md.md)] e a execução em dois estágios. O primeiro estágio usa a [SQLPrepare Function](http://go.microsoft.com/fwlink/?LinkId=59360) função para analisar e compilar o plano de execução da instrução no [!INCLUDE[ssDE](../../../includes/ssde-md.md)]. O segundo estágio usa a **SQLExecute** função para executar o plano de execução preparado anteriormente. Dessa forma, a sobrecarga de análise e compilação é salva em cada execução. A execução preparada geralmente é usada através de aplicativos para executar a mesma instrução SQL com parâmetros várias vezes.  
  
 As execuções direta e preparada podem executar uma única instrução [!INCLUDE[tsql](../../../includes/tsql-md.md)] ou um lote de instruções SQL, ou elas podem chamar um procedimento armazenado.  
  
## <a name="in-this-section"></a>Nesta seção  
  
-   [Execução direta](../../../relational-databases/native-client-odbc-queries/executing-statements/direct-execution.md)  
  
-   [Execução preparada](../../../relational-databases/native-client-odbc-queries/executing-statements/prepared-execution.md)  
  
-   [Procedimentos](../../../relational-databases/native-client-odbc-queries/executing-statements/procedures.md)  
  
-   [Lotes de instruções](../../../relational-databases/native-client-odbc-queries/executing-statements/batches-of-statements.md)  
  
-   [Efeitos das opções ISO](../../../relational-databases/native-client-odbc-queries/executing-statements/effects-of-iso-options.md)  
  
## <a name="see-also"></a>Consulte também  
 [Executando consultas &#40;ODBC&#41;](../../../relational-databases/native-client-odbc-queries/executing-queries-odbc.md)  
  
  
