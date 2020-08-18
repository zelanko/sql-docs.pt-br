---
description: Configurar o ExtendedAnsiSQL
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a5a2d739a3093b0d1e806bc9aa3f8d136746954c
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88412442"
---
# <a name="setting-extendedansisql"></a>Configurar o ExtendedAnsiSQL
O atributo pode ser controlado na cadeia de conexão adicionando o atributo ExtendedAnsiSQL:  
  
|Valor|Descrição|  
|-----------|-----------------|  
|ExtendedAnsiSQL = 0 (padrão)|Essa configuração não habilita os novos recursos.|  
|ExtendedAnsiSQL = 1|Essa configuração habilita os novos recursos.|  
  
 O atributo também pode ser definido em um DSN por meio da caixa de diálogo **Opções avançadas** ao configurar um DSN por meio do painel de controle.  
  
 Definir o atributo como 0 desabilita os novos recursos; defini-lo como 1 habilita os novos recursos.  
  
 O atributo também pode ser definido usando SQLSetConnectAttr (). O valor do atributo é 65501 e é definido como um valor sqlinteiro igual a 1 ou 0, conforme documentado na tabela anterior. Ele pode ser chamado antes ou depois da conexão, mas é melhor chamá-lo após a conexão devido à ordem em que o driver processa atributos de conexão em cache e cadeias de conexão.
