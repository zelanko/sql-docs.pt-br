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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3d127e2da3397e96059c7d04305a983766ca1db6
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47767304"
---
# <a name="automatic-population-of-the-ipd"></a>Preenchimento automático do IPD
Alguns drivers são capazes de definir os campos do IPD depois que uma consulta parametrizada preparada. Os campos de descritor são preenchidos automaticamente com informações sobre o parâmetro, incluindo o tipo de dados, precisão, escala e outras características. Isso é equivalente a dar suporte a **SQLDescribeParam**. Essas informações podem ser especialmente importantes para um aplicativo quando ele tiver nenhuma outra maneira de descobri-lo, como quando uma consulta ad hoc é executada com os parâmetros que o aplicativo não conhece.  
  
 Um aplicativo que determina se o driver dá suporte a população automática chamando **SQLGetConnectAttr** com um *atributo* de SQL_ATTR_AUTO_IPD. Se SQL_TRUE for retornado, o driver dá suporte a ele e o aplicativo poderá habilitá-lo definindo o atributo da instrução SQL_ATTR_ENABLE_AUTO_IPD como SQL_TRUE.  
  
 Quando a população automática é compatível e habilitada, o driver preenche os campos do IPD depois que uma instrução SQL que contenham marcadores de parâmetro foi preparada por uma chamada para **SQLPrepare**. Um aplicativo pode recuperar essas informações por meio da chamada **SQLGetDescField** ou **SQLGetDescRec**, ou **SQLDescribeParam**. O aplicativo pode usar as informações para associar o buffer de aplicativo mais apropriado para um parâmetro ou especificar uma conversão de dados para ele.  
  
 População automática do IPD pode produzir uma penalidade de desempenho. Um aplicativo pode desativá-lo, redefinindo o atributo da instrução SQL_ATTR_ENABLE_AUTO_IPD para SQL_FALSE (o valor padrão).
