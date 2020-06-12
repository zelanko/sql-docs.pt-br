---
title: Criando procedimentos armazenados | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- stored procedures [Analysis Services], designing
- dependent assemblies [Analysis Services]
- assemblies [Analysis Services]
ms.assetid: af4e7bd5-041b-4a40-9942-0ef6a3af46c6
author: minewiskan
ms.author: owend
ms.openlocfilehash: 42b33873d6bdf28f7f702bcf186d681f57d6024d
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/09/2020
ms.locfileid: "84545358"
---
# <a name="designing-stored-procedures"></a>Projetando procedimentos armazenados
  Tanto o Analysis Management Objects (AMO) do modelo de objeto administrativo como o [!INCLUDE[msCoName](../../includes/msconame-md.md)] ActiveX® Data Objects (Multidimensional) (ADO MD) do modelo de objeto orientado a cliente estão disponíveis nos procedimentos armazenados.  
  
 Os procedimentos armazenados devem estar no escopo (do servidor ou do banco de dados) para serem visíveis no nível da linguagem MDX que serão chamadas. No entanto, uma vez um chamado o procedimento armazenado, seu escopo não fica limitado a ações sob seu pai. Um procedimento armazenado pode fazer alterações ou modificações em qualquer lugar do servidor, sujeito apenas às limitações de segurança do processo do usuário que o chama ou às limitações da transação em que está operando.  
  
 Procedimentos de escopo de servidor ficam disponíveis em todos os contextos no servidor. Procedimentos armazenados de escopo de banco de dados ficam visíveis apenas no contexto do banco de dados no qual foram definidos.  
  
 Como toda função MDX, o procedimento armazenado deve ser resolvido antes que a sessão MDX possa prosseguir; os procedimentos armazenados bloqueiam as sessões MDX durante sua execução. A menos que exista um motivo específico para parar uma sessão MDX à espera de uma interação do usuário, qualquer interação do usuário (como caixas de diálogo) não são aconselhadas.  
  
## <a name="dependent-assemblies"></a>Assemblies dependentes  
 Todos os assemblies dependentes devem ser carregados em uma instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] para serem localizados pelo CLR (Common Language Runtime). O [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] armazena os assemblies dependentes na mesma pasta do assembly principal, de modo que o CLR resolve automaticamente todas as referências das funções para as funções desses assemblies.  
  
## <a name="see-also"></a>Consulte Também  
 [Gerenciamento de assemblies de modelo multidimensional](../multidimensional-models/multidimensional-model-assemblies-management.md)   
 [Definindo procedimentos armazenados](../multidimensional-models-extending-olap-stored-procedures/defining-stored-procedures.md)  
  
  
