---
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ae95160a11a965e47845726748c2b9449a819e8a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63284959"
---
# <a name="retrieving-the-values-in-descriptor-fields"></a>Recuperar os valores nos campos de descritor
Um aplicativo pode chamar **SQLGetDescField** para obter um único campo de um registro do descritor. **SQLGetDescField** fornece ao aplicativo acesso para todos os campos de descritor definidos no ODBC e também campos definidos pelo driver.  
  
 **SQLGetDescRec** pode ser chamado para recuperar as configurações de vários campos de descritor que afetam o tipo de dados e armazenamento de dados de coluna ou parâmetro.
