---
title: SQLParamData | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- SQLParamData function
ms.assetid: 92349482-ea22-4a6a-8484-e9c6566794fa
caps.latest.revision: 10
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: bd3fefeaa05f806650b58d1778658fda0ed63fa2
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36020039"
---
# <a name="sqlparamdata"></a>SQLParamData
  Quando SQLParamData retorna o *ValuePtrPtr* associado com um parâmetro com valor de tabela, o aplicativo deve chamar SQLPutData com *StrLen_Or_Ind*. Se *StrLen_Or_Ind* tem um valor maior que 0, isso significa que o aplicativo está pronto para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client para coletar dados de parâmetro para a próxima linha de parâmetro com valor de tabela. Se *StrLen_Or_Ind* tiver um valor 0, significará que não há mais linhas de dados para o parâmetro com valor de tabela. Para obter mais informações, consulte [de associação e Data Transfer of Table-Valued parâmetros e valores de coluna](../native-client-odbc-table-valued-parameters/binding-and-data-transfer-of-table-valued-parameters-and-column-values.md).  
  
 Para obter mais informações sobre parâmetros com valor de tabela, consulte [parâmetros com valor de tabela &#40;ODBC&#41;](../native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md).  
  
## <a name="see-also"></a>Consulte também  
 [SQLParamData](http://go.microsoft.com/fwlink/?LinkId=80706)   
 [Detalhes da implementação da API do ODBC](odbc-api-implementation-details.md)  
  
  