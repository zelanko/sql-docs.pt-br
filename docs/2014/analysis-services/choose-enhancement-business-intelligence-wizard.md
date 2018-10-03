---
title: Escolher aprimoramento (Assistente de Business Intelligence) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.biwizard.bienhancement.f1
ms.assetid: 39e2f36c-2c02-4a71-af8f-5dbd373190dc
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 8834e8412cedbd2d97f9b5717f2e7979999a0a06
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48196187"
---
# <a name="choose-enhancement-business-intelligence-wizard"></a>Escolher Aprimoramento (Assistente de Business Intelligence)
  Use a página **Escolher Aprimoramento** para escolher o aprimoramento de business intelligence a ser adicionado ao cubo ou dimensão.  
  
## <a name="options"></a>Opções  
 **Aprimoramentos disponíveis**  
 Selecione o aprimoramento de business intelligence a ser adicionado. A tabela a seguir lista os aprimoramentos disponíveis.  
  
|Aprimoramento|Description|  
|-----------------|-----------------|  
|**Definir inteligência de tempo**|Adicione exibições de tempo adicionais para uma hierarquia selecionada. Esses incluem exibições do período até esta data, exibições de média móvel e exibições de período a período.<br /><br /> Observação: essa opção está disponível apenas para cubos.|  
|**Definir inteligência de conta**|Atribua classificações padrão de contabilidade, como receita e despesa, para membros de um atributo de conta.<br /><br /> Se a função de agregação da medida for configurada como *ByAccount*, a instância do [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] usará as classificações de contabilidade para agregar uma medida entre os membros de um atributo de conta ao longo do tempo.|  
|**Definir inteligência de dimensão**|Use a inteligência de dimensão para especificar um tipo de negócios padrão para uma dimensão e para especificar tipos válidos para os atributos de dimensão. Aplicativos cliente podem usar essas especificações de tipo ao analisar dados.|  
|**Especificar um operador unário**|Especifique um operador unário para substituir a agregação padrão associada a membros de uma hierarquia pai-filho incluída em um cubo.<br /><br /> Observação: essa opção está disponível apenas para cubos.|  
|**Criar uma fórmula de membro personalizado**|Crie uma fórmula de membro personalizado para substituir a agregação padrão associada a um membro da dimensão por outro operador.|  
|**Especificar a ordenação de atributos**|Especifique como são ordenados os membros de um atributo selecionado. Os membros podem ser ordenados pelo nome ou chave de um atributo selecionado ou pelo nome ou chave de um atributo relacionado ao atributo selecionado. Por padrão, os membros são ordenados pelo nome do atributo selecionado.|  
|**Habilitar write-back de dimensão**|Habilite a modificação manual da estrutura da dimensão. Atualizações em uma dimensão habilitada para gravação são registradas diretamente na tabela de dimensões.|  
|**Definir comportamento semiaditivo**|Defina manualmente o método de agregação para medidas ou membros individuais de um atributo de tipo de conta. Se o cubo contiver uma dimensão de conta, você poderá usar a opção **Definir inteligência de conta** para definir automaticamente o comportamento semiaditivo com base no tipo de conta.<br /><br /> Observação: essa opção está disponível apenas para cubos.|  
|**Definir conversão de moeda**|Defina regras para converter e analisar dados multinacionais no cubo. Regras de conversão são aplicadas no cubo usando um script MDX gerado pelo Assistente de Business Intelligence.<br /><br /> Observação: essa opção está disponível apenas para cubos.|  
  
 **Descrição**  
 Fornece uma descrição breve do aprimoramento de business intelligence selecionado.  
  
## <a name="see-also"></a>Consulte também  
 [Ajuda de F1 do Assistente do Business Intelligence](business-intelligence-wizard-f1-help.md)   
 [Designer de cubo &#40;Analysis Services - dados multidimensionais&#41;](cube-designer-analysis-services-multidimensional-data.md)   
 [Designer de dimensão &#40;Analysis Services - dados multidimensionais&#41;](dimension-designer-analysis-services-multidimensional-data.md)  
  
  
