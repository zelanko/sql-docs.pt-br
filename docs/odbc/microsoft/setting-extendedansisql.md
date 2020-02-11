---
title: Configurando ExtendedAnsiSQL | Microsoft Docs
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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68063606"
---
# <a name="setting-extendedansisql"></a>Configurar o ExtendedAnsiSQL
O atributo pode ser controlado na cadeia de conexão adicionando o atributo ExtendedAnsiSQL:  
  
|Valor|DESCRIÇÃO|  
|-----------|-----------------|  
|ExtendedAnsiSQL = 0 (padrão)|Essa configuração não habilita os novos recursos.|  
|ExtendedAnsiSQL = 1|Essa configuração habilita os novos recursos.|  
  
 O atributo também pode ser definido em um DSN por meio da caixa de diálogo **Opções avançadas** ao configurar um DSN por meio do painel de controle.  
  
 Definir o atributo como 0 desabilita os novos recursos; defini-lo como 1 habilita os novos recursos.  
  
 O atributo também pode ser definido usando SQLSetConnectAttr (). O valor do atributo é 65501 e é definido como um valor sqlinteiro igual a 1 ou 0, conforme documentado na tabela anterior. Ele pode ser chamado antes ou depois da conexão, mas é melhor chamá-lo após a conexão devido à ordem em que o driver processa atributos de conexão em cache e cadeias de conexão.
