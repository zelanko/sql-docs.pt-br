---
description: Recuperar os valores nos campos de descritor
title: Recuperando os valores nos campos de descritor | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- descriptors [ODBC], retrieving or setting field values
ms.assetid: c05b180f-c2b0-437b-8d1c-ce7f4da93287
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a2118efe58b076287dd75192de679bdb74299435
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88494644"
---
# <a name="retrieving-the-values-in-descriptor-fields"></a>Recuperar os valores nos campos de descritor
Um aplicativo pode chamar **SQLGetDescField** para obter um único campo de um registro de descritor. O **SQLGetDescField** fornece ao aplicativo acesso a todos os campos de descritor definidos em ODBC e também a campos definidos por driver.  
  
 **SQLGetDescRec** pode ser chamado para recuperar as configurações de vários campos de descritor que afetam o tipo de dados e o armazenamento de dados de coluna ou parâmetro.
