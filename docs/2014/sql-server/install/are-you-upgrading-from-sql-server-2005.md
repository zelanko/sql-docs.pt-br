---
title: Você está atualizando do SQL Server 2005? | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 3d50a66a-1845-4116-8b3a-7b5a2eeb78e6
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 5795d91c02227db555401b3474e19ae39f9dd759
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66096716"
---
# <a name="are-you-upgrading-from-sql-server-2005"></a>Você está atualizando do SQL Server 2005?
  O fim do suporte estendido para o SQL Server 2005 é um motivo para atualizar agora para uma versão mais recente do SQL Server e do Banco de Dados SQL do Microsoft Azure. A atualização permite manter a segurança e a conformidade, alcançar um desempenho inovador e otimizar a infraestrutura da plataforma de dados.  
  
 Para obter mais informações, diretrizes e ferramentas para planejar e automatizar sua migração ou atualização, consulte [Fim do suporte do SQL Server 2005](https://www.microsoft.com/en-us/server-cloud/products/sql-server-2005/).  
  
## <a name="why-upgrade"></a>Por que atualizar?  
  
> [!IMPORTANT]  
>  O suporte estendido para o SQL Server 2005 termina em 12 de abril de 2016. Se ainda estiver executando o SQL Server 2005 depois de 12 de abril de 2016, você deixará de receber atualizações de segurança.  
  
 Para obter a folha de dados no formato PDF sobre a atualização do SQL Server 2005, [clique aqui](https://info.microsoft.com/rs/157-GQE-382/images/EN-CNTNT-Infographic-UpgradeSQL2005Datasheet.pdf) (não na imagem em miniatura abaixo).  
  
 ![Folha de dados sobre a atualização do SQL Server 2005](../../../2014/sql-server/install/media/sqlserver2005eos.png "folha de dados sobre a atualização do SQL Server 2005")  
  
## <a name="choose-your-upgrade-option"></a>Escolher sua opção de atualização  
 Se você estiver atualizando bancos de dados relacionais do SQL Server 2005, aqui estão suas opções para armazenamento relacional na plataforma Microsoft.  
  
 Para ver uma análise mais abrangente dessas opções, [clique aqui](http://sql05upgrade.azurewebsites.net/).  
  
|Opção de armazenamento relacional|Benefícios|Outros fatores a considerar|  
|-------------------------------|--------------|-------------------------------|  
|**SQL Server no local**<br /><br /> Considere esta opção para aplicativos de banco de dados de qualquer tipo, desde sistemas transacionais até data warehouses.<br /><br /> Para obter mais informações, consulte [SQL Server 2014](https://www.microsoft.com/EN-US/server-cloud/products/sql-server/).|Você tem o máximo de controle sobre recursos e escalabilidade porque você gerencia tanto o hardware quanto o software.<br /><br /> Se você estiver atualizando do SQL Server 2005, isso é o ambiente mais semelhante.|Você precisa fazer o maior investimento inicial e fornecer o gerenciamento mais contínuo, pois você precisa comprar, manter e gerenciar seu próprio hardware e software.|  
|**SQL Server hospedado em máquinas virtuais do Azure**<br /><br /> Considere esta opção se você quiser as coisas a seguir.<br />-Benefícios de migrar para um ambiente hospedado.<br />-Controle sobre o ambiente operacional.<br />-Conjunto de recursos familiares do SQL Server.<br /><br /> Para obter mais informações, consulte [SQL Server na visão geral de máquinas virtuais do Azure](https://azure.microsoft.com/documentation/articles/virtual-machines-sql-server-infrastructure-services/).<br /><br /> Para obter informações sobre a migração, consulte [Migrar um banco de dados para o SQL Server em uma VM do Azure](https://azure.microsoft.com/documentation/articles/virtual-machines-migrate-onpremises-database/).|Você pode implantar rapidamente de uma biblioteca de imagens de máquinas virtuais.<br /><br /> Obtenha o conjunto completo de recursos do SQL Server.<br /><br /> Você economiza o custo de hardware e do software para servidores. Você paga apenas pelo uso por hora.|Você precisa configurar e gerenciar ambos o SQL Server e o software do sistema operacional.|  
|**Serviço de banco de dados hospedado do banco de dados SQL do Azure**<br /><br /> Considere esta opção se você quiser uma solução de baixo custo com menos manutenção.<br /><br /> Essa opção é especialmente apropriada para aplicativos que não exigem a mesma capacidade durante todo o tempo ou que devem fornecer acesso externo.<br /><br /> Para obter mais informações, consulte [banco de dados SQL](https://azure.microsoft.com/services/sql-database/).<br /><br /> Para obter informações sobre a migração, consulte [migrando um banco de dados do SQL Server para o banco de dados do Azure SQL](https://azure.microsoft.com/documentation/articles/sql-database-cloud-migrate/).|Você pode implantar rapidamente e escalar verticalmente com facilidade.<br /><br /> Você paga apenas pelo uso por hora.<br /><br /> O custo do serviço inclui não apenas armazenamento, mas alta disponibilidade e backups automáticos.|O banco de dados SQL do Azure não tem alguns recursos do SQL Server que não são aplicáveis em um ambiente de nuvem hospedado. Para obter mais informações, veja [Informações do Transact-SQL do Banco de Dados SQL do Azure](https://azure.microsoft.com/documentation/articles/sql-database-transact-sql-information/).<br /><br /> O banco de dados SQL do Azure também tem um tamanho máximo de 500 GB, em comparação com 524 PB para o SQL Server.|  
  
 Você também pode desejar considerar uma solução não relacional ou NoSQL para determinados aplicativos e dados.  
  
|Solução não relacional|Benefícios|  
|------------------------------|--------------|  
|**Banco de Dados de Documentos do Azure**<br /><br /> Considere esta opção para aplicativos Web modernos, escalonáveis e móveis que usam dados JSON e exigem uma combinação de consultas robustas e processamento de dados transacional.<br /><br /> Para obter mais informações, consulte [Banco de Dados de Documentos](https://azure.microsoft.com/en-us/services/documentdb/).|Os documentos são indexados e você pode usar uma sintaxe SQL familiar para consultá-los.<br /><br /> O banco de dados é livre de esquemas.<br /><br /> Você pode adicionar propriedades aos documentos sem precisar recompilar índices.<br /><br /> Você obtém suporte ao JSON e ao JavaScript dentro do mecanismo de banco de dados.<br /><br /> Você obtém suporte nativo para dados geoespaciais e integração com outros serviços do Azure, incluindo Pesquisa do Azure, HDInsight e Data Factory.<br /><br /> Obtenha armazenamento de baixa latência e alto desempenho com níveis de produtividade reservados.|  
|**Armazenamento de tabela do Azure**<br /><br /> Considere esta opção para armazenar petabytes de dados semiestruturados em uma solução econômica.<br /><br /> Para obter mais informações, consulte o [Armazenamento de Tabela](https://azure.microsoft.com/services/storage/tables/).|Você pode evoluir seus aplicativos e seu esquema de tabela sem colocar os dados offline.<br /><br /> Você pode escalar verticalmente sem fragmentar seu conjunto de dados.<br /><br /> Você obtém armazenamento com redundância geográfica que replica os dados por várias regiões.|  
  
 Para baixar o relatório “Migrating from SQL Server 2005” (Migrando do SQL Server 2005) pelas Diretrizes na Microsoft, que contém mais detalhes sobre as opções de atualização, [clique aqui](https://info.microsoft.com/CO-SQL-CNTNT-FY16-09Sep-14-ModernizationDirOnMFST-Register.html) (não na imagem em miniatura abaixo).  
  
 ![Relatório sobre a migração do SQL Server 2005](../../../2014/sql-server/install/media/sqlserver2005migratingdoc.png "relatório sobre a migração do SQL Server 2005")  
  
## <a name="plan-your-upgrade"></a>Planejar sua atualização  
  
-   Leia sobre como planejar sua atualização na seguinte série de postagens no blog da equipe do SQL Server:  
  
    -   [Planejando uma atualização eficiente do SQL Server 2005: Etapa 1 de 3](http://blogs.technet.com/b/dataplatforminsider/archive/2015/12/10/planning-an-efficient-upgrade-from-sql-server-2005-step-1-of-3.aspx)  
  
    -   [Planejando uma atualização eficiente do SQL Server 2005: Etapa 2 de 3](http://blogs.technet.com/b/dataplatforminsider/archive/2015/12/15/planning-an-efficient-upgrade-from-sql-server-2005-step-2-of-3.aspx)  
  
    -   [Planejando uma atualização eficiente do SQL Server 2005: Etapa 3 de 3](http://blogs.technet.com/b/dataplatforminsider/archive/2015/12/17/planning-an-efficient-upgrade-from-sql-server-2005-step-3-of-3.aspx)  
  
-   Examine os requisitos e as considerações em [Planejando uma instalação do SQL Server](../../../2014/sql-server/install/planning-a-sql-server-installation.md), incluindo o [Hardware and Software Requirements for Installing SQL Server 2014](hardware-and-software-requirements-for-installing-sql-server.md).  
  
-   Leia sobre como atualizar.  
  
    -   Analise os métodos de atualização disponíveis e saiba como planejar e testar no tópico [Upgrade Database Engine](../../database-engine/install-windows/upgrade-database-engine.md).  
  
        > [!IMPORTANT]  
        >  Você não pode atualizar um servidor do SQL Server 2005 para um servidor do SQL Server 2014 in-loco. É necessário instalar o SQL Server 2014 e então migrar seus bancos de dados do SQL Server 2005 para a nova instalação.  
  
    -   Para obter o "Technical Upgrade Guide" mais detalhado em formato PDF, [clique aqui](https://download.microsoft.com/download/7/1/5/715BDFA7-51B6-4D7B-AF17-61E78C7E538F/SQL_Server_2014_Upgrade_technical_guide.pdf).  
  
-   Para obter mais informações, diretrizes e ferramentas para planejar e automatizar sua migração ou atualização, consulte [Fim do suporte do SQL Server 2005](https://www.microsoft.com/en-us/server-cloud/products/sql-server-2005/).  
  
## <a name="get-sql-server-2014"></a>Obter o SQL Server 2014  
 Para baixar uma cópia de avaliação do SQL Server 2014, [clique aqui](https://www.microsoft.com/en-us/evalcenter/evaluate-sql-server-2014).  
  
## <a name="see-also"></a>Consulte também  
 [SQL Server 2014](https://www.microsoft.com/en-us/server-cloud/products/sql-server/default.aspx)   
 [Fim do suporte do SQL Server 2005](https://www.microsoft.com/en-us/server-cloud/products/sql-server-2005/)   
 [Atualização do SQL Server 2005 para SQL Server 2016](https://msdn.microsoft.com/library/mt168847.aspx)  
  
  
