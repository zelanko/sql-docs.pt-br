---
title: Recuperando os valores nos campos de descritor | Microsoft Docs
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
- descriptors [ODBC], retrieving or setting field values
ms.assetid: c05b180f-c2b0-437b-8d1c-ce7f4da93287
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 05d05eb20fdfa603748e4819d7f7583c6576a0b8
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="retrieving-the-values-in-descriptor-fields"></a>Recuperando os valores nos campos de descritor
Um aplicativo pode chamar **SQLGetDescField** para obter um único campo de um registro do descritor. **SQLGetDescField** fornece o acesso de aplicativo para todos os campos de descritor definidos no ODBC e também os campos definidos pelo driver.  
  
 **SQLGetDescRec** pode ser chamado para recuperar as configurações de vários campos de descritor que afetam o tipo de dados e armazenamento de dados de coluna ou parâmetro.
