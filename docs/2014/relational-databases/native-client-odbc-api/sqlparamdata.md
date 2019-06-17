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
ms.openlocfilehash: da50163b90d4a871c2524e1723797474386be8f6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63046661"
---
# <a name="sqlparamdata"></a>SQLParamData
  Quando SQLParamData retorna o *ValuePtrPtr* associado com um parâmetro com valor de tabela, o aplicativo deve chamar SQLPutData com *StrLen_Or_Ind*. Se *StrLen_Or_Ind* tiver um valor maior que 0, significará que o aplicativo está pronto para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client coletar dados de parâmetro para a próxima linha de parâmetro com valor de tabela. Se *StrLen_Or_Ind* tiver um valor 0, significará que não há mais linhas de dados para o parâmetro com valor de tabela. Para obter mais informações, consulte [associação e Data Transfer of Table-Valued parâmetros e valores de coluna](../native-client-odbc-table-valued-parameters/binding-and-data-transfer-of-table-valued-parameters-and-column-values.md).  
  
 Para obter mais informações sobre parâmetros com valor de tabela, consulte [parâmetros com valor de tabela &#40;ODBC&#41;](../native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md).  
  
## <a name="see-also"></a>Consulte também  
 [SQLParamData](https://go.microsoft.com/fwlink/?LinkId=80706)   
 [Detalhes da implementação da API do ODBC](odbc-api-implementation-details.md)  
  
  
