---
title: População Automática do IPD | Microsoft Docs
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81285066"
---
# <a name="automatic-population-of-the-ipd"></a>Preenchimento automático do IPD
Alguns drivers são capazes de definir os campos do IPD depois que uma consulta parametrizada foi preparada. Os campos descritores são preenchidos automaticamente com informações sobre o parâmetro, incluindo o tipo de dados, precisão, escala e outras características. Isso equivale ao suporte ao **SQLDescribeParam**. Essas informações podem ser particularmente valiosas para um aplicativo quando não há outra maneira de descobri-la, como quando uma consulta ad hoc é realizada com parâmetros que o aplicativo não conhece.  
  
 Um aplicativo determina se o driver suporta população automática ligando para **SQLGetConnectAttr** com um *atributo* de SQL_ATTR_AUTO_IPD. Se SQL_TRUE for devolvida, o driver o suporta e o aplicativo pode habilitá-lo definindo o atributo de declaração SQL_ATTR_ENABLE_AUTO_IPD para SQL_TRUE.  
  
 Quando a população automática é suportada e habilitada, o driver preenche os campos do IPD após uma declaração SQL contendo marcadores de parâmetros ter sido preparada por uma chamada para **SQLPrepare**. Um aplicativo pode recuperar essas informações ligando para **SQLGetDescField** ou **SQLGetDescRec**ou **SQLDescribeParam**. O aplicativo pode usar as informações para vincular o buffer de aplicativo mais apropriado para um parâmetro ou para especificar uma conversão de dados para ele.  
  
 A população automática do IPD pode produzir uma penalidade de desempenho. Um aplicativo pode desatimá-lo redefinindo o atributo de declaração SQL_ATTR_ENABLE_AUTO_IPD para SQL_FALSE (o valor padrão).
