---
title: SQLParamData | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-odbc-api
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords: SQLParamData function
ms.assetid: 92349482-ea22-4a6a-8484-e9c6566794fa
caps.latest.revision: "10"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 93ee1e1bd50cbbf34933cdd085fb51a608dd6080
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2018
---
# <a name="sqlparamdata"></a>SQLParamData
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Quando SQLParamData retorna o *ValuePtrPtr* associado com um parâmetro com valor de tabela, o aplicativo deve chamar SQLPutData com *StrLen_Or_Ind*. Se *StrLen_Or_Ind* tem um valor maior que 0, isso significa que o aplicativo está pronto para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client para coletar dados de parâmetro para a próxima linha de parâmetro com valor de tabela. Se *StrLen_Or_Ind* tiver um valor 0, significará que não há mais linhas de dados para o parâmetro com valor de tabela. Para obter mais informações, consulte [de associação e Data Transfer of Table-Valued parâmetros e valores de coluna](../../relational-databases/native-client-odbc-table-valued-parameters/binding-and-data-transfer-of-table-valued-parameters-and-column-values.md).  
  
 Para obter mais informações sobre parâmetros com valor de tabela, consulte [parâmetros com valor de tabela &#40; ODBC &#41;](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md).  
  
## <a name="see-also"></a>Consulte Também  
 [SQLParamData](http://go.microsoft.com/fwlink/?LinkId=80706)   
 [Detalhes da implementação da API do ODBC](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
