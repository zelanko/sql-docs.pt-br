---
title: Definir pontos de interrupção | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: wmi
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.setbreakpoints.f1
helpviewer_keywords:
- Set Breakpoints dialog box
ms.assetid: 876e61b7-875c-43f4-bbce-d7eeb90f6730
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 0c2c543343bd602be75d600a489edfd84663790b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62911398"
---
# <a name="set-breakpoints"></a>Definir Pontos de Interrupção
  Use a caixa de diálogo **Definir Pontos de Interrupção** para especificar os eventos nos quais habilitar pontos de interrupção e para controlar o comportamento do ponto de interrupção.  
  
## <a name="options"></a>Opções  
 **Enabled**  
 Selecione para habilitar um ponto de interrupção em um evento.  
  
 **Condição de Interrupção**  
 Exiba uma lista de eventos disponíveis nos quais definir pontos de interrupção.  
  
 **Tipo de Contagem de Ocorrências**  
 Especifique quando o ponto de interrupção entra em vigor.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**Always**|A execução será sempre suspensa quando ocorrer o ponto de interrupção.|  
|**Contagem de ocorrências igual a**|A execução será suspensa quando o número de vezes que o ponto de interrupção ocorreu for igual à contagem de ocorrências.|  
|**Ocorrência maior ou igual**|A execução será suspensa quando o número de vezes que o ponto de interrupção ocorreu for igual ou maior que a contagem de ocorrências.|  
|**Várias contagens de ocorrências**|A execução será suspensa quando ocorrerem várias contagens de ocorrências. Por exemplo, se você definir esta opção como 5, a execução será suspensa a cada quinta vez.|  
  
 **Contagem de Ocorrências**  
 Especifique o número de ocorrências no qual engatilhe uma interrupção. Esta opção não estará disponível se o ponto de interrupção estiver sempre ativado.  
  
## <a name="see-also"></a>Consulte também  
 [Depurando o fluxo de controle](../../../integration-services/troubleshooting/debugging-control-flow.md)  
  
  
