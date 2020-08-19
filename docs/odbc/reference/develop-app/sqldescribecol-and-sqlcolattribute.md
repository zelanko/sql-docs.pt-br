---
description: SQLDescribeCol e SQLColAttribute
title: SQLDescribeCol e SQLColAttribute | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLColAttribute function [ODBC], and SQLDescribeCol
- SQLDescribeCol function [ODBC], and SQLColAttribute
- result sets [ODBC], metadata
- retrieving result set meta data [ODBC]
- metadata [ODBC], result set
ms.assetid: c2ca442c-03a8-4e0f-9e67-b300bb15962f
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 2de375ea207e8e393fa36c9795ebf0e3ca5f428b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88424498"
---
# <a name="sqldescribecol-and-sqlcolattribute"></a>SQLDescribeCol e SQLColAttribute
**SQLDescribeCol** e **SQLColAttribute** são usados para recuperar metadados do conjunto de resultados. A diferença entre essas duas funções é que **SQLDescribeCol** sempre retorna as mesmas cinco partes de informações (o nome de uma coluna, tipo de dados, precisão, escala e nulidade), enquanto **SQLColAttribute** retorna uma única informação solicitada pelo aplicativo. No entanto, o **SQLColAttribute** pode retornar uma seleção muito mais rica de metadados, incluindo a distinção entre maiúsculas e minúsculas de uma coluna, tamanho de exibição, atualização e capacidade de pesquisa.  
  
 Muitos aplicativos, especialmente aqueles que exibem apenas dados, exigem apenas os metadados retornados por **SQLDescribeCol**. Para esses aplicativos, é mais rápido usar **SQLDescribeCol** do que **SQLColAttribute** , pois as informações são retornadas em uma única chamada. Outros aplicativos, especialmente aqueles que atualizam dados, exigem os metadados adicionais retornados por **SQLColAttribute** e, portanto, usam ambas as funções. Além disso, o **SQLColAttribute** dá suporte a metadados específicos do driver; para obter mais informações, consulte [tipos de dados específicos do driver, tipos de descritores, tipos de informações, tipos de diagnóstico e atributos](../../../odbc/reference/develop-app/driver-specific-data-types-descriptor-information-diagnostic.md).  
  
 Um aplicativo pode recuperar os metadados do conjunto de resultados a qualquer momento depois que uma instrução tiver sido preparada ou executada e antes do cursor sobre o conjunto de resultados ser fechado. Poucos aplicativos exigem metadados do conjunto de resultados depois que a instrução é preparada e antes de ser executada. Se possível, os aplicativos devem aguardar para recuperar metadados até que a instrução seja executada, pois algumas fontes de dados não podem retornar metadados para instruções preparadas e emular esse recurso no driver geralmente é um processo lento. Por exemplo, o driver pode gerar um conjunto de resultados de linha zero, substituindo a cláusula **Where** de uma instrução **Select** pela cláusula **Where 1 = 2** e executando a instrução resultante.  
  
 Geralmente, os metadados são caros de serem recuperados da fonte de dados. Por isso, os drivers devem armazenar em cache todos os metadados que eles recuperam do servidor e mantê-los enquanto o cursor sobre o conjunto de resultados estiver aberto. Além disso, os aplicativos devem solicitar apenas os metadados absolutamente necessários.
