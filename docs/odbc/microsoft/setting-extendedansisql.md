---
title: Configuração ExtendedAnsiSQL | Microsoft Docs
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
ms.openlocfilehash: 6b5c2e4ed4d8bd64d02fb6a62861db832f6b0898
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300796"
---
# <a name="setting-extendedansisql"></a>Configurar o ExtendedAnsiSQL
O atributo pode ser controlado na seqüência de conexões adicionando o atributo ExtendedAnsiSQL:  
  
|Valor|Descrição|  
|-----------|-----------------|  
|AnsiSQL estendida=0 (padrão)|Esta configuração não habilita os novos recursos.|  
|AnsiSQL estendida=1|Esta configuração permite os novos recursos.|  
  
 O atributo também pode ser definido em um DSN através da caixa de diálogo **Opções Avançadas** ao configurar um DSN através do Painel de Controle.  
  
 Definir o atributo como 0 desativa os novos recursos; configurá-lo para 1 habilita os novos recursos.  
  
 O atributo também pode ser definido usando SQLSetConnectAttr(). O valor do atributo é 65501 e é definido como um valor SQLINTEGER de 1 ou 0, conforme documentado na tabela anterior. Ele pode ser chamado antes ou depois de se conectar, mas é melhor chamá-lo depois de se conectar por causa da ordem em que o driver processa atributos de conexão cacheados e strings de conexão.
