---
title: Escolher aprimoramento (Assistente de Business Intelligence) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.biwizard.bienhancement.f1
ms.assetid: 39e2f36c-2c02-4a71-af8f-5dbd373190dc
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 687f7fb96ee5a2b96d80562c20d536eeeb308379
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66088122"
---
# <a name="choose-enhancement-business-intelligence-wizard"></a>Escolher Aprimoramento (Assistente de Business Intelligence)
  Use a página **Escolher Aprimoramento** para escolher o aprimoramento de business intelligence a ser adicionado ao cubo ou dimensão.  
  
## <a name="options"></a>Opções  
 **Aprimoramentos disponíveis**  
 Selecione o aprimoramento de business intelligence a ser adicionado. A tabela a seguir lista os aprimoramentos disponíveis.  
  
|Aprimoramento|Descrição|  
|-----------------|-----------------|  
|**Definir inteligência de tempo**|Adicione exibições de tempo adicionais para uma hierarquia selecionada. Esses incluem exibições do período até esta data, exibições de média móvel e exibições de período a período.<br /><br /> Observação: Essa opção está disponível apenas para cubos.|  
|**Definir inteligência de conta**|Atribua classificações padrão de contabilidade, como receita e despesa, para membros de um atributo de conta.<br /><br /> Se a função de agregação da medida for configurada como *ByAccount*, a instância do [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] usará as classificações de contabilidade para agregar uma medida entre os membros de um atributo de conta ao longo do tempo.|  
|**Definir inteligência de dimensão**|Use a inteligência de dimensão para especificar um tipo de negócios padrão para uma dimensão e para especificar tipos válidos para os atributos de dimensão. Aplicativos cliente podem usar essas especificações de tipo ao analisar dados.|  
|**Especificar um operador unário**|Especifique um operador unário para substituir a agregação padrão associada a membros de uma hierarquia pai-filho incluída em um cubo.<br /><br /> Observação: Essa opção está disponível apenas para cubos.|  
|**Criar uma fórmula de membro personalizado**|Crie uma fórmula de membro personalizado para substituir a agregação padrão associada a um membro da dimensão por outro operador.|  
|**Especificar a ordenação de atributos**|Especifique como são ordenados os membros de um atributo selecionado. Os membros podem ser ordenados pelo nome ou chave de um atributo selecionado ou pelo nome ou chave de um atributo relacionado ao atributo selecionado. Por padrão, os membros são ordenados pelo nome do atributo selecionado.|  
|**Habilitar write-back de dimensão**|Habilite a modificação manual da estrutura da dimensão. Atualizações em uma dimensão habilitada para gravação são registradas diretamente na tabela de dimensões.|  
|**Definir comportamento semiaditivo**|Defina manualmente o método de agregação para medidas ou membros individuais de um atributo de tipo de conta. Se o cubo contiver uma dimensão de conta, você poderá usar a opção **Definir inteligência de conta** para definir automaticamente o comportamento semiaditivo com base no tipo de conta.<br /><br /> Observação: Essa opção está disponível apenas para cubos.|  
|**Definir conversão de moeda**|Defina regras para converter e analisar dados multinacionais no cubo. Regras de conversão são aplicadas no cubo usando um script MDX gerado pelo Assistente de Business Intelligence.<br /><br /> Observação: Essa opção está disponível apenas para cubos.|  
  
 **Descrição**  
 Fornece uma descrição breve do aprimoramento de business intelligence selecionado.  
  
## <a name="see-also"></a>Consulte também  
 [Ajuda F1 do Assistente de Business Intelligence](business-intelligence-wizard-f1-help.md)   
 [Designer de cubo &#40;Analysis Services - dados multidimensionais&#41;](cube-designer-analysis-services-multidimensional-data.md)   
 [Designer de dimensão &#40;Analysis Services - dados multidimensionais&#41;](dimension-designer-analysis-services-multidimensional-data.md)  
  
  
