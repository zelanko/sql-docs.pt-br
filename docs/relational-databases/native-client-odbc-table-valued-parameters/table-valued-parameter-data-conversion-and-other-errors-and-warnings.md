---
title: Conversão de dados de parâmetro com valor de tabela e outros erros e avisos | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- table-valued parameters (ODBC), data conversion
- table-valued parameters (ODBC), error messages
ms.assetid: edd45234-59dc-4338-94fc-330e820cc248
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 5df7f61a835d92a5eb69ea28158c81eb1dab95f9
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/07/2019
ms.locfileid: "73790762"
---
# <a name="table-valued-parameter-data-conversion-and-other-errors-and-warnings"></a>Conversão de dados de parâmetros com valor de tabela e outros erros e avisos
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Valores da coluna de parâmetros com valor de tabela podem ser convertidos entre tipos de dados de cliente e servidor da mesma forma que outros valores de parâmetro e coluna. Mas como um parâmetro com valor de tabela pode conter várias colunas e várias linhas, é importante conseguir identificar o valor real quando o erro ocorrer.  
  
 Quando um erro ou aviso é detectado em uma coluna de parâmetro com valor de tabela, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client gerará um registro diagnóstico. A mensagem de erro conterá o número de parâmetro com valor de tabela, assim como o número da linha e o ordinal da coluna. Um aplicativo também pode usar os campos de diagnóstico SQL_DIAG_SS_TABLE_COLUMN_NUMBER e SQL_DIAG_SS_TABLE_ROW_NUMBER dentro dos registros de diagnóstico para determinar quais valores são associados a erros e avisos. Estes campos de diagnóstico estão disponíveis no [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e versões posteriores.  
  
 Os componentes de mensagem e SQLSTATE dos registros de diagnóstico estarão em conformidade com o comportamento de ODBC existente em todos os níveis. Ou seja, exceto para as informações de identificação de parâmetro, linha e coluna, as mensagens de erro têm os mesmos valores para parâmetros com valor de tabela como seriam para parâmetros com valor não tabela.  
  
## <a name="see-also"></a>Consulte também  
 [Parâmetros &#40;com valor de tabela ODBC&#41;](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)  
  
  
