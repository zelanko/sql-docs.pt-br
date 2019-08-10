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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 79285523ec83d3f10ad6f23010a7f9a6398e5980
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/09/2019
ms.locfileid: "68890105"
---
# <a name="sqlparamdata"></a>SQLParamData
  Quando SQLParamData retorna o *ValuePtrPtr* associado a um parâmetro com valor de tabela, o aplicativo deve chamar SQLPutData com *StrLen_or_Ind*. Se *StrLen_Or_Ind* tiver um valor maior que 0, significará que o aplicativo está pronto para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client coletar dados de parâmetro para a próxima linha de parâmetro com valor de tabela. Se *StrLen_Or_Ind* tiver um valor 0, significará que não há mais linhas de dados para o parâmetro com valor de tabela. Para obter mais informações, consulte [associação e transferência de dados de parâmetros com valor de tabela e valores de coluna](../native-client-odbc-table-valued-parameters/binding-and-data-transfer-of-table-valued-parameters-and-column-values.md).  
  
 Para obter mais informações sobre parâmetros com valor de tabela, consulte [parâmetros &#40;com valor&#41;de tabela ODBC](../native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md).  
  
## <a name="see-also"></a>Consulte também  
 [SQLParamData](/sql/odbc/reference/syntax/sqlparamdata-function)   
 [Detalhes da implementação da API do ODBC](odbc-api-implementation-details.md)  
  
  
