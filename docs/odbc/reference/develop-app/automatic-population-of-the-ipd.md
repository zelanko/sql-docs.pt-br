---
title: Preenchimento automático do IPD | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- automatically populating ipd [ODBC]
- descriptors [ODBC], automatically populating ipd
- descriptors [ODBC], allocating and freeing
- ipd [ODBC]
- allocating and freeing descriptors [ODBC]
ms.assetid: 1184a7d8-d557-4140-843b-6633ae6deacc
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 473594a879fe3bc6ab66937d2cd4e35f1975ecf1
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="automatic-population-of-the-ipd"></a>Preenchimento automático do IPD
Alguns drivers são capazes de definir os campos do IPD depois que uma consulta parametrizada foi preparada. Os campos de descritor são preenchidos automaticamente com informações sobre o parâmetro, incluindo o tipo de dados, precisão, escala e outras características. Isso é equivalente ao suporte **SQLDescribeParam**. Essas informações podem ser especialmente importantes para um aplicativo quando ele não tem outros como descobri-lo, como quando uma consulta ad hoc é executada com parâmetros que o aplicativo não conhece.  
  
 Um aplicativo que determina se o driver oferece suporte à população automática chamando **SQLGetConnectAttr** com um *atributo* de SQL_ATTR_AUTO_IPD. Se SQL_TRUE for retornado, o driver oferece suporte a ele e o aplicativo poderá habilitá-lo definindo o atributo da instrução SQL_ATTR_ENABLE_AUTO_IPD como SQL_TRUE.  
  
 Quando a população automática é suportada e habilitada, o driver preenche os campos do IPD depois que uma instrução SQL que contém os marcadores de parâmetro foi preparada por uma chamada para **SQLPrepare**. Um aplicativo pode recuperar essas informações chamando **SQLGetDescField** ou **SQLGetDescRec**, ou **SQLDescribeParam**. O aplicativo pode usar as informações para associar o buffer de aplicativo mais apropriado para um parâmetro ou especificar uma conversão de dados para ele.  
  
 Preenchimento automático do IPD pode produzir uma penalidade de desempenho. Um aplicativo pode desativá-lo, redefinindo o atributo da instrução SQL_ATTR_ENABLE_AUTO_IPD para SQL_FALSE (o valor padrão).
