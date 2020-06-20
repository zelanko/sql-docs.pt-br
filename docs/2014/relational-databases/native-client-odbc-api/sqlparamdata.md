---
title: SQLParamData | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQLParamData function
ms.assetid: 92349482-ea22-4a6a-8484-e9c6566794fa
author: rothja
ms.author: jroth
ms.openlocfilehash: a4e0e8b31a65f28ce83e0d114231bdedd7a35a4c
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85021972"
---
# <a name="sqlparamdata"></a>SQLParamData
  Quando SQLParamData retorna o *ValuePtrPtr* associado a um parâmetro com valor de tabela, o aplicativo deve chamar SQLPutData com *StrLen_or_Ind*. Se *StrLen_Or_Ind* tiver um valor maior que 0, significará que o aplicativo está pronto para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client coletar dados de parâmetro para a próxima linha de parâmetro com valor de tabela. Se *StrLen_Or_Ind* tiver um valor 0, significará que não há mais linhas de dados para o parâmetro com valor de tabela. Para obter mais informações, consulte [associação e transferência de dados de parâmetros com valor de tabela e valores de coluna](../native-client-odbc-table-valued-parameters/binding-and-data-transfer-of-table-valued-parameters-and-column-values.md).  
  
 Para obter mais informações sobre parâmetros com valor de tabela, consulte [parâmetros com valor de tabela &#40;&#41;ODBC ](../native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md).  
  
## <a name="see-also"></a>Consulte Também  
 [SQLParamData](/sql/odbc/reference/syntax/sqlparamdata-function)   
 [ODBC API Implementation Details](odbc-api-implementation-details.md)  
  
  
