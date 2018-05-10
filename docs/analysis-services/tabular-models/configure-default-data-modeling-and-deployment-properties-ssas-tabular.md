---
title: Configurar propriedades de implantação e modelagem de dados padrão | Microsoft Docs
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: tabular-models
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: d6ac366301da0758e731f602d46b82f3ec3bf153
ms.sourcegitcommit: 1aedef909f91dc88dc741748f36eabce3a04b2b1
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/08/2018
---
# <a name="configure-default-data-modeling-and-deployment-properties"></a>Configurar propriedades de implantação e modelagem de dados padrão 
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  Este artigo descreve como configurar o nível de compatibilidade padrão, implantação e configurações de propriedade do espaço de trabalho banco de dados, podem ser pré-definidas para cada modelo de tabela novo projeto que você criam no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]. Depois que um novo projeto é criado, essas propriedades ainda podem ser alteradas dependendo dos requisitos específicos.  
  
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
 [Propriedades do projeto](../../analysis-services/tabular-models/project-properties-ssas-tabular.md)   
 [Propriedades do modelo](../../analysis-services/tabular-models/model-properties-ssas-tabular.md)   
 [Nível de compatibilidade](../../analysis-services/tabular-models/compatibility-level-for-tabular-models-in-analysis-services.md)  
  
  
