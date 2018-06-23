---
title: Definir inteligência de conta (Assistente para dimensões) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.asvs.dimensionwizard.accountintelligencetypemapping.f1
ms.assetid: cbcff072-3a7e-4e98-858f-1b4265461561
caps.latest.revision: 26
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 27c0a8d48ae1a4a69ea96c4c87cc7cf8d0f1f1d3
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36007154"
---
# <a name="define-account-intelligence-dimension-wizard"></a>Definir Inteligência de Conta (Assistente de Business Intelligence)
  Use a página **Definir Inteligência de Conta** para mapear tipos de conta definidos na instância do [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] para tipos de conta definidos no atributo de dimensão associado ao atributo **Tipo de Conta** na dimensão.  
  
> [!NOTE]  
>  Essa página será exibida apenas se você tiver selecionado **Dimensão padrão** na página **Selecionar o Tipo de Dimensão** e se tiver mapeado um atributo de dimensão para o tipo de atributo **Tipo de Conta** na página **Especificar Tipo de Dimensão** .  
  
## <a name="options"></a>Opções  
 **Tipos de conta da tabela de origem**  
 Exibe os valores contidos no atributo de dimensão atribuídos ao atributo **Tipo de Conta** na página **Especificar Chave e Tipo de Dimensão** .  
  
 **Tipos de conta interna**  
 Selecione o tipo de conta definido na instância do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] que mapeia para os tipos de conta na tabela de origem.  
  
 A tabela a seguir lista os tipos de conta que estão definidos em uma instância do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] .  
  
|Valor|Description|  
|-----------|-----------------|  
|**Ativo**|Valor de itens possuídos em um momento específico.|  
|**Saldo**|Contagem de algo em um momento específico.|  
|**Despesa**|Valor de despesas efetuadas.|  
|**Fluxo**|Contagem incremental de itens.|  
|**Receita**|Valor de itens recebidos.|  
|**Dívida**|Valor de itens devidos em um momento específico.|  
|**Estatística**|Taxa calculada de algo ou contagem de algo que não agrega.|  
  
## <a name="see-also"></a>Consulte também  
 [Ajuda de F1 do Assistente de dimensão](dimension-wizard-f1-help.md)   
 [Dimensões &#40;Analysis Services - dados multidimensionais&#41;](multidimensional-models-olap-logical-dimension-objects/dimensions-analysis-services-multidimensional-data.md)   
 [Dimensões em modelos multidimensionais](multidimensional-models/dimensions-in-multidimensional-models.md)  
  
  