---
title: Definir inteligência de conta (Assistente para dimensões) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.dimensionwizard.accountintelligencetypemapping.f1
ms.assetid: cbcff072-3a7e-4e98-858f-1b4265461561
author: minewiskan
ms.author: owend
ms.openlocfilehash: 0b218c10826253bc63985e2eb970a4102873e699
ms.sourcegitcommit: 2f166e139f637d6edfb5731510d632a13205eb25
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/08/2020
ms.locfileid: "84528852"
---
# <a name="define-account-intelligence-dimension-wizard"></a>Definir Inteligência de Conta (Assistente de Business Intelligence)
  Use a página **Definir Inteligência de Conta** para mapear tipos de conta definidos na instância do [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] para tipos de conta definidos no atributo de dimensão associado ao atributo **Tipo de Conta** na dimensão.  
  
> [!NOTE]  
>   Essa página é exibida apenas de você tiver selecionado **Dimensão padrão** na página **Selecionar o Tipo de Dimensão** e se tiver mapeado um atributo de dimensão para o tipo de atributo **Tipo de Conta** na página **Especificar Tipo de Dimensão** .  
  
## <a name="options"></a>Opções  
 **Tipos de Conta de Tabela de Origem**  
 Exibe os valores contidos no atributo de dimensão atribuídos ao atributo **Tipo de Conta** na página **Especificar Chave e Tipo de Dimensão** .  
  
 **Tipos de Conta Interna**  
 Selecione o tipo de conta definido na instância do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] que mapeia para os tipos de conta na tabela de origem.  
  
 A tabela a seguir lista os tipos de conta que estão definidos em uma instância do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] .  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**Ativo**|Valor de itens possuídos em um momento específico.|  
|**Saldo**|Contagem de algo em um momento específico.|  
|**Despesa**|Valor de despesas efetuadas.|  
|**Flow**|Contagem incremental de itens.|  
|**Líqui**|Valor de itens recebidos.|  
|**Dívida**|Valor de itens devidos em um momento específico.|  
|**Estatística**|Taxa calculada de algo ou contagem de algo que não agrega.|  
  
## <a name="see-also"></a>Consulte Também  
 [Ajuda F1 do assistente para dimensões](dimension-wizard-f1-help.md)   
 [Dimensões &#40;Analysis Services de dados multidimensionais&#41;](multidimensional-models-olap-logical-dimension-objects/dimensions-analysis-services-multidimensional-data.md)   
 [Dimensões em modelos multidimensionais](multidimensional-models/dimensions-in-multidimensional-models.md)  
  
  
