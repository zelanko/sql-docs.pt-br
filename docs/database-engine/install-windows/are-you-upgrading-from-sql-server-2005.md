---
title: "Voc&#234; est&#225; atualizando do SQL Server 2005? | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "setup-install"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: ad40e66f-71fe-4ee6-9ce3-17127e7b1d7a
caps.latest.revision: 21
author: "MikeRayMSFT"
ms.author: "mikeray"
manager: "jhubbard"
caps.handback.revision: 21
---
# Voc&#234; est&#225; atualizando do SQL Server 2005?
  O fim do suporte estendido para o SQL Server 2005 é um motivo para atualizar agora para uma versão mais recente do SQL Server e do Banco de Dados SQL do Microsoft Azure. A atualização permite manter a segurança e a conformidade, alcançar um desempenho inovador e otimizar a infraestrutura da plataforma de dados.  
  
 Para obter mais informações, diretrizes e ferramentas para planejar e automatizar sua migração ou atualização, consulte [Fim do suporte do SQL Server 2005](http://www.microsoft.com/en-us/server-cloud/products/sql-server-2005/).  
  
## Por que atualizar?  
  
> [!IMPORTANT]  
>  O suporte estendido para o SQL Server 2005 termina em 12 de abril de 2016. Se ainda estiver executando o SQL Server 2005 depois de 12 de abril de 2016, você deixará de receber atualizações de segurança.  
  
 Para obter uma folha de dados em formato PDF que explica os benefícios de atualizar do SQL Server 2005, [clique aqui](https://info.microsoft.com/rs/157-GQE-382/images/EN-CNTNT-Infographic-UpgradeSQL2005Datasheet.pdf) (não na imagem em miniatura abaixo).  
  
 ![Data sheet about upgrading from SQL Server 2005](../../database-engine/install-windows/media/sqlserver2005eos.png "Data sheet about upgrading from SQL Server 2005")  
  
## Escolher sua opção de atualização  
 Se você estiver atualizando bancos de dados relacionais do SQL Server 2005, aqui estão as opções para armazenamento relacional na plataforma Microsoft.  
  
 Para ver uma análise mais abrangente dessas opções, [clique aqui](http://sql05upgrade.azurewebsites.net/).  
  
|Opção de armazenamento relacional|Benefícios|Outros fatores a considerar|  
|-------------------------------|--------------|-------------------------------|  
|**SQL Server no local**<br /><br /> Considere esta opção para aplicativos de banco de dados de qualquer tipo, desde sistemas transacionais até data warehouses.|Você tem o máximo de controle sobre recursos e escalabilidade porque você gerencia tanto o hardware quanto o software.<br /><br /> Se você estiver atualizando do SQL Server 2005, esse é o ambiente mais semelhante.|Você precisa fazer o maior investimento inicial e fornecer o gerenciamento mais contínuo, pois você precisa comprar, manter e gerenciar seu próprio hardware e software.<br /><br /> Para saber mais, confira [SQL Server 2016](https://www.microsoft.com/EN-US/server-cloud/products/sql-server-2016/).|  
|**SQL Server hospedado em máquinas virtuais do Azure**<br /><br /> Considere essa opção se você quiser o seguinte:<br /><br /> Benefícios da migração para um ambiente hospedado.<br /><br /> Controle sobre o ambiente operacional.<br /><br /> Conjunto de recursos familiares do SQL Server.|Você pode implantar rapidamente de uma biblioteca de imagens de máquinas virtuais.<br /><br /> Obtenha o conjunto completo de recursos do SQL Server.<br /><br /> Você economiza o custo de hardware e do software para servidores. Você paga apenas pelo uso por hora.|Você precisa configurar e gerenciar ambos o SQL Server e o software do sistema operacional.<br /><br /> <br /><br /> Para saber mais, confira [Visão geral do SQL Server em máquinas virtuais do Azure](https://azure.microsoft.com/documentation/articles/virtual-machines-sql-server-infrastructure-services/).<br /><br /> Para obter informações sobre a migração, consulte [Migrar um banco de dados para o SQL Server em uma VM do Azure](https://azure.microsoft.com/documentation/articles/virtual-machines-migrate-onpremises-database/).|  
|**Serviço de banco de dados hospedado do banco de dados SQL do Azure**<br /><br /> Considere esta opção se você quiser uma solução de baixo custo com menos manutenção.<br /><br /> Essa opção é especialmente apropriada para aplicativos que não exigem a mesma capacidade durante todo o tempo ou que devem fornecer acesso externo.|Você pode implantar rapidamente e escalar verticalmente com facilidade.<br /><br /> Você paga apenas pelo uso por hora.<br /><br /> O custo do serviço inclui não apenas armazenamento, mas alta disponibilidade e backups automáticos.|O banco de dados SQL do Azure não tem alguns recursos do SQL Server que não são aplicáveis em um ambiente de nuvem hospedado. Para obter mais informações, veja [Informações do Transact-SQL do Banco de Dados SQL do Azure](https://azure.microsoft.com/documentation/articles/sql-database-transact-sql-information/).<br /><br /> O banco de dados SQL do Azure também tem um tamanho máximo de 500 GB, em comparação com 524 PB para o SQL Server.<br /><br /> Para saber mais, confira [Banco de Dados SQL](https://azure.microsoft.com/services/sql-database/).<br /><br /> Para saber mais sobre a migração, confira [Migração de um banco de dados do SQL Server para um banco de dados SQL do Azure](https://azure.microsoft.com/documentation/articles/sql-database-cloud-migrate/).|  
  
 Você também pode desejar considerar uma solução não relacional ou NoSQL para determinados aplicativos e dados.  
  
|Solução não relacional|Benefícios|  
|------------------------------|--------------|  
|**Banco de Dados de Documentos do Azure**<br /><br /> Considere esta opção para aplicativos Web modernos, escalonáveis e móveis que usam dados JSON e exigem uma combinação de consultas robustas e processamento de dados transacional.<br /><br /> Para obter mais informações, consulte [Banco de Dados de Documentos](https://azure.microsoft.com/en-us/services/documentdb/).<br /><br /> Para saber mais sobre como importar dados, confira [Importar dados para o Banco de Dados de Documentos](https://azure.microsoft.com/documentation/articles/documentdb-import-data/).|Os documentos são indexados e você pode usar uma sintaxe SQL familiar para consultá-los.<br /><br /> O banco de dados é livre de esquemas.<br /><br /> Você pode adicionar propriedades aos documentos sem precisar recompilar índices.<br /><br /> Você obtém suporte ao JSON e ao JavaScript dentro do mecanismo de banco de dados.<br /><br /> Você obtém suporte nativo para dados geoespaciais e integração com outros serviços do Azure, incluindo Pesquisa do Azure, HDInsight e Data Factory.<br /><br /> Obtenha armazenamento de baixa latência e alto desempenho com níveis de produtividade reservados.|  
|**Armazenamento de tabela do Azure**<br /><br /> Considere esta opção para armazenar petabytes de dados semiestruturados em uma solução econômica.<br /><br /> Para obter mais informações, consulte o [Armazenamento de Tabela](https://azure.microsoft.com/services/storage/tables/).|Você pode evoluir seus aplicativos e seu esquema de tabela sem colocar os dados offline.<br /><br /> Você pode escalar verticalmente sem fragmentar seu conjunto de dados.<br /><br /> Você obtém armazenamento com redundância geográfica que replica os dados por várias regiões.|  
  
 Para baixar o relatório “Migrating from SQL Server 2005” (Migrando do SQL Server 2005) pelas Diretrizes na Microsoft, que contém mais detalhes sobre as opções de atualização, [clique aqui](https://info.microsoft.com/CO-SQL-CNTNT-FY16-09Sep-14-ModernizationDirOnMFST-Register.html) (não na imagem em miniatura abaixo).  
  
 ![Report about migrating from SQL Server 2005](../../database-engine/install-windows/media/sqlserver2005migratingdoc.png "Report about migrating from SQL Server 2005")  
  
## Planejar sua atualização  
  
-   Leia sobre como planejar sua atualização na seguinte série de postagens no blog da equipe do SQL Server:  
  
    -   [Planejamento de uma atualização eficiente do SQL Server 2005: etapa 1 de 3](http://blogs.technet.com/b/dataplatforminsider/archive/2015/12/10/planning-an-efficient-upgrade-from-sql-server-2005-step-1-of-3.aspx)  
  
    -   [Planejamento de uma atualização eficiente do SQL Server 2005: etapa 2 de 3](http://blogs.technet.com/b/dataplatforminsider/archive/2015/12/15/planning-an-efficient-upgrade-from-sql-server-2005-step-2-of-3.aspx)  
  
    -   [Planejamento de uma atualização eficiente do SQL Server 2005: etapa 3 de 3](http://blogs.technet.com/b/dataplatforminsider/archive/2015/12/17/planning-an-efficient-upgrade-from-sql-server-2005-step-3-of-3.aspx)  
  
-   Examine os requisitos e as considerações em [Planning a SQL Server Installation](../../sql-server/install/planning-a-sql-server-installation.md), incluindo o [Hardware and Software Requirements for Installing SQL Server 2016](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server-2016.md).  
  
-   Leia sobre como atualizar.  
  
    -   Analise os métodos de atualização disponíveis e saiba como planejar e testar no tópico [Upgrade Database Engine](../../database-engine/install-windows/upgrade-database-engine.md).  
  
        > [!IMPORTANT]  
        >  Você não pode atualizar um servidor do SQL Server 2005 para um servidor do SQL Server 2016 in-loco. É necessário instalar o SQL Server 2016 e, em seguida, migrar os bancos de dados do SQL Server 2005 para a nova instalação. Para saber mais, confira a seção "Nova Atualização da Instalação" no tópico [Choose a Database Engine Upgrade Method](../../database-engine/install-windows/choose-a-database-engine-upgrade-method.md).  
  
    -   Para obter o "Technical Upgrade Guide" mais detalhado em formato PDF, [clique aqui](http://download.microsoft.com/download/7/1/5/715BDFA7-51B6-4D7B-AF17-61E78C7E538F/SQL_Server_2014_Upgrade_technical_guide.pdf).  
  
        > [!NOTE]  
        >  Atualmente, esta é a versão do SQL Server 2014 do "Guia Técnico de Atualização". A versão do SQL Server 2016 do guia ainda não está disponível.  
  
-   Para obter mais informações, diretrizes e ferramentas para planejar e automatizar sua migração ou atualização, consulte [Fim do suporte do SQL Server 2005](http://www.microsoft.com/en-us/server-cloud/products/sql-server-2005/).  
  
## Obter o SQL Server 2016  
 Para baixar uma cópia de avaliação do SQL Server 2016, [clique aqui](https://www.microsoft.com/en-us/evalcenter/evaluate-sql-server-2016/?wt.mc_id=upgrade2005).  
  
## Consulte também  
 [SQL Server 2016](http://www.microsoft.com/en-us/server-cloud/products/sql-server-2016/default.aspx)   
 [Fim do suporte do SQL Server 2005](http://www.microsoft.com/en-us/server-cloud/products/sql-server-2005/)   
 [Atualização do SQL Server 2005 para o SQL Server 2014](https://msdn.microsoft.com/en-us/library/mt170591\(v=sql.120\).aspx)  
  
  