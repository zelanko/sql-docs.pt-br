---
title: Recuperando os valores nos campos de descritor | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- descriptors [ODBC], retrieving or setting field values
ms.assetid: c05b180f-c2b0-437b-8d1c-ce7f4da93287
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b8284167a27439c65256ee4559210843ec7dcffe
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32911381"
---
# <a name="retrieving-the-values-in-descriptor-fields"></a>Recuperando os valores nos campos de descritor
Um aplicativo pode chamar **SQLGetDescField** para obter um único campo de um registro do descritor. **SQLGetDescField** fornece o acesso de aplicativo para todos os campos de descritor definidos no ODBC e também os campos definidos pelo driver.  
  
 **SQLGetDescRec** pode ser chamado para recuperar as configurações de vários campos de descritor que afetam o tipo de dados e armazenamento de dados de coluna ou parâmetro.
