---
title: Executando instruções (ODBC) | Microsoft Docs
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
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: efd0b9ba46975512491dadccb5a44940af52ec28
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "73791030"
---
# <a name="executing-statements-odbc"></a>Executando instruções (ODBC)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  O [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] driver ODBC do Native Client oferece várias maneiras de executar instruções SQL em um [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] banco de dados:  
  
-   Execução direta  
  
-   Execução preparada  
  
 A execução direta envolve criar uma cadeia de caracteres [!INCLUDE[tsql](../../../includes/tsql-md.md)] que contém uma instrução e enviá-la para execução usando a função **SQLExecDirect** . A execução preparada envolve a compilação de uma cadeia de caracteres contendo uma instrução [!INCLUDE[tsql](../../../includes/tsql-md.md)] e a execução em dois estágios. O primeiro estágio usa a função de [função SQLPrepare](https://go.microsoft.com/fwlink/?LinkId=59360) para analisar e compilar o plano de execução para a instrução [!INCLUDE[ssDE](../../../includes/ssde-md.md)]no. O segundo estágio usa a função **SQLExecute** para executar o plano de execução preparado anteriormente. Dessa forma, a sobrecarga de análise e compilação é salva em cada execução. A execução preparada geralmente é usada através de aplicativos para executar a mesma instrução SQL com parâmetros várias vezes.  
  
 As execuções direta e preparada podem executar uma única instrução [!INCLUDE[tsql](../../../includes/tsql-md.md)] ou um lote de instruções SQL, ou elas podem chamar um procedimento armazenado.  
  
## <a name="in-this-section"></a>Nesta seção  
  
-   [Execução direta](../../../relational-databases/native-client-odbc-queries/executing-statements/direct-execution.md)  
  
-   [Execução preparada](../../../relational-databases/native-client-odbc-queries/executing-statements/prepared-execution.md)  
  
-   [Procedimentos](../../../relational-databases/native-client-odbc-queries/executing-statements/procedures.md)  
  
-   [Lotes de instruções](../../../relational-databases/native-client-odbc-queries/executing-statements/batches-of-statements.md)  
  
-   [Efeitos das opções ISO](../../../relational-databases/native-client-odbc-queries/executing-statements/effects-of-iso-options.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Executando consultas &#40;ODBC&#41;](../../../relational-databases/native-client-odbc-queries/executing-queries-odbc.md)  
  
  
