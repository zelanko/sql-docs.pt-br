---
title: Configurar propriedades de implantação e modelagem de dados padrão (SSAS tabular) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.bidtoolset.deployment.f1
- VS.TOOLSOPTIONSPAGES.ANALYSIS_SERVICES.DATA_MODELING
- sql12.asvs.bidtoolset.asoptions.f1
- VS.TOOLSOPTIONSPAGES.ANALYSIS_SERVICES.DEPLOYMENT
ms.assetid: 140d0c4e-943c-4387-a8d2-6e066c7e4e75
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: e1246119b72890bc80125034c8ee23bcd0c221b5
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66067588"
---
# <a name="configure-default-data-modeling-and-deployment-properties-ssas-tabular"></a>Configurar propriedades padrão de implantação e modelagem de dados (SSAS tabular)
  Este tópico descreve como definir as configurações de propriedade padrão de nível de compatibilidade, implantação e banco de dados de workspace, que podem ser predefinidas para cada novo projeto de modelo de tabela criado no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]. Depois que um novo projeto é criado, essas propriedades ainda podem ser alteradas dependendo dos requisitos específicos.  
  
#### <a name="to-configure-the-default-compatibility-level-property-setting-for-new-model-projects"></a>Para definir a configuração de propriedade padrão de Nível de Compatibilidade para novos projetos de modelo  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], clique no menu **Ferramentas** e em **Opções**.  
  
2.  Na caixa de diálogo **Opções** , expanda **Designers de Tabela do Analysis Services**e clique em **Nível de Compatibilidade**.  
  
3.  Defina as configurações de propriedades a seguir:  
  
    |Propriedade|Configuração padrão|DESCRIÇÃO|  
    |--------------|---------------------|-----------------|  
    |**Nível de compatibilidade padrão para novos projetos**|SQL Server 2012 (1100)|Essa configuração especifica o nível de compatibilidade padrão a ser usado ao criar um novo projeto de modelo de tabela. Você pode escolher o SQL Server 2012 RTM (1100) se implantar em uma instância do Analysis Services sem o SP1 aplicado, ou o SQL Server 2012 SP1 se a instância de implantação tiver o SP1 aplicado ou SQL Server 2014. Para obter mais informações, consulte [nível de compatibilidade &#40;SSAS tabular&#41;](compatibility-level-for-tabular-models-in-analysis-services.md).|  
    |**Opções de nível de compatibilidade**|Todas selecionadas|Especifica opções de nível de compatibilidade para novos projetos de modelo de tabela e ao implantar em outra instância do Analysis Services.|  
  
#### <a name="to-configure-the-default-deployment-server-property-setting-for-new-model-projects"></a>Para definir a configuração de propriedade padrão do servidor de implantação para novos projetos de modelo  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], clique no menu **Ferramentas** e em **Opções**.  
  
2.  Na caixa de diálogo **Opções** , expanda **Designers de Tabela do Analysis Services**e clique em **Implantação**.  
  
3.  Defina as configurações de propriedades a seguir:  
  
    |Propriedade|Configuração padrão|DESCRIÇÃO|  
    |--------------|---------------------|-----------------|  
    |**Servidor de implantação padrão**|localhost|Esta configuração especifica o servidor padrão a ser usado ao implantar um modelo. Você pode clicar na seta para baixo para navegar para servidores de rede local do Analysis Services ou pode digitar o nome de um servidor remoto.|  
  
    > [!NOTE]  
    >  As alterações à configuração de propriedade Servidor de Implantação Padrão não afetará projetos existentes criados antes da alteração.  
  
###  <a name="bkmk_conf_default"></a>Para definir as configurações de propriedade de banco de dados de espaço de trabalho padrão para novos projetos de modelo  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], clique no menu **Ferramentas** e em **Opções**.  
  
2.  Na caixa de diálogo **Opções**, expanda **Designers de Tabela do Analysis Services** e clique em **Banco de Dados de Workspace**.  
  
3.  Defina as configurações de propriedades a seguir:  
  
    |Propriedade|Configuração padrão|DESCRIÇÃO|  
    |--------------|---------------------|-----------------|  
    |**Servidor de espaço de trabalho padrão**|**localhost**|Essa propriedade especifica o servidor fora-de-processo padrão que será usado para hospedar o banco de dados de workspace enquanto o modelo é criado no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]. Todas as instâncias disponíveis do Analysis Services que executam no computador local são incluídas na caixa de listagem.<br /><br /> Observação: é recomendável especificar sempre um servidor do Analysis Services local como o servidor de workspace. Para bancos de dados de workspace em um servidor remoto, não há suporte para a importação de dados PowerPivot, o backup dos dados não pode ser feito localmente e a interface do usuário pode experimentar latência durante consultas.|  
    |**Retenção de banco de dados de espaço de trabalho após o modelo ser fechado**|**Manter bancos de dados de espaço de trabalho em disco, mas descarregar da memória**|Especifica como um banco de dados de workspace é retido depois que um modelo é fechado. Um banco de dados de workspace inclui metadados modelo, os dados importados em um modelo e credenciais de representação (criptografadas). Em alguns casos, o banco de dados de workspace pode ser muito grande e consumir uma quantidade significativa de memória. Por padrão, os bancos de dados de workspace são removidos da memória. Ao alterar essa configuração, é importante considerar os recursos de memória disponíveis, bem como a frequência na qual você planeja trabalhar no modelo. Essa configuração de propriedade tem as seguintes opções:<br /><br /> **Manter espaços de trabalho na memória** – especifica para manter os espaços de trabalho na memória depois que um modelo é fechado. Essa opção consumirá mais memória. No entanto, ao abrir um modelo no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], menos recursos serão consumidos e o workspace será carregado mais rapidamente.<br /><br /> **Manter bancos de dados de espaço de trabalho em disco, mas descarregar da memória** -especifica para manter o banco de dados de espaço de trabalho em disco, mas não mais na memória depois que um modelo é fechado. Essa opção consumirá menos memória. No entanto, ao abrir um modelo no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], recursos adicionais serão consumidos e o modelo será carregado mais lentamente do que se o banco de dados de workspace estivesse mantido na memória. Use essa opção quando os recursos de memória forem limitados ou ao trabalhar em um banco de dados de workspace remoto.<br /><br /> **Excluir espaço de trabalho** -especifica para excluir o banco de dados de espaço de trabalho da memória e não manter o banco de dados de espaço de trabalho em disco após o modelo Essa opção consumirá menos memória e espaço de armazenamento, No entanto, ao abrir um modelo no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], serão consumidos recursos adicionais e o modelo será carregado mais lentamente do que se o banco de dados de workspace estivesse mantido na memória ou no disco. Use essa opção apenas ao trabalhar ocasionalmente em modelos.|  
    |**Backup de dados**|**Manter backup de dados em disco**|Especifica se o backup dos dados do modelo é mantido em um arquivo de backup. Essa configuração de propriedade tem as seguintes opções:<br /><br /> **Manter backup de dados em disco** -especifica para manter um backup dos dados do modelo em disco. Quando o modelo for salvo, os dados também serão salvos no arquivo de backup (ABF). A seleção dessa opção pode tornar o salvamento e os tempos de carregamento do modelo mais lentos.<br /><br /> **Não manter o backup de dados em disco** -especifica para não manter um backup de data do modelo em disco. Essa opção minimizará o tempo de salvamento e carregamento do modelo.|  
  
> [!NOTE]  
>  As alterações às propriedades de modelo padrão não afetará as propriedades para modelos existentes criados antes da alteração.  
  
## <a name="see-also"></a>Consulte Também  
 [Propriedades do projeto &#40;SSAS tabular&#41;](properties-ssas-tabular.md)   
 [Propriedades de modelo &#40;SSAS de tabela&#41;](model-properties-ssas-tabular.md)   
 [Nível de compatibilidade &#40;SSAS tabular&#41;](compatibility-level-for-tabular-models-in-analysis-services.md)  
  
  
