---
title: Executando instruções (ODBC) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client ODBC driver, statements
- statements [ODBC]
- ODBC applications, statements
- statements [ODBC], executing
ms.assetid: 063fc40d-ff81-490d-9c9b-2faefb729f37
author: rothja
ms.author: jroth
ms.openlocfilehash: 01dc4298855fd3418029164dea3ed089185da934
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85018418"
---
# <a name="executing-statements-odbc"></a>Executando instruções (ODBC)
  O [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] driver ODBC do Native Client oferece várias maneiras de executar instruções SQL em um [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] banco de dados:  
  
-   Execução direta  
  
-   Execução preparada  
  
 A execução direta envolve criar uma cadeia de caracteres que contém uma [!INCLUDE[tsql](../../../includes/tsql-md.md)] instrução e enviá-la para execução usando a função **SQLExecDirect** . A execução preparada envolve a compilação de uma cadeia de caracteres contendo uma instrução [!INCLUDE[tsql](../../../includes/tsql-md.md)] e a execução em dois estágios. O primeiro estágio usa a função de [função SQLPrepare](https://go.microsoft.com/fwlink/?LinkId=59360) para analisar e compilar o plano de execução para a instrução no [!INCLUDE[ssDE](../../../includes/ssde-md.md)] . O segundo estágio usa a função **SQLExecute** para executar o plano de execução preparado anteriormente. Dessa forma, a sobrecarga de análise e compilação é salva em cada execução. A execução preparada geralmente é usada através de aplicativos para executar a mesma instrução SQL com parâmetros várias vezes.  
  
 As execuções direta e preparada podem executar uma única instrução [!INCLUDE[tsql](../../../includes/tsql-md.md)] ou um lote de instruções SQL, ou elas podem chamar um procedimento armazenado.  
  
## <a name="in-this-section"></a>Nesta seção  
  
-   [Execução direta](direct-execution.md)  
  
-   [Execução preparada](prepared-execution.md)  
  
-   [Procedimentos](procedures.md)  
  
-   [Lotes de instruções](batches-of-statements.md)  
  
-   [Efeitos das opções ISO](effects-of-iso-options.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Executando consultas &#40;ODBC&#41;](../executing-queries-odbc.md)  
  
  
