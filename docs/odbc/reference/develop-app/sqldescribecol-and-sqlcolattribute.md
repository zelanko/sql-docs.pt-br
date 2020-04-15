---
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
ms.openlocfilehash: 8bd21010908473e4216a02a504b2de25578d5c84
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299756"
---
# <a name="sqldescribecol-and-sqlcolattribute"></a>SQLDescribeCol e SQLColAttribute
**SQLDescribeCol** e **SQLColAttribute** são usados para recuperar metadados do conjunto de resultados. A diferença entre essas duas funções é que **o SQLDescribeCol** sempre retorna as mesmas cinco informações (nome de uma coluna, tipo de dados, precisão, escala e nulidade), enquanto **sQLColAttribute** retorna uma única peça de informação solicitada pelo aplicativo. No entanto, **o SQLColAttribute** pode retornar uma seleção muito mais rica de metadados, incluindo a sensibilidade ao caso de uma coluna, o tamanho da exibição, a updatability e a capacidade de pesquisa.  
  
 Muitos aplicativos, especialmente aqueles que exibem apenas dados, exigem apenas os metadados retornados pelo **SQLDescribeCol**. Para esses aplicativos, é mais rápido usar **SQLDescribeCol** do que **SQLColAttribute** porque as informações são retornadas em uma única chamada. Outros aplicativos, especialmente aqueles que atualizam dados, exigem os metadados adicionais retornados pelo **SQLColAttribute** e, portanto, usam ambas as funções. Além disso, **o SQLColAttribute** suporta metadados específicos do driver; para obter mais informações, consulte [Tipos de dados específicos do driver, tipos de descritores, tipos de informações, tipos de diagnóstico e atributos](../../../odbc/reference/develop-app/driver-specific-data-types-descriptor-information-diagnostic.md).  
  
 Um aplicativo pode recuperar metadados definidos por resultados a qualquer momento após a preparação ou execução de uma declaração e antes que o cursor sobre o conjunto de resultados seja fechado. Muito poucos aplicativos requerem metadados definidos por resultados após a declaração ser preparada e antes de ser executada. Se possível, os aplicativos devem esperar para recuperar metadados até que a instrução seja executada, pois algumas fontes de dados não podem retornar metadados para declarações preparadas e emular esse recurso no driver é muitas vezes um processo lento. Por exemplo, o driver pode gerar um resultado de linha zero definido substituindo a cláusula **WHERE** de uma declaração **SELECT** pela cláusula **WHERE 1 = 2** e executando a declaração resultante.  
  
 Metadados são muitas vezes caros para recuperar da fonte de dados. Por causa disso, os drivers devem armazenar qualquer metadados que recuperem do servidor e segurá-los enquanto o cursor sobre o conjunto de resultados estiver aberto. Além disso, os aplicativos devem solicitar apenas os metadados de que precisam.
