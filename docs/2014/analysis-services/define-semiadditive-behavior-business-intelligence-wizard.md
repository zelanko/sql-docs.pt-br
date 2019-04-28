---
title: Definir comportamento Semiaditivo (Assistente de Business Intelligence) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.biwizard.semiadditivememberdetection.f1
ms.assetid: e57080ba-ce96-40f8-bca7-6701d1725b3c
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 436610a4c52d213a2d5b80c4277988b615f81449
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62732152"
---
# <a name="define-semiadditive-behavior-business-intelligence-wizard"></a>Definir Comportamento Semiaditivo (Assistente de Business Intelligence)
  Use a página **Definir Comportamento Semiaditivo** para habilitar ou desabilitar comportamento semiaditivo em medidas. O comportamento semiaditivo determina como medidas que são contidas por um cubo são agregadas sobre uma dimensão de tempo.  
  
> [!NOTE]  
>  Com exceção de LastChild que está disponível na edição standard, os comportamentos semiaditivos só estão disponíveis nas edições business intelligence ou enterprise. Além disso, como o comportamento semiaditivo é definido somente em medidas e não em dimensões, você não encontrará esta página no Assistente de Business Intelligence caso ele tenha sido iniciado do Designer de Dimensão ou por meio de um clique com o botão direito do mouse no Gerenciador de Soluções do [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)].  
  
## <a name="options"></a>Opções  
 **Desativar comportamento semiaditivo**  
 Desabilita comportamento semiaditivo em todas as medidas contidas pelo cubo.  
  
 **O assistente detectou a \<nome da dimensão > dimensão de conta, que contém membros semiaditivos. O servidor agregará membros dessa dimensão de acordo com o comportamento semiaditivo especificado para cada tipo de conta.**  
 Habilita comportamento semiaditivo para dimensões de conta que contêm membros semiaditivos. A seleção dessa opção configura a função de agregação de todas as medidas do grupo de medidas que faz referência à dimensão de conta para `ByAccount`.  
  
 Para obter mais informações sobre dimensões de conta, consulte [Criar uma Conta de Finanças de dimensão de tipo pai-filho](multidimensional-models/database-dimensions-finance-account-of-parent-child-type.md).  
  
 **Definir comportamento semiaditivo para membros individuais**  
 Habilita comportamento semiaditivo e especifica a função de agregação semiaditiva para medidas específicas. A função de agregação aplica-se a todas as dimensões que são referenciadas pelo grupo de medidas que contém a medida.  
  
 **Medidas**  
 Exibe o nome de uma medida contida pelo cubo.  
  
 **Função semiaditiva**  
 Selecione a função de agregação da medida selecionada. A tabela a seguir lista as funções de agregação disponíveis.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**AverageOfChildren**|Agregada retornando a média dos filhos da medida.|  
|`ByAccount`|Agregada pela função de agregação associada ao tipo de conta especificado de um atributo em uma dimensão de conta.|  
|`Count`|Agregada com a função `Count`.|  
|`DistinctCount`|Agregada com a função `DistinctCount`.|  
|**FirstChild**|Agregado ao retornar o primeiro membro filho da medida em uma dimensão de tempo.|  
|**FirstNonEmpty**|Agregado ao retornar o primeiro membro não vazio da medida em uma dimensão de tempo.|  
|**LastChild**|Agregado ao retornar o último membro filho da medida em uma dimensão de tempo.|  
|**LastNonEmpty**|Agregado ao retornar o último membro não vazio da medida em uma dimensão de tempo.|  
|`Max`|Agregada com a função `Max`.|  
|`Min`|Agregada com a função `Min`.|  
|**Nenhum**|Nenhuma agregação executada.|  
|`Sum`|Agregada com a função `Sum`.|  
  
> [!NOTE]  
>  Seleções feitas para essa opção serão aplicadas apenas se **Definir comportamento semiaditivo para membros individuais** estiver selecionada.  
  
## <a name="see-also"></a>Consulte também  
 [Ajuda F1 do Assistente de Business Intelligence](business-intelligence-wizard-f1-help.md)   
 [Designer de cubo &#40;Analysis Services - dados multidimensionais&#41;](cube-designer-analysis-services-multidimensional-data.md)   
 [Designer de dimensão &#40;Analysis Services - dados multidimensionais&#41;](dimension-designer-analysis-services-multidimensional-data.md)  
  
  
