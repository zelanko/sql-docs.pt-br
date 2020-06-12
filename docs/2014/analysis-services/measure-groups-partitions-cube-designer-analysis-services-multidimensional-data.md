---
title: Grupos de medidas (guia partições, designer de cubo) (Analysis Services-dados multidimensionais) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.cubeeditor.partitions.partitionspane.measuregroupdetail.f1
ms.assetid: 58e44b24-cfcd-4908-b445-d4374b961b98
author: minewiskan
ms.author: owend
ms.openlocfilehash: 058248b5b2cb66a73124d8632ad6426ee9f3ad59
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/09/2020
ms.locfileid: "84541579"
---
# <a name="measure-groups-partitions-tab-cube-designer-analysis-services---multidimensional-data"></a>Grupos de Medidas (guia Partições, Designer de Cubo) (Analysis Services - Dados Multidimensionais)
  Use o painel **Grupos de Medidas** na guia **Partições** do Designer de Cubo para gerenciar as partições associadas a cada grupo de medidas do cubo.  
  
## <a name="options"></a>Opções  
 **Partições**  
 Exibe uma grade que contém a lista de partições que oferecem suporte ao grupo de medidas selecionado. A grade contém as seguintes colunas:  
  
 **Numera**  
 Exibe a posição ordinal da partição dentro do grupo de medidas.  
  
 Clique para selecionar a linha inteira da partição.  
  
 **Nome da Partição**  
 Digite o nome da partição selecionada.  
  
 **Fonte**  
 Digite o nome da tabela (para associação de tabela) ou da consulta (para associação de consulta) que fornece os dados da tabela de fatos para a partição selecionada.  
  
 Clique no botão **...** para exibir a caixa de diálogo **Origem da Partição** e definir a origem para a partição selecionada.  
  
 **Aggregation**  
 Exibe o modo de agregação e o modo de armazenamento da partição. O modo de armazenamento é exibido primeiro: ROLAP (processamento analítico online relacional), MOLAP (processamento analítico online multidimensional) ou HOLAP (processamento analítico online híbrido). O modo de agregação é exibido como uma porcentagem da otimização solicitada, como uma medida de espaço solicitado ou usado ou como o número de agregações criadas. Clique no botão **...** para exibir o **Assistente de Design de Agregação** e definir o design de agregação para a partição especificada.  
  
 **Descrição**  
 Digite a descrição opcional da partição.  
  
 **Nova Partição...**  
 Clique para exibir o **Assistente para Partições** e criar uma nova partição no grupo de medidas selecionado.  
  
 **Configurações de armazenamento...**  
 Clique para exibir a caixa de diálogo **Configurações de Armazenamento** e especificar o modo de armazenamento, o cache pró-ativo e configurações de notificação para a partição selecionada.  
  
> [!NOTE]  
>  Esta opção será habilitada apenas se uma célula de uma partição estiver selecionada na grade **Partições** do grupo de medidas selecionado.  
  
 **Configurações de Write-back...**  
 Clique para exibir a caixa de diálogo **Habilitar/Desabilitar Write-back** e especificar configurações de write-back para o grupo de medidas selecionado.  
  
## <a name="context-menu"></a>Menu de contexto  
 As seguintes opções estão disponíveis no menu de contexto exibido ao clicar com o botão direito do mouse na grade **Partições** de um grupo de medidas selecionado:  
  
|Opção|Definição|  
|------------|----------------|  
|**Adicionar Business Intelligence**|Clique para exibir o **Assistente de Business Intelligence** e adicionar recursos de Business Intelligence ao cubo. Para obter mais informações sobre o **Assistente de Business Intelligence**, consulte [Ajuda F1 do Assistente de Business Intelligence](business-intelligence-wizard-f1-help.md).|  
|**Nova partição**|Clique para exibir o **Assistente para Partições** e criar uma nova partição no grupo de medidas selecionado.|  
|**Renomear Partição**|Selecione para renomear a partição selecionada.|  
|**Delete (excluir)**|Clique para exibir a caixa de diálogo **Excluir Objetos** e excluir a ação selecionada.<br /><br /> Observação: esta opção será desabilitada se uma partição de write-back for selecionada.|  
|**Criar Agregações**|Clique para exibir o **Assistente de Design de Agregação** e criar um design de agregação para a partição selecionada.<br /><br /> Observação: esta opção será desabilitada se uma partição de write-back for selecionada.|  
|**Configurações de armazenamento**|Clique para exibir a caixa de diálogo **Configurações de Armazenamento** e especificar o modo de armazenamento, o cache pró-ativo e configurações de notificação para a partição selecionada.|  
|**Configurações de write-back**|Clique para exibir a caixa de diálogo **Habilitar/Desabilitar Write-back** e especificar configurações de write-back para o grupo de medidas que contém a partição selecionada.|  
|**Otimização baseada no uso**|Clique para exibir o **Assistente de Otimização com Base no Uso** e criar um design de agregação baseado em padrões de uso existentes para a partição selecionada.<br /><br /> Observação: esta opção será desabilitada se uma partição de write-back for selecionada.|  
|**Processo**|Clique para exibir a caixa de diálogo **Processar** e processar a partição selecionada.|  
|**Cópia**|Esta opção está desabilitada.|  
|**Colar**|Esta opção está desabilitada.|  
|**Propriedades**|Selecione para exibir a janela **Propriedades** do [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] da partição selecionada.|  
  
  
