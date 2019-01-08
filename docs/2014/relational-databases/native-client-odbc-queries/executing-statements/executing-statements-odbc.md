---
title: Execução de instruções (ODBC) | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1517e17a7b0ecaf9137e3af21e076dacc2fd98f3
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/13/2018
ms.locfileid: "53376988"
---
# <a name="executing-statements-odbc"></a>Executando instruções (ODBC)
  O [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] driver ODBC Native Client oferece várias formas para executar instruções SQL em um [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] banco de dados:  
  
-   Execução direta  
  
-   Execução preparada  
  
 Execução direta envolve compilar uma cadeia de caracteres contendo um [!INCLUDE[tsql](../../../includes/tsql-md.md)] instrução e enviá-lo para execução usando o **SQLExecDirect** função. A execução preparada envolve a compilação de uma cadeia de caracteres contendo uma instrução [!INCLUDE[tsql](../../../includes/tsql-md.md)] e a execução em dois estágios. O primeiro estágio usa a [SQLPrepare Function](https://go.microsoft.com/fwlink/?LinkId=59360) função para analisar e compilar o plano de execução da instrução no [!INCLUDE[ssDE](../../../includes/ssde-md.md)]. O segundo estágio usa a **SQLExecute** função para executar o plano de execução preparado anteriormente. Dessa forma, a sobrecarga de análise e compilação é salva em cada execução. A execução preparada geralmente é usada através de aplicativos para executar a mesma instrução SQL com parâmetros várias vezes.  
  
 As execuções direta e preparada podem executar uma única instrução [!INCLUDE[tsql](../../../includes/tsql-md.md)] ou um lote de instruções SQL, ou elas podem chamar um procedimento armazenado.  
  
## <a name="in-this-section"></a>Nesta seção  
  
-   [Execução direta](direct-execution.md)  
  
-   [Execução preparada](prepared-execution.md)  
  
-   [Procedimentos](procedures.md)  
  
-   [Lotes de instruções](batches-of-statements.md)  
  
-   [Efeitos das opções ISO](effects-of-iso-options.md)  
  
## <a name="see-also"></a>Consulte também  
 [Executando consultas &#40;ODBC&#41;](../executing-queries-odbc.md)  
  
  
