---
title: Banco de dados de espaço de trabalho (SSAS tabular) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 662daf08-a514-44a7-8675-44644aa454a2
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 8708bd3f4375179638ce5e86a0619a1e1ccf4d77
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66066256"
---
# <a name="workspace-database-ssas-tabular"></a>Banco de dados do workspace (SSAS tabular)
  O banco de dados de workspace modelo de tabela, usado durante a criação de modelos, é criado quando você cria um novo projeto de modelo de tabela no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]. O banco de dados de workspace reside na memória em uma instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] que é executada em modo Tabela; em geral no mesmo computador que o [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)].  
  
 Este tópico inclui as seções a seguir:  
  
-   [Visão geral do Banco de Dados de Workspace](#bkmk_overview)  
  
-   [Propriedades de Banco de Dados de Workspace](#bkmk_ws_prop)  
  
-   [Usando SSMS para gerenciar o banco de dados de workspace](#bkmk_use_ssms)  
  
-   [Tarefas relacionadas](#bkmk_related_tasks)  
  
##  <a name="workspace-database-overview"></a><a name="bkmk_overview"></a>Visão geral do banco de dados Workspace  
 Um banco de dados de workspace é criado na instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], especificada na propriedade de Servidor de Workspace, quando você cria um novo projeto de Business Intelligence usando um dos modelos de projeto de modelo de tabela no [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]. Cada projeto de modelo tabular terá seu próprio banco de dados de workspace. Você pode usar o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] para exibir o banco de dados de workspace no servidor do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. O nome de banco de dados de workspace inclui o nome de projeto, seguido por um sublinhado, seguido pelo nome de usuário, seguido por um sublinhado, seguido por um GUID.  
  
 O banco de dados de workspace reside na memória enquanto o projeto de modelo tabular está aberto no [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]. Quando você fecha o projeto, o banco de dados de workspace é mantido na memória, armazenado em disco e removido da memória (padrão), ou removido da memória e não armazenado em disco, como determinado pela propriedade de Retenção de Workspace. Para obter mais informações sobre a propriedade de Retenção de Workspace, consulte [Propriedades de Banco de Dados de Workspace](#bkmk_ws_prop) posteriormente neste tópico.  
  
 Depois que você adicionou dados a seu projeto de modelo usando o Assistente de Importação de Tabela ou usando copiar/colar, ao exibir as tabelas, colunas e dados no designer de modelo, você estará exibindo o banco de dados de workspace. Se você adicionar mais tabelas, colunas, relacionamentos, etc., estará alterando o banco de dados do workspace.  
  
> [!IMPORTANT]  
>  Se alguma das tabelas em seu modelo contiver um número grande de linhas, importe somente um subconjunto dos dados durante a criação do modelo. Ao importar um subconjunto dos dados, você poderá reduzir o tempo de processamento e o consumo de recursos do servidor de banco de dados do workspace.  
  
> [!NOTE]  
>  A janela de visualização na página Selecionar tabelas e exibições no Assistente de Importação de Tabela, caixa de diálogo Editar Propriedades da Tabela e caixa de diálogo Gerenciador de Partições mostra tabelas, colunas e linhas à fonte de dados e pode não mostrar as mesmas tabelas, colunas e linhas que o banco de dados de workspace.  
  
 Quando você implantar um projeto de modelo tabular, o banco de dados modelo implantado, que é essencialmente uma cópia do banco de dados de workspace, é criado na instância de servidor do Analysis Services especificada na propriedade de Servidor de Implantação. Para obter mais informações sobre a propriedade Servidor de Implantação, consulte [Propriedades de projeto &#40;SSAS de Tabela&#41;](properties-ssas-tabular.md).  
  
 O banco de dados de workspace modelo geralmente reside no host local ou uma instância nomeada local de um servidor do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Você pode usar uma instância remota do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] para hospedar o banco de dados de workspace, no entanto, esta configuração não é recomendada devido à latência durante consulta de dados e outras restrições. Idealmente, a instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] que hospedará os bancos de dados de workspace está no mesmo computador que o [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]. Criar projetos de modelo no mesmo computador que a instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] que hospeda o banco de dados de workspace pode melhorar o desempenho.  
  
 Bancos de dados de workspace remotos têm as seguintes restrições:  
  
-   Latência potencial durante consultas.  
  
-   A propriedade Backup de Dados não pode ser definida como **Backup em disco**.  
  
-   Você não pode importar dados de uma pasta de trabalho PowerPivot ao criar um novo projeto de modelo de tabela usando a Importação de modelo de projeto do PowerPivot.  
  
##  <a name="workspace-database-properties"></a><a name="bkmk_ws_prop"></a>Propriedades do banco de dados espaço de trabalho  
 As propriedades de banco de dados de workspace são incluídas nas propriedades modelo. Para exibir propriedades de modelo, no [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)], no **Gerenciador de Soluções**, clique no arquivo **Model.bim** . As propriedades do modelo podem ser configuradas usando a janela **Propriedades** . As propriedades específicas do banco de dados de workspace incluem:  
  
> [!NOTE]  
>  As propriedades **Servidor de Workspace**, **Retenção de Workspace** e **Backup de Dados** têm configurações padrão aplicadas quando você cria um novo projeto de modelo. Você pode alterar as configurações padrão para novos projetos de modelos na página **Modelagem de Dados** nas configurações do **Analysis Server** na caixa de diálogo Ferramentas\Opções. Estas propriedades, assim como outras, também podem ser definidas para cada projeto de modelo na janela **Propriedades** . Alterar as configurações padrão não se aplicará a projetos de modelo já criados. Para obter mais informações, consulte [Configurar propriedades padrão de implantação e modelagem de dados &#40;SSAS de Tabela&#41;](configure-default-data-modeling-and-deployment-properties-ssas-tabular.md).  
  
|Propriedade|Configuração padrão|Descrição|  
|--------------|---------------------|-----------------|  
|**Banco de dados do workspace**|O nome de projeto, seguido por um sublinhado, seguido pelo nome de usuário, seguido por um sublinhado, seguido por um GUID.|O nome do banco de dados de workspace usado por armazenar e editar o projeto de modelo de memória temporário. Depois que um projeto de modelo tabular é criado, este banco de dados aparecerá na instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] especificada na propriedade de **Servidor de Workspace**. Essa propriedade não pode ser configurada na janela Propriedades.|  
|**Retenção de Workspace**|Descarregar na memória|Especifica como um banco de dados de workspace é retido depois que um projeto de modelo é fechado. Um banco de dados de workspace inclui metadados modelo e dados importados. Em alguns casos, o banco de dados de workspace pode ser muito grande e consumir uma grande quantidade de memória. Por padrão, quando você fecha um projeto de modelo no [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)], o banco de dados de workspace é descarregado da memória. Ao alterar essa configuração, é importante considerar os recursos de memória disponíveis, bem como a frequência na qual você planeja trabalhar no projeto de modelo. Essa configuração de propriedade tem as seguintes opções:<br /><br /> **Manter na memória** – Especifica manter o banco de dados de workspace na memória depois que um projeto de modelo é fechado. Essa opção consumirá mais memória. No entanto, ao abrir um projeto de modelo no [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)], menos recursos serão consumidos e o banco de dados do workspace será carregado mais rapidamente.<br /><br /> **Descarregar da memória** – Especifica manter banco de dados de workspace em disco, e não mais na memória depois que um projeto de modelo é fechado. Essa opção consumirá menos memória. No entanto, ao abrir um projeto de modelo no [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)], o banco de dados de workspace deve ser reanexado; recursos adicionais serão consumidos e o projeto de modelo será carregado mais lentamente do que se o banco de dados de workspace fosse mantido na memória. Use essa opção quando os recursos de memória forem limitados ou ao trabalhar em um banco de dados de workspace remoto.<br /><br /> **Excluir workspace** – Especifica excluir o banco de dados de workspace da memória e não manter banco de dados de workspace em disco depois que o projeto de modelo é fechado. Essa opção consumirá menos memória e espaço de armazenamento. No entanto, ao abrir um projeto de modelo no [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)], serão consumidos recursos adicionais e o projeto de modelo será carregado mais lentamente do que se o banco de dados de workspace fosse mantido na memória ou no disco. Use essa opção apenas ao trabalhar ocasionalmente em projetos modelo.<br /><br /> <br /><br /> A configuração padrão para essa propriedade pode ser alterada na página **Modelagem de Dados** nas configurações do **Analysis Server** na caixa de diálogo Ferramentas\Opções.|  
|**Servidor de espaço de trabalho**|localhost|Essa propriedade especifica o servidor fora-de-processo padrão que será usado para hospedar o banco de dados de workspace enquanto o projeto de modelo é criado no [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]. Todas as instâncias disponíveis do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] que executam no computador local são incluídas na caixa de listagem.<br /><br /> Para especificar um servidor do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] diferente (executando em modo Tabular), digite o nome do servidor. O usuário conectado deve ser Administrador no servidor do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .<br /><br /> Observe que é recomendável especificar um servidor local [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] como o servidor de espaço de trabalho. Para bancos de dados de workspace em um servidor remoto, não há suporte para a importação do PowerPivot, o backup dos dados não pode ser feito localmente e a interface do usuário pode experimentar latência durante consultas.<br /><br /> Observe também que a configuração padrão para essa propriedade pode ser alterada na página modelagem de dados em [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] configurações na caixa de diálogo ferramentas \ Opções.|  
  
##  <a name="using-ssms-to-manage-the-workspace-database"></a><a name="bkmk_use_ssms"></a>Usando o SSMS para gerenciar o banco de dados de espaço de trabalho  
 Você pode usar o SSMS ([!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]) para se conectar ao servidor do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] que hospeda o banco de dados de workspace. Normalmente, não há gerenciamento do banco de dados de workspace necessário; a exceção é desanexar ou excluir um banco de dados de workspace, o que deve ser feito no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
> [!WARNING]  
>  Não use o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] para gerenciar o banco de dados de workspace enquanto o projeto estiver aberto no designer de modelo. Fazer isso poderia causar a perda de dados.  
  
##  <a name="related-tasks"></a><a name="bkmk_related_tasks"></a> Tarefas relacionadas  
  
|Tópico|Descrição|  
|-----------|-----------------|  
|[Propriedades de modelo &#40;SSAS de Tabela&#41;](model-properties-ssas-tabular.md)|Fornece descrições e etapas de configuração para as propriedades do banco de dados de espaço de trabalho de um modelo.|  
  
## <a name="see-also"></a>Consulte Também  
 [Configurar propriedades de implantação e modelagem de dados padrão &#40;SSAS tabular&#41;](configure-default-data-modeling-and-deployment-properties-ssas-tabular.md)   
 [Propriedades de projeto &#40;SSAS de Tabela&#41;](properties-ssas-tabular.md)  
  
  
