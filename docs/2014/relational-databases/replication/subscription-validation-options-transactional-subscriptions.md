---
title: Opções de Validação de Assinatura (assinaturas transacionais) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.validate.options.f1
helpviewer_keywords:
- Subscription Validation Options dialog box
ms.assetid: fd66ad1f-df01-4240-9e89-8f41bff12c1e
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: a82e13202209121897a5e5878a141c8d53800a47
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62745417"
---
# <a name="subscription-validation-options-transactional-subscriptions"></a>Opções de Validação de Assinatura (assinaturas transacionais)
  Use a caixa de diálogo **Opções de Validação de Assinatura** para especificar se a validação deve usar somente uma contagem de linha ou uma contagem de linhas e uma soma de verificação binária.  
  
## <a name="options"></a>Opções  
 **Verifique se o Assinante tem o mesmo número de linhas dos dados replicados que o Publicador**  
 Selecione o tipo de validação de contagem de linhas a ser executado. Para publicações Oracle, a única opção disponível é **Calcular uma contagem de linhas real consultando as tabelas diretamente**.  
  
 **Comparar as somas de verificação para verificar os dados da linha**  
 Além de contar o número de linhas no Publicador e no Assinante, uma soma de verificação de todos os dados é calculada usando o algoritmo de soma de verificação binária. Se a contagem de linhas falhar, a soma de verificação não será executada.  
  
 **Interromper o Distribution Agent após a conclusão da validação**  
 Por padrão, o Distribution Agent executa continuamente. Selecione essa opção para interromper o agente depois que validação for executada. Isso permite verificar se validação teve êxito antes de continuar replicando dados para o Assinante.  
  
## <a name="see-also"></a>Consulte Também  
 [Validar dados no assinante](validate-data-at-the-subscriber.md)   
 [Validar os dados replicados](validate-data-at-the-subscriber.md)  
  
  
