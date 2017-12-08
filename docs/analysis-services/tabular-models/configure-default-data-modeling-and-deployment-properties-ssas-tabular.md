---
title: "Configurar a modelagem de dados padrão e propriedades de implantação (SSAS Tabular) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: tabular-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- VS.TOOLSOPTIONSPAGES.ANALYSIS_SERVICES.DATA_MODELING
- sql13.asvs.bidtoolset.deployment.f1
- sql13.asvs.bidtoolset.asoptions.f1
- VS.TOOLSOPTIONSPAGES.ANALYSIS_SERVICES.DEPLOYMENT
ms.assetid: 140d0c4e-943c-4387-a8d2-6e066c7e4e75
caps.latest.revision: "17"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 704a719e3f2d509b5a949f7e44dd86cdcea7b183
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="configure-default-data-modeling-and-deployment-properties-ssas-tabular"></a>Configurar propriedades padrão de implantação e modelagem de dados (SSAS tabular)
  Este tópico descreve como definir as configurações de propriedade padrão de nível de compatibilidade, implantação e banco de dados de espaço de trabalho, que podem ser predefinidas para cada novo projeto de modelo de tabela criado no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]. Depois que um novo projeto é criado, essas propriedades ainda podem ser alteradas dependendo dos requisitos específicos.  
  
#### <a name="to-configure-the-default-compatibility-level-property-setting-for-new-model-projects"></a>Para definir a configuração de propriedade padrão de Nível de Compatibilidade para novos projetos de modelo  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], clique no menu **Ferramentas** e em **Opções**.  
  
2.  Na caixa de diálogo **Opções** , expanda **Designers de Tabela do Analysis Services**e clique em **Nível de Compatibilidade**.  
  
3.  Defina as configurações de propriedades a seguir:  
  
    |Propriedade|Configuração padrão|Description|  
    |--------------|---------------------|-----------------|  
    |**Nível de compatibilidade padrão para novos projetos**|SQL Server 2016 (1200)|Essa configuração especifica o nível de compatibilidade padrão a ser usado ao criar um novo projeto de modelo de tabela. Você pode escolher o SQL Server 2012 (1100) se for implantar em uma instância do Analysis Services sem o SP1 aplicado, ou o SQL Server 2012 SP1 ou posterior se a instância de implantação tiver o SP1 aplicado. Para obter mais informações, consulte [Nível de compatibilidade para modelos de tabela no Analysis Services](../../analysis-services/tabular-models/compatibility-level-for-tabular-models-in-analysis-services.md).|  
    |**Opções de nível de compatibilidade**|Todas selecionadas|Especifica opções de nível de compatibilidade para novos projetos de modelo de tabela e ao implantar em outra instância do Analysis Services.|  
  
#### <a name="to-configure-the-default-deployment-server-property-setting-for-new-model-projects"></a>Para definir a configuração de propriedade padrão do servidor de implantação para novos projetos de modelo  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], clique no menu **Ferramentas** e em **Opções**.  
  
2.  Na caixa de diálogo **Opções** , expanda **Designers de Tabela do Analysis Services**e clique em **Implantação**.  
  
3.  Defina as configurações de propriedades a seguir:  
  
    |Propriedade|Configuração padrão|Description|  
    |--------------|---------------------|-----------------|  
    |**Servidor de implantação padrão**|localhost|Esta configuração especifica o servidor padrão a ser usado ao implantar um modelo. Você pode clicar na seta para baixo para navegar para servidores de rede local do Analysis Services ou pode digitar o nome de um servidor remoto.|  
  
    > [!NOTE]  
    >  As alterações à configuração de propriedade Servidor de Implantação Padrão não afetará projetos existentes criados antes da alteração.  
  
###  <a name="bkmk_conf_default"></a> Para definir as configurações de propriedade padrão do Banco de Dados de Espaço de Trabalho para novos projetos de modelo  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], clique no menu **Ferramentas** e em **Opções**.  
  
2.  Na caixa de diálogo **Opções** , expanda **Designers de Tabela do Analysis Services**e clique em **Banco de Dados de Espaço de Trabalho**.  
  
3.  Defina as configurações de propriedades a seguir:  
  
    |Propriedade|Configuração padrão|Description|  
    |--------------|---------------------|-----------------|  
    |**Servidor de espaço de trabalho padrão**|**localhost**|Essa propriedade especifica o servidor fora-de-processo padrão que será usado para hospedar o banco de dados de espaço de trabalho enquanto o modelo é criado no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]. Todas as instâncias disponíveis do Analysis Services que executam no computador local são incluídas na caixa de listagem.<br /><br /> <br /><br /> Observação: é recomendável especificar sempre um servidor do Analysis Services local como o servidor de espaço de trabalho. Para bancos de dados de espaço de trabalho em um servidor remoto, não há suporte para a importação de dados do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] , o backup dos dados não pode ser feito localmente e a interface do usuário pode experimentar latência durante consultas.|  
    |**Retenção de banco de dados de espaço de trabalho após o fechamento do modelo**|**Mantenha bancos de dados de espaço de trabalho em disco, mas descarregue da memória**|Especifica como um banco de dados de espaço de trabalho é retido depois que um modelo é fechado. Um banco de dados de espaço de trabalho inclui metadados modelo, os dados importados em um modelo e credenciais de representação (criptografadas). Em alguns casos, o banco de dados de espaço de trabalho pode ser muito grande e consumir uma quantidade significativa de memória. Por padrão, os bancos de dados de espaço de trabalho são removidos da memória. Ao alterar essa configuração, é importante considerar os recursos de memória disponíveis, bem como a frequência na qual você planeja trabalhar no modelo. Essa configuração de propriedade tem as seguintes opções:<br /><br /> **Manter espaços de trabalho na memória** – Especifica que os espaços de trabalho são mantidos na memória depois que um modelo é fechado. Essa opção consumirá mais memória. No entanto, ao abrir um modelo no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], menos recursos serão consumidos e o espaço de trabalho será carregado mais rapidamente.<br /><br /> **Manter bancos de dados de espaço de trabalho em disco, mas descarregar da memória** – Especifica que os bancos de dados de espaço de trabalho são mantidos em disco, e não mais na memória depois que um modelo é fechado. Essa opção consumirá menos memória. No entanto, ao abrir um modelo no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], recursos adicionais serão consumidos e o modelo será carregado mais lentamente do que se o banco de dados de espaço de trabalho estivesse mantido na memória. Use essa opção quando os recursos de memória forem limitados ou ao trabalhar em um banco de dados de espaço de trabalho remoto.<br /><br /> **Excluir espaço de trabalho** – Especifica que o banco de dados de espaço de trabalho é excluído da memória e que o banco de dados de espaço de trabalho não é mantido em disco depois que o modelo é fechado. Essa opção consumirá menos memória e espaço de armazenamento; no entanto, ao abrir um modelo no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], serão consumidos recursos adicionais e o modelo será carregado mais lentamente do que ocorreria se o banco de dados de espaço de trabalho fosse mantido na memória ou em disco. Use essa opção apenas ao trabalhar ocasionalmente em modelos.|  
    |**Backup de dados**|**Mantenha backup de dados em disco**|Especifica se o backup dos dados do modelo é mantido em um arquivo de backup. Essa configuração de propriedade tem as seguintes opções:<br /><br /> **Manter o backup dos dados em disco** – Especifica que um backup de dados do modelo é mantido em disco. Quando o modelo for salvo, os dados também serão salvos no arquivo de backup (ABF). A seleção dessa opção pode tornar o salvamento e os tempos de carregamento do modelo mais lentos.<br /><br /> **Não manter backup de dados em disco** – Especifica que um backup de dados do modelo não é mantido em disco. Essa opção minimizará o tempo de salvamento e carregamento do modelo.|  
  
> [!NOTE]  
>  As alterações às propriedades de modelo padrão não afetará as propriedades para modelos existentes criados antes da alteração.  
  
## <a name="see-also"></a>Consulte também  
 [Propriedades de projeto &#40;SSAS de Tabela&#41;](../../analysis-services/tabular-models/project-properties-ssas-tabular.md)   
 [Propriedades do modelo &#40; SSAS de tabela &#41;](../../analysis-services/tabular-models/model-properties-ssas-tabular.md)   
 [Nível de compatibilidade para modelos de tabela no Analysis Services](../../analysis-services/tabular-models/compatibility-level-for-tabular-models-in-analysis-services.md)  
  
  
