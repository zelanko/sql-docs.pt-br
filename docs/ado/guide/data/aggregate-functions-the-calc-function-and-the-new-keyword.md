---
description: Funções de agregação, a função CALC e a palavra-chave NEW
title: Funções de agregação, a função CALC e a nova palavra-chave | Microsoft Docs
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
author: rothja
ms.author: jroth
ms.openlocfilehash: ad6bf4b041fbae0f30e327bd32dd067c1e9c429a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88453748"
---
# <a name="aggregate-functions-the-calc-function-and-the-new-keyword"></a>Funções de agregação, a função CALC e a palavra-chave NEW
O data Shaping oferece suporte às funções a seguir. O nome atribuído ao capítulo que contém a coluna a ser operada é o *Chapter-alias*.  
  
 Um alias de capítulo pode ser totalmente qualificado, consistindo em cada nome de coluna de capítulo que leva ao capítulo que contém o *nome da coluna,* tudo separado por pontos. Por exemplo, se o capítulo pai, chap1, contiver um capítulo filho, CHAP2, que tem uma coluna amount, AMT, o nome qualificado será chap1. CHAP2. AMT.  
  
|Funções de Agregação|Descrição|  
|-------------------------|-----------------|  
|SUM (*capítulo-alias*.* nome da coluna*)|Calcula a soma de todos os valores na coluna especificada.|  
|AVG (*alias de capítulo*.* nome da coluna*)|Calcula a média de todos os valores na coluna especificada.|  
|MÁX. (*alias de capítulo*.* nome da coluna*)|Calcula o valor máximo na coluna especificada.|  
|MIN (*alias de capítulo*.* nome da coluna*)|Calcula o valor mínimo na coluna especificada.|  
|CONTAGEM (*capítulo-alias*[.* nome da coluna*])|Conta o número de linhas no alias especificado. Se uma coluna for especificada, somente as linhas para as quais essa coluna não for nula serão incluídas na contagem.|  
|DESVPAD (*capítulo-alias*.* nome da coluna*)|Calcula o desvio padrão na coluna especificada.|  
|QUALQUER (*alias de capítulo*.* nome da coluna*)|Um valor da coluna especificada. ANY tem um valor previsível somente quando o valor da coluna é o mesmo para todas as linhas do capítulo.<br /><br /> **Observação** Se a coluna não contiver o mesmo valor para todas as linhas do capítulo, o comando SHAPE, arbitrariamente, retornará um dos valores para ser o valor da função ANY.|  
  
|Expressão calculada|Descrição|  
|---------------------------|-----------------|  
|CALC (*expressão*)|Calcula uma expressão arbitrária, mas apenas na linha do **conjunto de registros** que contém a função Calc. Qualquer expressão que use essas [funções Visual Basic for Applications (VBA)](../../../ado/guide/data/visual-basic-for-applications-functions.md) é permitida.|  
  
|NOVA palavra-chave|Descrição|  
|-----------------|-----------------|  
|NOVO *campo-tipo* [(*largura* &#124; *escala* &#124; *precisão* &#124; *erro* [, *escala* &#124; *erro*])]|Adiciona uma coluna vazia do tipo especificado ao conjunto de **registros**.|  
  
 O *tipo de campo* passado com a nova palavra-chave pode ser qualquer um dos tipos de dados a seguir.  
  
|Tipos de dados OLE DB|Tipo de dados ADO equivalente (s)|  
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
  
 Quando o novo campo é do tipo decimal (em OLE DB, DBTYPE_DECIMAL ou no ADO, adDecimal), você deve especificar os valores de precisão e escala.  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo de formatação de dados](../../../ado/guide/data/data-shaping-example.md)   
 [Gramática forma formal](../../../ado/guide/data/formal-shape-grammar.md)   
 [Modelar comandos em geral](../../../ado/guide/data/shape-commands-in-general.md)
