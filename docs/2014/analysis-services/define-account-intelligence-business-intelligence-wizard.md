---
title: Definir inteligência de conta (Assistente de Business Intelligence) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.biwizard.acctintelligence.mapaccounttype.f1
ms.assetid: fe4c204b-1031-4ac4-9916-8052ce2301cc
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 51e19ed19c78903be0565461871ccc0b00460002
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66082195"
---
# <a name="define-account-intelligence-business-intelligence-wizard"></a>Definir Inteligência de Conta (Assistente de Business Intelligence)
  Use a página **Definir Inteligência de Conta** para mapear tipos de conta definidos na instância do [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] como tipos de conta definidos por uma tabela de origem na fonte de dados que fornece os dados para a dimensão de conta.  
  
> [!NOTE]  
>  Essa página será exibida se um atributo de dimensão tiver sido mapeado para o atributo **Tipo de Conta** na página **Configurar Atributos de Dimensão** .  
  
## <a name="options"></a>Opções  
 **Tipos de conta de tabela de origem**  
 Exibe os valores contidos no atributo de dimensão atribuído ao atributo **Tipo de Conta** na página **Configurar Atributos de Dimensão** .  
  
 **Tipos de conta interna**  
 Selecione o tipo de conta definido na instância do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] que mapeia para os tipos de conta na tabela de origem.  
  
 A tabela a seguir lista os tipos de conta que estão definidos em uma instância do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] .  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**Ativo**|Valor de itens possuídos em um momento específico.|  
|**Saldo**|Contagem de algo em um momento específico.|  
|**Despesa**|Valor de despesas efetuadas.|  
|**Fluxo**|Contagem incremental de itens.|  
|**Receita**|Valor de itens recebidos.|  
|**Dívida**|Valor de itens devidos em um momento específico.|  
|**Estatística**|Taxa calculada de algo ou contagem de algo que não agrega.|  
  
## <a name="see-also"></a>Consulte também  
 [Ajuda F1 do Assistente de Business Intelligence](business-intelligence-wizard-f1-help.md)   
 [Designer de cubo &#40;Analysis Services - dados multidimensionais&#41;](cube-designer-analysis-services-multidimensional-data.md)   
 [Designer de dimensão &#40;Analysis Services - dados multidimensionais&#41;](dimension-designer-analysis-services-multidimensional-data.md)  
  
  
