---
title: Dados de parâmetro com valor de tabela de conversão e outros erros e avisos | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- table-valued parameters (ODBC), data conversion
- table-valued parameters (ODBC), error messages
ms.assetid: edd45234-59dc-4338-94fc-330e820cc248
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: f5e9b4d74d4ab33fee6398ab0e679d92765aff96
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/06/2018
ms.locfileid: "39555376"
---
# <a name="table-valued-parameter-data-conversion-and-other-errors-and-warnings"></a>Conversão de dados de parâmetros com valor de tabela e outros erros e avisos
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Valores da coluna de parâmetros com valor de tabela podem ser convertidos entre tipos de dados de cliente e servidor da mesma forma que outros valores de parâmetro e coluna. Mas como um parâmetro com valor de tabela pode conter várias colunas e várias linhas, é importante conseguir identificar o valor real quando o erro ocorrer.  
  
 Quando um erro ou aviso é detectado em uma coluna de parâmetro com valor de tabela, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client gerará um registro diagnóstico. A mensagem de erro conterá o número de parâmetro com valor de tabela, assim como o número da linha e o ordinal da coluna. Um aplicativo também pode usar os campos de diagnóstico SQL_DIAG_SS_TABLE_COLUMN_NUMBER e SQL_DIAG_SS_TABLE_ROW_NUMBER dentro dos registros de diagnóstico para determinar quais valores são associados a erros e avisos. Estes campos de diagnóstico estão disponíveis no [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e versões posteriores.  
  
 Os componentes de mensagem e SQLSTATE dos registros de diagnóstico estarão em conformidade com o comportamento de ODBC existente em todos os níveis. Ou seja, com exceção das informações de identificação de parâmetro, linha e coluna, as mensagens de erro deverão ter os mesmos valores para parâmetros com valor de tabela que teriam para os parâmetros que não apresentam valor de tabela.  
  
## <a name="see-also"></a>Consulte também  
 [Parâmetros com valor de tabela &#40;ODBC&#41;](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)  
  
  
