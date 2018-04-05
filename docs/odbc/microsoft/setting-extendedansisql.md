---
title: Configuração ExtendedAnsiSQL | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- extendedANSISQL [ODBC], setting
ms.assetid: 37b775d1-65ac-45ac-8572-454bc4e3c1a2
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: d263d57d9fecbcb03f737dc73472452367900a47
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="setting-extendedansisql"></a>Configuração ExtendedAnsiSQL
O atributo pode ser controlado na cadeia de conexão, adicionando o atributo ExtendedAnsiSQL:  
  
|Valor|Description|  
|-----------|-----------------|  
|ExtendedAnsiSQL = 0 (padrão)|Essa configuração não habilitar os novos recursos.|  
|ExtendedAnsiSQL = 1|Essa configuração permite que os novos recursos.|  
  
 O atributo também pode ser definido em um DSN por meio de **opções avançadas** ao configurar um DSN por meio do painel de controle de caixa de diálogo.  
  
 Definir o atributo como 0 desabilita os novos recursos. definir o valor como 1 permite que os novos recursos.  
  
 O atributo também pode ser definido usando SQLSetConnectAttr(). O valor do atributo é 65501 e é definido como um valor de sqlinteger que contém de 1 ou 0, conforme documentado na tabela anterior. Ele pode ser chamado antes ou depois de se conectar, mas é melhor para chamá-lo depois de se conectar devido a ordem na qual os processos de driver em cache os atributos de conexão e cadeias de caracteres de conexão.
