---
title: Configurando o ExtendedAnsiSQL | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- extendedANSISQL [ODBC], setting
ms.assetid: 37b775d1-65ac-45ac-8572-454bc4e3c1a2
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 330b55ef2d4fee090c453990d3fe75e6e2dacb6f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68063606"
---
# <a name="setting-extendedansisql"></a>Configurar o ExtendedAnsiSQL
O atributo pode ser controlado na cadeia de conexão, adicionando o atributo ExtendedAnsiSQL:  
  
|Valor|Descrição|  
|-----------|-----------------|  
|ExtendedAnsiSQL = 0 (padrão)|Essa configuração não permite os novos recursos.|  
|ExtendedAnsiSQL=1|Essa configuração permite que os novos recursos.|  
  
 O atributo também pode ser definido em um DSN por meio de **opções avançadas de** ao configurar um DSN por meio do painel de controle de caixa de diálogo.  
  
 Configurar o atributo para 0 desabilita os novos recursos. Configurando-a como 1 habilita os recursos novos.  
  
 O atributo também pode ser definido usando SQLSetConnectAttr(). O valor do atributo é 65501 e é definido como um valor de sqlinteger que contém de 1 ou 0, conforme documentado na tabela anterior. Ele pode ser chamado antes ou depois de se conectar, mas é melhor para chamá-lo após a conexão devido à ordem na qual os processos de driver em cache os atributos de conexão e cadeias de caracteres de conexão.
