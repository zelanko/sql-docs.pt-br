---
title: (Guia partições, Designer de cubo) de grupos de medidas (Analysis Services - dados multidimensionais) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.cubeeditor.partitions.partitionspane.measuregroupdetail.f1
ms.assetid: 58e44b24-cfcd-4908-b445-d4374b961b98
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 7ffd5b3ff4eb98c96e1832e353e64f1953bd62e9
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62727982"
---
# <a name="measure-groups-partitions-tab-cube-designer-analysis-services---multidimensional-data"></a>Grupos de Medidas (guia Partições, Designer de Cubo) (Analysis Services - Dados Multidimensionais)
  Use o painel **Grupos de Medidas** na guia **Partições** do Designer de Cubo para gerenciar as partições associadas a cada grupo de medidas do cubo.  
  
## <a name="options"></a>Opções  
 **Partições**  
 Exibe uma grade que contém a lista de partições que oferecem suporte ao grupo de medidas selecionado. A grade contém as seguintes colunas:  
  
 **(Ordinal)**  
 Exibe a posição ordinal da partição dentro do grupo de medidas.  
  
 Clique para selecionar a linha inteira da partição.  
  
 **Nome da Partição**  
 Digite o nome da partição selecionada.  
  
 **Origem**  
 Digite o nome da tabela (para associação de tabela) ou da consulta (para associação de consulta) que fornece os dados da tabela de fatos para a partição selecionada.  
  
 Clique no botão **...** para exibir a caixa de diálogo **Origem da Partição** e definir a origem para a partição selecionada.  
  
 **Agregação**  
 Exibe o modo de agregação e o modo de armazenamento da partição. O modo de armazenamento é exibido primeiro: ROLAP (processamento analítico online relacional), MOLAP (processamento analítico online multidimensional) ou HOLAP (processamento analítico online híbrido). O modo de agregação é exibido como uma porcentagem da otimização solicitada, como uma medida de espaço solicitado ou usado ou como o número de agregações criadas. Clique no botão **...** para exibir o **Assistente de Design de Agregação** e definir o design de agregação para a partição especificada.  
  
 **Descrição**  
 Digite a descrição opcional da partição.  
  
 **Nova partição...**  
 Clique para exibir o **Assistente para Partições** e criar uma nova partição no grupo de medidas selecionado.  
  
 **Configurações de armazenamento...**  
 Clique para exibir a caixa de diálogo **Configurações de Armazenamento** e especificar o modo de armazenamento, o cache pró-ativo e configurações de notificação para a partição selecionada.  
  
> [!NOTE]  
>  Esta opção será habilitada apenas se uma célula de uma partição estiver selecionada na grade **Partições** do grupo de medidas selecionado.  
  
 **Configurações de write-back...**  
 Clique para exibir a caixa de diálogo **Habilitar/Desabilitar Write-back** e especificar configurações de write-back para o grupo de medidas selecionado.  
  
## <a name="context-menu"></a>Menu de contexto  
 As seguintes opções estão disponíveis no menu de contexto exibido ao clicar com o botão direito do mouse na grade **Partições** de um grupo de medidas selecionado:  
  
|Opção|Definição|  
|------------|----------------|  
|**Adicionar Business Intelligence**|Clique para exibir o **Assistente de Business Intelligence** e adicionar recursos de Business Intelligence ao cubo. Para obter mais informações sobre o **Assistente de Business Intelligence**, consulte [Ajuda F1 do Assistente de Business Intelligence](business-intelligence-wizard-f1-help.md).|  
|**Nova partição**|Clique para exibir o **Assistente para Partições** e criar uma nova partição no grupo de medidas selecionado.|  
|**Renomear partição**|Selecione para renomear a partição selecionada.|  
|**Delete (excluir)**|Clique para exibir a caixa de diálogo **Excluir Objetos** e excluir a ação selecionada.<br /><br /> Observação: Esta opção será desabilitada se uma partição de write-back for selecionada.|  
|**Agregações de design**|Clique para exibir o **Assistente de Design de Agregação** e criar um design de agregação para a partição selecionada.<br /><br /> Observação: Esta opção será desabilitada se uma partição de write-back for selecionada.|  
|**Configurações de armazenamento**|Clique para exibir a caixa de diálogo **Configurações de Armazenamento** e especificar o modo de armazenamento, o cache pró-ativo e configurações de notificação para a partição selecionada.|  
|**Configurações de write-back**|Clique para exibir a caixa de diálogo **Habilitar/Desabilitar Write-back** e especificar configurações de write-back para o grupo de medidas que contém a partição selecionada.|  
|**Otimização baseada no uso**|Clique para exibir o **Assistente de Otimização com Base no Uso** e criar um design de agregação baseado em padrões de uso existentes para a partição selecionada.<br /><br /> Observação: Esta opção será desabilitada se uma partição de write-back for selecionada.|  
|**Processar**|Clique para exibir a caixa de diálogo **Processar** e processar a partição selecionada.|  
|**Copiar**|Esta opção está desabilitada.|  
|**Colar**|Esta opção está desabilitada.|  
|**Propriedades**|Selecione para exibir a janela **Propriedades** do [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] da partição selecionada.|  
  
  
