---
title: Partições remotas – caixa de diálogo de configurações (Analysis Services - dados multidimensionais) avançada | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.asvs.sqlserverstudio.advancedrestoresettings.f1
ms.assetid: a03bb7e1-efaf-47c8-b0ee-f3e4438311cb
caps.latest.revision: 19
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 21550167b2850d8e76daa74c0fdb860ca4e98cc5
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37241656"
---
# <a name="remote-partitions---advanced-settings-dialog-box-analysis-services---multidimensional-data"></a>Partições Remotas - (caixa de diálogo Configurações Avançadas) (Analysis Services - Dados Multidimensionais)
  Use a caixa de diálogo **Partições Remotas - Configurações Avançadas** no [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] para editar configurações avançadas, como a cadeia de conexão da fonte de dados que representa o banco de dados remoto do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] que mantém partições remotas, ao restaurar partições remotas de um arquivo de backup remoto em um banco de dados do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] utilizando a caixa de diálogo **Restaurar Banco de Dados**. É possível exibir a caixa de diálogo **Partições Remotas – Configurações Avançadas** na página **Partições** da caixa de diálogo **Restaurar Banco de Dados** clicando no botão de reticências (**...**) de uma partição remota após selecionar a opção **Restaurar partições remotas** .  
  
## <a name="options"></a>Opções  
  
|Termo|Definição|  
|----------|----------------|  
|**Nome da fonte de dados**|Exibe o nome da fonte de dados que representa o banco de dados remoto do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] que gerencia as partições remotas listadas.|  
|**Arquivo de backup**|Exibe o nome do arquivo de backup remoto que contém os dados a serem restaurados das partições remotas listadas.<br /><br /> Observação: Nenhum arquivo de backup é exibido se um arquivo de backup remoto foi especificado na **arquivo de Backup** coluna sobre o **partições** página da **restaurar banco de dados** caixa de diálogo.|  
|**Cadeia de conexão**|Exibe a cadeia de conexão da fonte de dados exibida em **Nome da fonte de dados**.|  
|**Editar**|Clique para exibir a caixa de diálogo **Propriedades de Vínculo de Dados** e editar as propriedades contidas na cadeia de conexão.|  
|**Lista de partições**|Selecione para especificar locais diferentes nos quais restaurar partições remotas. Observe que você só poderá alterar a pasta de restauração de uma partição remota se foi especificado um local diferente do local padrão para essa partição remota no cubo. A grade a seguir, habilitada quando esta opção está selecionada, é usada para especificar uma pasta de restauração para cada partição remota:<br /><br /> **Cubo**: exibe o nome do cubo que contém a partição remota.<br /><br /> **MeasureGroup**: exibe o nome do grupo de medidas que contém a partição remota.<br /><br /> **Partição**: exibe o nome da partição remota.<br /><br /> **Tamanho (MB)**: exibe o tamanho, em megabytes, da partição remota.<br /><br /> **Pasta original**: exibe o nome da pasta original na qual a partição remota foi armazenada.<br /><br /> **Pasta de restauração**: digite o nome da pasta de restauração da partição remota ou clique no botão de reticências (**... **) para exibir o **Procurar pasta remota** caixa de diálogo e selecionar o caminho da pasta a ser usada. Para obter mais informações sobre a caixa de diálogo **Procurar Pasta Remota**, consulte [Caixa de diálogo Procurar Pasta Remota &#40;Analysis Services – Dados Multidimensionais&#41;](browse-for-remote-folder-dialog-box-analysis-services-multidimensional-data.md).|  
  
## <a name="see-also"></a>Consulte também  
 [Designers e caixas de diálogo do Analysis Services &#40;dados multidimensionais&#41;](analysis-services-designers-and-dialog-boxes-multidimensional-data.md)   
 [Partições &#40;restaurar a caixa de diálogo banco de dados&#41; &#40;Analysis Services - dados multidimensionais&#41;](partitions-restore-database-dialog-box-analysis-services-multidimensional-data.md)   
 [Backup e restauração de bancos de dados do Analysis Services](multidimensional-models/backup-and-restore-of-analysis-services-databases.md)  
  
  
