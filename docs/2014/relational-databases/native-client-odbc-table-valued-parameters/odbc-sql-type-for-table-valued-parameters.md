---
title: Tipo ODBC SQL para parâmetros com valor de tabela | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL_SS_TABLE
ms.assetid: 6725bfb9-5f10-4115-be09-fd9c9f5779ea
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 90857b24fb467df0292beeb88fb9751e68204d12
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63199981"
---
# <a name="odbc-sql-type-for-table-valued-parameters"></a>Tipo ODBC SQL para parâmetros com valor de tabela
  O suporte para parâmetros com valor de tabela é fornecido por um novo tipo ODBC SQL, SQL_SS_TABLE.  
  
## <a name="remarks"></a>Comentários  
 SQL_SS_TABLE não pode ser convertido em qualquer outro tipo de dados ODBC ou do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 Se SQL_SS_TABLE for usado como um tipo de dados C na *ValueType* parâmetro SQLBindParameter ou uma tentativa for feito para definir SQL_DESC_TYPE em um registro APD (descritor) do parâmetro de aplicativo como SQL_SS_TABLE, SQL_ERROR será retornado e um registro de diagnóstico será gerado com SQLSTATE=hy003, "tipo de buffer de aplicativo inválido".  
  
 Se SQL_DESC_TYPE for definido como SQL_SS_TABLE em um registro do IPD e o registro do descritor de parâmetro de aplicativo correspondente não for SQL_C_DEFAULT, SQL_ERROR será retornado e um registro de diagnóstico será gerado com SQLSTATE=HY003, "Tipo de buffer de aplicativo inválido". Isso pode ocorrer com o *ParameterType* de SQLSetDescField, SQLSetDescRec ou SQLBindParameter.  
  
 Se o *TargetType* parâmetro for SQL_SS_TABLE ao chamar SQLGetData, SQL_ERROR será retornado e um registro de diagnóstico será gerado com SQLSTATE=hy003, "tipo de buffer de aplicativo inválido".  
  
 Não é possível associar uma coluna de parâmetros com valor de tabela como o tipo SQL_SS_TABLE. Se `SQLBindParameter` é chamado com *ParameterType* definido como SQL_SS_TABLE, SQL_ERROR será retornado e um registro de diagnóstico será gerado com SQLSTATE=hy004, "Tipo de dados SQL inválido". Isso também pode ocorrer com SQLSetDescField e SQLSetDescRec.  
  
 Os valores de coluna de parâmetros com valor de tabela têm as mesmas opções de conversão de dados que as colunas de parâmetros e resultados.  
  
 Um parâmetro com valor de tabela pode ser um parâmetro de entrada somente no [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ou posterior. Se for feita uma tentativa de definir SQL_DESC_PARAMETER_TYPE como um valor diferente de SQL_PARAM_INPUT por meio de SQLBindParameter ou SQLSetDescField, SQL_ERROR será retornado e um registro de diagnóstico é adicionado à instrução com SQLSTATE = HY105 e a mensagem "parâmetro inválido Digite".  
  
 As colunas de parâmetros com valor de tabela não podem usar SQL_DEFAULT_PARAM em *StrLen_or_IndPtr*, porque não há suporte para valores padrão por linha com parâmetros com valor de tabela. Em vez disso, um aplicativo pode definir o atributo de coluna SQL_CA_SS_COL_HAS_DEFAULT_VALUE como 1. Isso significa que a coluna terá valores padrão para todas as linhas. Se *StrLen_or_IndPtr* é definido como SQL_DEFAULT_PARAM, SQLExecute ou SQLExecDirect retornará SQL_ERROR e um registro de diagnóstico será adicionado à instrução com SQLSTATE=hy090 e a mensagem "Comprimento inválido de buffer ou cadeia de caracteres".  
  
## <a name="see-also"></a>Consulte também  
 [Parâmetros com valor de tabela &#40;ODBC&#41;](table-valued-parameters-odbc.md)  
  
  
