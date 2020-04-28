---
title: População automática do IPD | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- automatically populating ipd [ODBC]
- descriptors [ODBC], automatically populating ipd
- descriptors [ODBC], allocating and freeing
- ipd [ODBC]
- allocating and freeing descriptors [ODBC]
ms.assetid: 1184a7d8-d557-4140-843b-6633ae6deacc
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 1998ea1992ee7f14d87d01e348d955b017166088
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81285066"
---
# <a name="automatic-population-of-the-ipd"></a>Preenchimento automático do IPD
Alguns drivers são capazes de definir os campos do IPD depois que uma consulta parametrizada tiver sido preparada. Os campos de descritor são preenchidos automaticamente com informações sobre o parâmetro, incluindo o tipo de dados, a precisão, a escala e outras características. Isso é equivalente ao suporte a **SQLDescribeParam**. Essas informações podem ser particularmente valiosas para um aplicativo quando não há nenhuma outra maneira de descobri-lo, como quando uma consulta ad hoc é executada com parâmetros que o aplicativo não conhece.  
  
 Um aplicativo determina se o driver dá suporte à população automática chamando **SQLGetConnectAttr** com um *atributo* de SQL_ATTR_AUTO_IPD. Se SQL_TRUE for retornado, o driver dará suporte a ele e o aplicativo poderá habilitá-lo definindo o atributo SQL_ATTR_ENABLE_AUTO_IPD Statement como SQL_TRUE.  
  
 Quando a população automática tem suporte e está habilitada, o driver popula os campos do IPD depois que uma instrução SQL que contém marcadores de parâmetro foi preparada por uma chamada para **SQLPrepare**. Um aplicativo pode recuperar essas informações chamando **SQLGetDescField** ou **SQLGetDescRec**, ou **SQLDescribeParam**. O aplicativo pode usar as informações para associar o buffer de aplicativo mais apropriado para um parâmetro ou para especificar uma conversão de dados para ele.  
  
 A população automática do IPD pode produzir uma penalidade de desempenho. Um aplicativo pode desativá-lo redefinindo o atributo da instrução SQL_ATTR_ENABLE_AUTO_IPD como SQL_FALSE (o valor padrão).
