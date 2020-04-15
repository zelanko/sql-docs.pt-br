---
title: ODBC SQL Tipo para parâmetros avaliados em tabela | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL_SS_TABLE
ms.assetid: 6725bfb9-5f10-4115-be09-fd9c9f5779ea
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 6aae522544f4d9532dbc2d71db1b3d55ebee3da5
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81297836"
---
# <a name="odbc-sql-type-for-table-valued-parameters"></a>Tipo ODBC SQL para parâmetros com valor de tabela
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  O suporte para parâmetros com valor de tabela é fornecido por um novo tipo ODBC SQL, SQL_SS_TABLE.  
  
## <a name="remarks"></a>Comentários  
 SQL_SS_TABLE não pode ser convertido em qualquer outro tipo de dados ODBC ou do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 Se SQL_SS_TABLE for usado como um tipo de dados C no parâmetro *ValueType* do SQLBindParameter, ou se for feita uma tentativa de definir SQL_DESC_TYPE em um registro de descritor de parâmetro de aplicativo (APD) para SQL_SS_TABLE, SQL_ERROR é retornado e um registro de diagnóstico é gerado com SQLSTATE=HY003, "Tipo de buffer de aplicativo inválido".  
  
 Se SQL_DESC_TYPE for definido como SQL_SS_TABLE em um registro do IPD e o registro do descritor de parâmetro de aplicativo correspondente não for SQL_C_DEFAULT, SQL_ERROR será retornado e um registro de diagnóstico será gerado com SQLSTATE=HY003, "Tipo de buffer de aplicativo inválido". Isso pode ocorrer com o *ParameterType* de um SQLSetDescField, SQLSetDescRec ou SQLBindParameter.  
  
 Se o parâmetro *TargetType* for SQL_SS_TABLE ao ligar para o SQLGetData, SQL_ERROR é retornado e um registro de diagnóstico é gerado com SQLSTATE=HY003, "Tipo de buffer de aplicativo inválido".  
  
 Não é possível associar uma coluna de parâmetros com valor de tabela como o tipo SQL_SS_TABLE. Se **SQLBindParameter** for chamado com *ParameterType* definido como SQL_SS_TABLE, SQL_ERROR será retornado e um registro de diagnóstico será gerado com SQLSTATE=HY004, "Tipo de dados SQL inválido". Isso também pode ocorrer com SQLSetDescField e SQLSetDescRec.  
  
 Os valores de coluna de parâmetros com valor de tabela têm as mesmas opções de conversão de dados que as colunas de parâmetros e resultados.  
  
 Um parâmetro com valor de tabela pode ser um parâmetro de entrada somente no [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ou posterior. Se for feita uma tentativa de definir SQL_DESC_PARAMETER_TYPE para um valor diferente SQL_PARAM_INPUT via SQLBindParameter ou SQLSetDescField, SQL_ERROR é retornada e um registro de diagnóstico é adicionado à declaração com SQLSTATE=HY105 e a mensagem "Tipo de parâmetro inválido".  
  
 As colunas de parâmetros com valor de tabela não podem usar SQL_DEFAULT_PARAM em *StrLen_or_IndPtr*, porque não há suporte para valores padrão por linha com parâmetros com valor de tabela. Em vez disso, um aplicativo pode definir o atributo de coluna SQL_CA_SS_COL_HAS_DEFAULT_VALUE como 1. Isso significa que a coluna terá valores padrão para todas as linhas. Se *StrLen_or_IndPtr* estiver definida como SQL_DEFAULT_PARAM, SQLExecute ou SQLExecDirect retornarão SQL_ERROR e um registro de diagnóstico será adicionado à declaração com SQLSTATE=HY090 e a mensagem "Comprimento de seqüência ou buffer inválido".  
  
## <a name="see-also"></a>Consulte Também  
 [Parâmetros avaliados em tabela &#40;&#41;o ODBC](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)  
  
  
