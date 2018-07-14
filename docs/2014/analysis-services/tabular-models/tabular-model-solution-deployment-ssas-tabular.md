---
title: Implantação de solução de modelo tabular (SSAS Tabular) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: aff96558-e5e5-4b95-8ddf-ee0709c842fb
caps.latest.revision: 21
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 99b9e1594c4d4fbe07a6085544021b94820db640
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37220032"
---
# <a name="tabular-model-solution-deployment-ssas-tabular"></a>Implantação de uma solução de modelo tabular (SSAS tabular)
  Depois de criar um projeto de modelo de tabela, você deve implantá-lo para que os usuários procurem o modelo usando um aplicativo cliente de relatório. Este tópico descreve as várias propriedades e os vários métodos que você pode usar ao implantar soluções de modelo de tabela em seu ambiente.  
  
 Seções neste tópico:  
  
-   [Benefícios](#bkmk_benefits)  
  
-   [Implantando um modelo de tabela do SSDT (Ferramentas de Dados do SQL Server)](#bkmk_deploying_bism)  
  
-   [Propriedades de implantação](#bkmk_deploy_props)  
  
-   [Métodos de implantação](#bkmk_meth)  
  
-   [Configurando o servidor de implantação e conectando a um modelo implantado](#bkmk_connecting)  
  
-   [Tarefas relacionadas](#bkmk_rt)  
  
##  <a name="bkmk_benefits"></a> Benefícios  
 A implantação de um modelo de tabela cria um banco de dados modelo em um ambiente de produção, teste ou preparo. Os usuários podem então se conectar ao modelo implantado por meio de um arquivo de conexão .bism no Sharepoint ou usando uma conexão de dados diretamente de aplicativos cliente de relatório como o Microsoft Excel, o [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)]ou um aplicativo personalizado. O banco de dados de espaço de trabalho modelo, criado quando você cria um novo projeto de modelo de tabela no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]e usado para criar o modelo, permanecerá na instância de servidor de espaço de trabalho, permitindo fazer alterações no projeto do modelo e, em seguida, reimplantá-lo no ambiente de teste, preparo e produção, quando necessário.  
  
##  <a name="bkmk_deploying_bism"></a> Implantando um modelo de tabela do SSDT (Ferramentas de Dados do SQL Server)  
 A implantação é um processo simples; porém, determinadas etapas são necessárias para garantir a implantação de seu modelo na instância correta do Analysis Services e com as opções corretas de configuração.  
  
 São definidos modelos tabulares com várias propriedades específicas de implantação. Quando você implanta, é estabelecida uma conexão com a instância do Analysis Services especificada na propriedade **Servidor** . É criado um novo banco de dados modelo com o nome especificado na propriedade **Banco de Dados** nessa instância, se ainda não existir. Os metadados do arquivo Model.bim do projeto modelo são usados para configurar objetos no banco de dados modelo no servidor de implantação. Com a **Opção de Processamento**, você pode especificar se apenas os metadados modelo são implantados, criando o banco de dados modelo, ou, se **Padrão** ou **Completa** estiver especificado, as credenciais de representação usadas para conectar-se a fontes de dados de memória serão transmitidas na memória do banco de dados de espaço de trabalho modelo para o modelo de banco de dados implantado. O Analysis Services executa o processamento para popular dados no modelo implantado. Quando o processo de implantação for concluído, o modelo poderá ser conectado por aplicativos cliente que usam uma conexão de dados, ou usando um arquivo de conexão .bism no SharePoint.  
  
##  <a name="bkmk_deploy_props"></a> Propriedades de implantação  
 As propriedades Opções de Implantação e Servidor de Implantação do projeto especificam como e onde um modelo é implantado para um ambiente de preparo ou de produção do Analysis Services. Apesar de as configurações de propriedades padrão serem definidas para todos os projetos modelo, de acordo com os seus requisitos de implantação específicos, você pode alterar essas configurações de propriedades para cada projeto. Para obter mais informações sobre como definir as propriedades de implantação padrão, consulte [Configurar propriedades padrão de implantação e modelagem de dados &#40;SSAS Tabular&#41;](properties-ssas-tabular.md).  
  
### <a name="deployment-options-properties"></a>Propriedades de Opções de Implantação  
 As propriedades de Opções de Implantação incluem:  
  
|Propriedade|Configuração padrão|Description|  
|--------------|---------------------|-----------------|  
|**Opção de Processamento**|**Default**|Esta propriedade especifica o tipo de processamento exigido quando as alterações em objetos são implantadas. Essa propriedade oferece as seguintes opções:<br /><br /> **Padrão** – Essa configuração especifica que o Analysis Services determinará o tipo de processamento necessário. Os objetos não processados serão processados e, se preciso for, recalculando relações de atributos, hierarquias de atributo, hierarquias de usuário e colunas calculadas. Estas configurações geralmente resultam em um tempo de implantação mais rápido do que usar a opção de processamento completo.<br /><br /> **Não Processar** – Esta configuração especifica que somente os metadados serão implantados. Depois de implantar, pode ser necessário executar uma operação de processo no modelo implantado para atualizar e recalcular dados.<br /><br /> **Completa** – Esta configuração especifica que ambos os metadados são implantados e uma operação completa de processo é executada. Isto garante que o modelo implantado tem as atualizações mais recentes a metadados e dados.|  
|**Implantação Transacional**|**Falso**|Esta propriedade especifica se a implantação é transacional. Por padrão, a implantação de todos os objetos ou dos objetos alterados não é transacional com o processamento desses objetos implantados. A implantação pode ser bem-sucedida e persistir mesmo em caso de falha do processamento. É possível alterar esse padrão para incorporar a implantação e o processamento em uma única transação.|  
|**Modo de Consulta**|**Na Memória**|Esta propriedade especifica o modo no qual a origem da qual os resultados da consulta são retornados está sendo executada no modo Na Memória (armazenado em cache) ou no modo DirectQuery. Essa propriedade oferece as seguintes opções:<br /><br /> **DirectQuery** – Essa configuração especifica que todas as consultas ao modelo devem usar somente a fonte de dados relacional.<br /><br /> **DirectQuery com na memória** – Essa configuração especifica, por padrão, que as consultas devem ser respondidas usando a origem relacional, a menos que especificado em contrário na cadeia de conexão do cliente.<br /><br /> **Na Memória** – Esta configuração especifica que as consultas devem ser respondidas usando somente o cache.<br /><br /> **Na Memória com DirectQuery** – Esta configuração especifica, por padrão. que as consultas devem ser respondidas usando o cache, a menos que especificado em contrário na cadeia de conexão do cliente.<br /><br /> <br /><br /> Para obter mais informações, consulte [Modo DirectQuery &#40;SSAS Tabular&#41;](directquery-mode-ssas-tabular.md).|  
  
### <a name="deployment-server-properties"></a>Propriedades de Servidor de Implantação  
 As propriedades de Servidor de Implantação incluem:  
  
|Propriedade|Configuração padrão|Description|  
|--------------|---------------------|-----------------|  
|**Servidor**<br /><br /> Defina quando o projeto é criado.|**localhost**|Essa propriedade, definida quando o projeto é criado, especifica a instância do Analysis Services por nome no qual o modelo será implantado. Por padrão, o modelo será implantado na instância padrão do Analysis Services no computador local. Contudo, é possível alterar essa configuração para especificar uma instância nomeada no computador local ou uma instância em qualquer computador remoto no qual você tenha permissão para criar objetos do Analysis Services.|  
|**Edição**|A mesma edição como a instância na qual o Servidor de Espaço de trabalho está localizado.|Essa propriedade especifica a edição do servidor do Analysis Services no qual o modelo será implantado. A edição do servidor define vários recursos que podem ser incorporados no projeto. Por padrão, a edição será do servidor do Analysis Services local. Se você especificar outro servidor do Analysis Services, como, por exemplo, um servidor de produção do Analysis Services, especifique a edição desse servidor do Analysis Services.|  
|**Backup de banco de dados**|**\<projectname>**|Essa propriedade especifica o nome do banco de dados do Analysis Services no qual os objetos modelo serão instanciados na implantação. Esse nome também será especificado em uma conexão de dados de cliente de relatório ou em um arquivo de conexão de dados .bism.<br /><br /> Você poderá alterar este nome a qualquer momento quando estiver criando o modelo. Se você alterar o nome depois de implantar o modelo, as alterações feitas depois da implantação não afetarão o modelo implantado previamente. Por exemplo, se você abrir uma solução nomeada `TestDB` e implantar sua solução com o nome padrão de banco de dados modelo e, em seguida, modificar a solução e renomear o banco de dados de modelo `Sales`, a instância do Analysis Services, as soluções foram implantadas para será exibição separar os bancos de dados, um denominado Model e outro denominado Sales.|  
|**Nome do Cubo**|**Modelo**|Esta propriedade especifica o nome de cubo como mostrado nas ferramentas de cliente (como o Excel) e AMO (Objetos de Gerenciamento de Análise).|  
  
### <a name="directquery-options-properties"></a>Propriedades de opções do DirectQuery  
 As propriedades de Opções de Implantação incluem:  
  
|Propriedade|Configuração padrão|Description|  
|--------------|---------------------|-----------------|  
|**Configurações da representação**|**Padrão**|Esta propriedade especifica as configurações de representação usadas quando um modelo que está sendo executado em modo DirectQuery conecta-se a fontes de dados. Credenciais de representação não são usadas ao consultar o cache Na Memória. Essa configuração de propriedade tem as seguintes opções:<br /><br /> **Padrão** – Esta configuração especifica que o Analysis Services usará a opção especificada na página de Informações de Representação quando a conexão da fonte de dados for criada usando o Assistente de Importação de Tabela.<br /><br /> **ImpersonateCurrentUser** – Esta configuração especifica que a conta de usuário conectado no momento será usada ao se conectar a todas as fontes de dados.|  
  
##  <a name="bkmk_meth"></a> Métodos de implantação  
 Há vários métodos que você pode usar para implantar um projeto de modelo de tabela. A maioria dos métodos de implantação que podem ser usados para outros projetos do Analysis Services, como multidimensional, também podem ser usados para implantar projetos de modelo de tabela.  
  
|Método|Description|Link|  
|------------|-----------------|----------|  
|**Implantar comando em Ferramentas de Dados do SQL Server**|O comando Implantar fornece um método simples e intuitivo para implantar um projeto de modelo de tabela do ambiente de criação do [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] .<br /><br /> **\*\* Cuidado \*\*** Este método não deve ser usado para implantar em servidores de produção. Usar este método pode substituir determinadas propriedades em um modelo existente.|[Implantar do SQL Server Data Tools &#40;Tabular do SSAS&#41;](deploy-from-sql-server-data-tools-ssas-tabular.md)|  
|**Usando Automação AMO (Objetos de Gerenciamento de Análise)**|AMO fornece uma interface programática para o conjunto completo de comandos definidos para o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], incluindo comandos que podem ser usados para implantação de solução. Como uma abordagem para implantação de solução, a automação AMO é a mais flexível, mas também a que exige um esforço de programação.  Uma vantagem importante para usar AMO é que você pode usar o SQL Server Agent com o aplicativo AMO para executar a implantação em uma programação predefinida.|[Desenvolvendo com objetos de gerenciamento de análise &#40;AMO&#41;](../multidimensional-models/analysis-management-objects/developing-with-analysis-management-objects-amo.md)|  
|**XMLA**|Use o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] para gerar um script XMLA dos metadados de um banco de dados existente do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] e, em seguida, executar esse script em outro servidor para recriar o banco de dados inicial. Os scripts XMLA são gerados facilmente no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ao definir o processo de implantação e, em seguida, codificá-lo e salvá-lo como um script XMLA. Quando o script XMLA está em um arquivo salvo, é possível executá-lo de acordo com uma programação ou inseri-lo em um aplicativo que se conecta diretamente em uma instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].<br /><br /> Também é possível executar scripts XMLA em uma base predefinida com o SQL Server Agent, mas não haverá a mesma flexibilidade do AMO. O AMO fornece uma amplitude maior de funcionalidade hospedando o espectro completo de comandos administrativos.|[Implantar soluções de modelo usando XMLA](../multidimensional-models/deploy-model-solutions-using-xmla.md)|  
|**Assistente para Implantação**|Use o Assistente para Implantação para usar os arquivos de saída do XMLA gerados por um projeto do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] para implantar os metadados do projeto em um servidor de destino. Com o Assistente para Implantação, é possível implantar diretamente a partir do arquivo do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , conforme criado pelo diretório de saída do construtor de projetos.<br /><br /> A vantagem principal de usar o Assistente de Implantação do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] é conveniência. Da mesma maneira que você pode salvar um script XMLA para usar posteriormente no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], pode salvar scripts do Assistente de Implantação. O Assistente para Implantação pode ser executado de modo interativo e no prompt de comando utilizando o Utilitário de Implantação.|[Implantar soluções de modelo usando o Assistente de implantação](../multidimensional-models/deploy-model-solutions-using-the-deployment-wizard.md)|  
|**Utilitário de Implantação**|O utilitário de Implantação permite iniciar o mecanismo de implantação do Analysis Services de um prompt de comando.|[Implantar soluções de modelo com o Utilitário de Implantação](../multidimensional-models/deploy-model-solutions-with-the-deployment-utility.md)|  
|**Assistente para Sincronizar Banco de Dados**|Use o Assistente para Sincronizar Bancos de Dados para sincronizar os metadados e os dados entre quaisquer dois bancos de dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .<br /><br /> O Assistente para Sincronizar pode ser usado para copiar os dados e os metadados de um servidor de origem em um servidor de destino. Se o servidor de destino não tiver uma cópia do banco de dados que você deseja implantar, um novo banco de dados é copiado para o servidor de destino. Se o servidor de destino já tiver uma cópia do mesmo banco de dados, o banco de dados no servidor de destino será atualizado para usar os metadados e os dados no banco de dados de origem.|[Sincronizar bancos de dados do Analysis Services](../multidimensional-models/synchronize-analysis-services-databases.md)|  
|**Backup e restauração**|O backup oferece a abordagem mais simples para transferir bancos de dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Na caixa de diálogo **Backup** , é possível definir a configuração das opções e, em seguida, executar o backup na própria caixa de diálogo. Se preferir, crie um script que pode ser salvo e executado com a frequência necessária.<br /><br /> O backup e a restauração não são usados com tanta frequência como os outros métodos, mas podem ajudar a concluir rapidamente uma implantação com requisitos mínimos de infraestrutura.|[Backup e restauração de bancos de dados do Analysis Services](../multidimensional-models/backup-and-restore-of-analysis-services-databases.md)|  
  
##  <a name="bkmk_connecting"></a> Configurando o servidor de implantação e conectando a um modelo implantado  
 Depois que um modelo é implantado, há considerações adicionais para proteger o acesso a dados modelo, backups e operações de processamento que devem ser configurados no servidor do Analysis Services usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Apesar de essas propriedades e parâmetros de configuração estarem fora do escopo deste tópico, eles são, no entanto, muito importantes para garantir que seus dados modelo implantados estejam seguros, atualizados e ofereçam um valioso recurso de análise de dados para usuários em sua organização.  
  
 Depois que um modelo for implantado, e configurações opcionais de servidor forem definidas, o modelo poderá ser conectado por aplicativos cliente de relatório e usado para navegar e analisar os metadados do modelo. A conexão a um banco de dados modelo implantado de aplicativos cliente está fora do escopo deste tópico. Para saber mais sobre como conectar a um banco de dados modelo de aplicativos cliente, consulte [Tabular Model Data Access](tabular-model-data-access.md).  
  
##  <a name="bkmk_rt"></a> Tarefas relacionadas  
  
|Tarefa|Description|  
|----------|-----------------|  
|[Implantar do SQL Server Data Tools &#40;Tabular do SSAS&#41;](deploy-from-sql-server-data-tools-ssas-tabular.md)|Descreve como configurar propriedades de implantação e implantar um projeto de modelo de tabela usando o comando Implantar no [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)].|  
|[Implantar soluções de modelo usando o Assistente de implantação](../multidimensional-models/deploy-model-solutions-using-the-deployment-wizard.md)|Os tópicos nesta seção descrevem como usar o Assistente de Implantação do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] para implantar soluções de modelo de tabela e multidimensionais.|  
|[Implantar soluções de modelo com o Utilitário de Implantação](../multidimensional-models/deploy-model-solutions-with-the-deployment-utility.md)|Descreve como usar o Utilitário de Implantação do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] para implantar soluções de modelo de tabela e multidimensionais.|  
|[Implantar soluções de modelo usando XMLA](../multidimensional-models/deploy-model-solutions-using-xmla.md)|Descreve como usar XMLA para implantar as soluções de tabela e multidimensionais do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .|  
|[Sincronizar bancos de dados do Analysis Services](../multidimensional-models/synchronize-analysis-services-databases.md)|Descreve como usar o Assistente para Sincronizar Bancos de Dados para sincronizar os metadados e os dados entre quaisquer dois bancos de dados de tabela ou multidimensionais do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .|  
  
## <a name="see-also"></a>Consulte também  
 [Conectar um banco de dados do modelo de tabela &#40;SSAS&#41;](connect-to-a-tabular-model-database-ssas.md)  
  
  
