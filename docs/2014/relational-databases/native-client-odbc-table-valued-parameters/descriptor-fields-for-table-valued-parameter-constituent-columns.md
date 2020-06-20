---
title: Campos de descritor para colunas constituintes de parâmetro com valor de tabela | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- table-valued parameters (ODBC), descriptor fields for constituent columns
ms.assetid: 944b3968-fd47-4847-98d6-b87e8ef2acdc
author: rothja
ms.author: jroth
ms.openlocfilehash: 3e4c45cf608c78715abd7c5075d4cd7fb2e162a5
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85018392"
---
# <a name="descriptor-fields-for-table-valued-parameter-constituent-columns"></a>Campos descritores para colunas constituintes do parâmetro com valor de tabela
  Os campos de descritor de parâmetro com valor de tabela descritos nesta seção são manipulados usando [SQLSetDescField](../native-client-odbc-api/sqlsetdescfield.md) e [SQLSetDescField](../native-client-odbc-api/sqlsetdescfield.md) com o identificador para o IPD (descritor de parâmetro de implementação).  
  
## <a name="remarks"></a>Comentários  
 SQL_DESC_AUTO_UNIQUE_VALUE é usado para parâmetros com valor de tabela, e também com outros recursos.  
  
|Nome do atributo|Type|Descrição|  
|--------------------|----------|-----------------|  
|SQL_DESC_AUTO_UNIQUE_VALUE|SQLINTEGER|SQL_TRUE indica que esta coluna é uma coluna de identidade.<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]pode usar essas informações para otimizar o desempenho, mas os aplicativos não são obrigados a defini-lo para colunas de identidade.|  
  
 Os seguintes atributos são adicionado a todos os tipos de parâmetros no APD (Descritor de Parâmetro de Aplicativo) e no IPD:  
  
|Nome do atributo|Type|Descrição|  
|--------------------|----------|-----------------|  
|SQL_CA_SS_COLUMN_COMPUTED|SQLSMALLINT|SQL_TRUE indica que essa coluna é computada.<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]pode usar essas informações para otimizar o desempenho, mas não é necessário que os aplicativos a definam para colunas computadas.<br /><br /> Este atributo é ignorado para associações que não são colunas de parâmetro com valor de tabela.|  
|SQL_CA_SS_COLUMN_IN_UNIQUE_KEY|SQLSMALLINT|SQL_TRUE indica que uma coluna de parâmetro com valor de tabela participa de uma chave exclusiva. Isto pode resultar em melhor desempenho de consulta. Este atributo é ignorado para associações que não são colunas de parâmetro com valor de tabela.|  
|SQL_CA_SS_COLUMN_SORT_ORDER|SQLSMALLINT|Indica a ordem de classificação de uma coluna de parâmetro com valor de tabela. Isto pode resultar em melhor desempenho de consulta. Este atributo é ignorado para associações que não são colunas de parâmetro com valor de tabela. Os seguintes valores são possíveis:<br /><br /> -SQL_SS_ASCENDING_ORDER<br />-SQL_SS_DESCENDING_ORDER<br />-SQL_SS_ORDER_UNSPECIFIED<br /><br /> Valores diferentes de SQL_SS_ASCENDING_ORDER e SQL_SS_DESCENDING_ORDER geram um erro com SQLSTATE HY024 e a mensagem 'Valor de atributo inválido' e são tratados como SQL_SS_ORDER_UNSPECIFIED, que é o valor padrão para este atributo.|  
|SQL_CA_SS_COLUMN_SORT_ORDINAL|SQLSMALLINT|Indica o ordinal de uma coluna de parâmetro com valor de tabela no conjunto de colunas que definem a ordenação global para um parâmetro com valor de tabela. Isto pode resultar em melhor desempenho de consulta. Este atributo é ignorado para associações que não são colunas de parâmetro com valor de tabela. Ordinais de classificação iniciam em 1. Um valor 0, o padrão, indica que uma coluna de parâmetro com valor de tabela não tem ordenação de coluna.|  
|SQL_CA_SS_COLUMN_HAS_DEFAULT_VALUE|SQLSMALLINT|Indica se todas as linhas no parâmetro com valor de tabela terão o valor padrão para esta coluna. Para parâmetros com valor de tabela, não é possível selecionar o valor padrão em uma base linha por linha. Um valor SQL_FALSE indica que as linhas terão valores não padrão. Este é o padrão. Um valor SQL_TRUE indica que esta coluna terá valores padrão para todas as linhas.<br /><br /> Se definido como SQL_TRUE, nenhum dos dados será enviado ao servidor.<br /><br /> Este campo também poderá ser usado com identidade ou colunas computadas se os valores de coluna não forem requeridos para processamento de servidor.|  
  
 Estes atributos só são válidos para colunas de parâmetro com valor de tabela. Eles são ignorados para outros parâmetros.  
  
 Se SQL_CA_SS_COL_HAS_DEFAULT_VALUE for definido para uma coluna de parâmetro com valor de tabela, SQL_DESC_DATA_PTR para essa coluna deverá ser um ponteiro nulo. Caso contrário, SQLExecute ou SQLExecDirect retornará SQL_ERROR. Um registro de diagnóstico será gerado com SQLSTATE = 07S01 e a mensagem "uso inválido do parâmetro padrão para \<p> o parâmetro, coluna \<c> ", em que \<p> é o ordinal do parâmetro e \<c> é o ordinal da coluna.  
  
## <a name="see-also"></a>Consulte Também  
 [Parâmetros com valor de tabela &#40;&#41;ODBC](table-valued-parameters-odbc.md)  
  
  
