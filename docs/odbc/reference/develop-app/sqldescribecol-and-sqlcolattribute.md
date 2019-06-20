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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e569e51540cbaa5612b158abdacac5faae77f940
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63149026"
---
# <a name="sqldescribecol-and-sqlcolattribute"></a>SQLDescribeCol e SQLColAttribute
**SQLDescribeCol** e **SQLColAttribute** são usados para recuperar metadados de conjunto de resultados. A diferença entre essas duas funções é que **SQLDescribeCol** sempre retorna as mesmas cinco peças de informação (uma coluna Nome, tipo de dados, precisão, escala e nulidade), enquanto **SQLColAttribute** retorna uma única informação solicitada pelo aplicativo. No entanto, **SQLColAttribute** pode retornar uma seleção muito mais sofisticada de metadados, incluindo diferenciação de maiusculas e minúsculas da coluna, exibir o tamanho, a capacidade de atualização e a capacidade de pesquisa.  
  
 Muitos aplicativos, especialmente aqueles que só exibem dados, exigem somente metadados retornados pelo **SQLDescribeCol**. Para esses aplicativos, ele é mais rápido usar **SQLDescribeCol** que **SQLColAttribute** porque as informações são retornadas em uma única chamada. Outros aplicativos, especialmente aqueles que atualizam dados, requerem metadados adicionais retornados pelo **SQLColAttribute** e, portanto, usar ambas as funções. Além disso, **SQLColAttribute** dá suporte a metadados específicos do driver; para obter mais informações, consulte [tipos de dados específicos do Driver, tipos de descritor, tipos de informação, tipos de diagnóstico e atributos](../../../odbc/reference/develop-app/driver-specific-data-types-descriptor-information-diagnostic.md).  
  
 Um aplicativo pode recuperar metadados de conjunto de resultados a qualquer momento depois que uma instrução tiver sido preparada ou executada e antes do cursor sobre o resultado do conjunto é fechado. Muito poucos aplicativos exigem metadados de conjunto de resultados após a instrução é preparada e antes de ser executado. Se possível, os aplicativos devem esperar para recuperar metadados até depois que a instrução é executada, porque algumas fontes de dados não é possível retornar metadados para instruções preparadas e emular essa funcionalidade no driver geralmente é um processo lento. Por exemplo, o driver pode gerar um resultado de linha de zero definido, substituindo o **onde** cláusula de uma **selecionar** instrução com a cláusula **WHERE 1 = 2** e executando o instrução resultante.  
  
 Metadados costuma ser caro para recuperar da fonte de dados. Por isso, drivers devem armazenar em cache todos os metadados que recuperar do servidor e segure para desde que o cursor sobre o resultado do conjunto estiver aberto. Além disso, os aplicativos devem solicitar apenas os metadados que eles precisam.
