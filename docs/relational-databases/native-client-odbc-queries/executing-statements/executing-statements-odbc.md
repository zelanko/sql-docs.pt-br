---
title: Executando Declarações (ODBC) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client ODBC driver, statements
- statements [ODBC]
- ODBC applications, statements
- statements [ODBC], executing
ms.assetid: 063fc40d-ff81-490d-9c9b-2faefb729f37
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 3489c26073da15fb41af6d1560cb48fe38897386
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81297926"
---
# <a name="executing-statements-odbc"></a>Executando instruções (ODBC)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  O [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] driver ODBC do Cliente Nativo oferece uma variedade [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] de maneiras de executar instruções SQL em um banco de dados:  
  
-   Execução direta  
  
-   Execução preparada  
  
 A execução direta envolve a [!INCLUDE[tsql](../../../includes/tsql-md.md)] construção de uma seqüência de caracteres contendo uma declaração e enviá-la para execução usando a função **SQLExecDirect.** A execução preparada envolve a compilação de uma cadeia de caracteres contendo uma instrução [!INCLUDE[tsql](../../../includes/tsql-md.md)] e a execução em dois estágios. O primeiro estágio usa a função [SQLPrepare function](https://go.microsoft.com/fwlink/?LinkId=59360) para analisar e [!INCLUDE[ssDE](../../../includes/ssde-md.md)]compilar o plano de execução da declaração no . O segundo estágio usa a função **SQLExecute** para executar o plano de execução previamente preparado. Dessa forma, a sobrecarga de análise e compilação é salva em cada execução. A execução preparada geralmente é usada através de aplicativos para executar a mesma instrução SQL com parâmetros várias vezes.  
  
 As execuções direta e preparada podem executar uma única instrução [!INCLUDE[tsql](../../../includes/tsql-md.md)] ou um lote de instruções SQL, ou elas podem chamar um procedimento armazenado.  
  
## <a name="in-this-section"></a>Nesta seção  
  
-   [Execução direta](../../../relational-databases/native-client-odbc-queries/executing-statements/direct-execution.md)  
  
-   [Execução preparada](../../../relational-databases/native-client-odbc-queries/executing-statements/prepared-execution.md)  
  
-   [Procedimentos](../../../relational-databases/native-client-odbc-queries/executing-statements/procedures.md)  
  
-   [Lotes de instruções](../../../relational-databases/native-client-odbc-queries/executing-statements/batches-of-statements.md)  
  
-   [Efeitos das opções ISO](../../../relational-databases/native-client-odbc-queries/executing-statements/effects-of-iso-options.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Execução de consultas &#40;&#41;ODBC](../../../relational-databases/native-client-odbc-queries/executing-queries-odbc.md)  
  
  
