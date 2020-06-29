---
title: Opções de Atributo Fixo e de Alteração (Assistente para Dimensões de Alteração Lenta) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.loaddimwizard.attriboption.f1
ms.assetid: c841345c-7d03-452f-9379-1c8c464f029c
author: chugugrace
ms.author: chugu
ms.openlocfilehash: df654cd97b343179828ebd94dea40eacc90e003d
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/26/2020
ms.locfileid: "85430563"
---
# <a name="fixed-and-changing-attribute-options-slowly-changing-dimension-wizard"></a>Opções de Atributo Fixo e de Alteração (Assistente para Dimensões de Alteração Lenta)
  Use a caixa de diálogo **Opções de Atributo Fixo e de Alteração** para especificar como responder a mudanças nos atributos fixos e de alteração.  
  
 Para obter mais informações sobre este assistente, consulte [Slowly Changing Dimension Transformation](slowly-changing-dimension-transformation.md).  
  
## <a name="options"></a>Opções  
 **Atributos fixos**  
 Para os atributos fixos, indique se a tarefa falhará se uma mudança for detectada em um atributo fixo.  
  
 **Atributos de alteração**  
 Para alterar atributos, indique se a tarefa alterará registros antigos ou expirados, além de registros atuais, quando uma mudança for detectada em um atributo de alteração. Um registro expirado é um registro que foi substituído por um registro mais novo por uma alteração em um atributo histórico (uma alteração Tipo 2). A seleção desta opção pode impor requisitos de processamento adicionais em um objeto multidimensional construído no data warehouse relacional.  
  
## <a name="see-also"></a>Consulte Também  
 [Configurar saídas por meio do Assistente para Dimensões de Alteração Lenta](configure-outputs-using-the-slowly-changing-dimension-wizard.md)  
  
  
