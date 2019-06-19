---
title: A nova palavra-chave, a função CALC e funções de agregação | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- data shaping [ADO], functions
- CALC function [ADO]
- NEW keyword [ADO]
- aggregate functions [ADO]
ms.assetid: 0590b466-2a36-49a2-868e-028ef5e49394
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 0a72cf80f9fee9c887e7805f3a2a5bd542d7f47c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66702428"
---
# <a name="aggregate-functions-the-calc-function-and-the-new-keyword"></a>Funções de agregação, a função CALC e a palavra-chave NEW
Formatação de dados oferece suporte a funções a seguir. O nome atribuído o capítulo que contém a coluna a ser operado é o *capítulo alias*.  
  
 Um alias de capítulo pode ser totalmente qualificado, consistindo de cada nome de coluna de capítulo que levam a capítulo que contém o *nome de coluna,* todos separados por pontos. Por exemplo, se o capítulo pai, Cap1, contém um capítulo de filho, chap2, que tem uma coluna de quantidade amt, e o nome qualificado seria chap1.chap2.amt.  
  
|Funções de agregação|Descrição|  
|-------------------------|-----------------|  
|Soma (*capítulo alias*. *nome da coluna*)|Calcula a soma de todos os valores na coluna especificada.|  
|AVG(*chapter-alias*.*column-name*)|Calcula a média de todos os valores na coluna especificada.|  
|MAX(*chapter-alias*.*column-name*)|Calcula o valor máximo na coluna especificada.|  
|MIN(*chapter-alias*.*column-name*)|Calcula o valor mínimo na coluna especificada.|  
|CONTAGEM (*capítulo alias*[. *nome da coluna*])|Conta o número de linhas em que o alias especificado. Se uma coluna for especificada, somente as linhas para o qual essa coluna não for nulo serão incluídas na contagem.|  
|STDEV(*chapter-alias*.*column-name*)|Calcula o desvio padrão da coluna especificada.|  
|ANY(*chapter-alias*.*column-name*)|Um valor da coluna especificada. QUALQUER tem um valor previsível somente quando o valor da coluna é o mesmo para todas as linhas do capítulo.<br /><br /> **Observação** se a coluna não contiver o mesmo valor para todas as linhas do capítulo, o comando de forma arbitrariamente retorna um dos valores como o valor de qualquer função.|  
  
|expressão calculada|Descrição|  
|---------------------------|-----------------|  
|CALC(*expression*)|Calcula uma expressão arbitrária, mas apenas na linha do **Recordset** que contém a função CALC. Qualquer expressão usando esses [do Visual Basic for Applications (VBA) funções](../../../ado/guide/data/visual-basic-for-applications-functions.md) é permitido.|  
  
|NOVA palavra-chave|Descrição|  
|-----------------|-----------------|  
|NEW *field-type* [(*width* &#124; *scale* &#124; *precision* &#124; *error* [, *scale* &#124; *error*])]|Adiciona uma coluna vazia do tipo especificado para o **conjunto de registros**.|  
  
 O *tipo de campo* transmitido com a nova palavra-chave pode ser qualquer um dos seguintes tipos de dados.  
  
|Tipos de dados OLE DB|Equivalent(s) de tipo de dados ADO|  
|-----------------------|-----------------------------------|  
|DBTYPE_BSTR|adBSTR|  
|DBTYPE_BOOL|adBoolean|  
|DBTYPE_DECIMAL|adDecimal|  
|DBTYPE_UI1|adUnsignedTinyInt|  
|DBTYPE_I1|adTinyInt|  
|DBTYPE_UI2|adUnsignedSmallInt|  
|DBTYPE_UI4|adUnsignedInt|  
|DBTYPE_I8|adBigInt|  
|DBTYPE_UI8|adUnsignedBigInt|  
|DBTYPE_GUID|adGuid|  
|DBTYPE_BYTES|adBinary, AdVarBinary, adLongVarBinary|  
|DBTYPE_STR|adChar, adVarChar, adLongVarChar|  
|DBTYPE_WSTR|adWChar, adVarWChar, adLongVarWChar|  
|DBTYPE_NUMERIC|adNumeric|  
|DBTYPE_DBDATE|adDBDate|  
|DBTYPE_DBTIME|adDBTime|  
|DBTYPE_DBTIMESTAMP|adDBTimeStamp|  
|DBTYPE_VARNUMERIC|adVarNumeric|  
|DBTYPE_FILETIME|adFileTime|  
|DBTYPE_ERROR|adError|  
  
 Quando o novo campo é do tipo decimal (OLE DB, DBTYPE_DECIMAL, ou no ADO, adDecimal), você deve especificar os valores de precisão e escala.  
  
## <a name="see-also"></a>Consulte também  
 [Exemplo de Data Shaping](../../../ado/guide/data/data-shaping-example.md)   
 [Gramática de forma formal](../../../ado/guide/data/formal-shape-grammar.md)   
 [Modelar comandos em geral](../../../ado/guide/data/shape-commands-in-general.md)
