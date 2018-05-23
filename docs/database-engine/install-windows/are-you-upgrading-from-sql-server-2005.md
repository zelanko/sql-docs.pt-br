---
title: Você está atualizando do SQL Server 2005? | Microsoft Docs
ms.custom: ''
ms.date: 07/18/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: install
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: ad40e66f-71fe-4ee6-9ce3-17127e7b1d7a
caps.latest.revision: 21
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 673a02355e33dec5bcbf27b052804898318758e3
ms.sourcegitcommit: ee661730fb695774b9c483c3dd0a6c314e17ddf8
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/19/2018
---
# <a name="are-you-upgrading-from-sql-server-2005"></a>Você está atualizando do SQL Server 2005?

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]
 
 O fim do suporte estendido para o SQL Server 2005 é um motivo para atualizar agora para uma versão mais recente do SQL Server e do Banco de Dados SQL do Microsoft Azure. A atualização permite manter a segurança e a conformidade, alcançar um desempenho inovador e otimizar a infraestrutura da plataforma de dados.  
  
 Para obter mais informações, diretrizes e ferramentas para planejar e automatizar sua migração ou atualização, consulte [Fim do suporte do SQL Server 2005](http://www.microsoft.com/en-us/server-cloud/products/sql-server-2005/).  
  
## <a name="why-upgrade"></a>Por que atualizar?  
  
> [!IMPORTANT]  
>  O suporte estendido para o SQL Server 2005 terminou em 12 de abril de 2016. Se você ainda estiver executando o SQL Server 2005 após 12 de abril de 2016, deixará de receber atualizações de segurança.  
  
## <a name="choose-your-upgrade-option"></a>Escolher sua opção de atualização  
Se você estiver atualizando bancos de dados relacionais do SQL Server 2005, aqui estão as opções para armazenamento relacional na plataforma Microsoft.  
  
Para ver uma análise mais abrangente dessas opções, [clique aqui](http://sql05upgrade.azurewebsites.net/).  
  
|Opção de armazenamento relacional|Benefícios|Outros fatores a considerar|  
|-------------------------------|--------------|-------------------------------|  
|**SQL Server no local**<br /><br /> Considere esta opção para aplicativos de banco de dados de qualquer tipo, desde sistemas transacionais até data warehouses.|Você tem o máximo de controle sobre recursos e escalabilidade porque você gerencia tanto o hardware quanto o software.<br /><br /> Se você estiver atualizando do SQL Server 2005, esse é o ambiente mais semelhante.|Você precisa fazer o maior investimento inicial e fornecer o gerenciamento mais contínuo, pois você precisa comprar, manter e gerenciar seu próprio hardware e software.<br /><br /> Para obter mais informações, consulte [SQL Server](https://www.microsoft.com/EN-US/server-cloud/products/sql-server-2017/).|  
|**SQL Server hospedado em máquinas virtuais do Azure**<br /><br /> Considere essa opção se você quiser o seguinte:<br /><br /> Benefícios da migração para um ambiente hospedado.<br /><br /> Controle sobre o ambiente operacional.<br /><br /> Conjunto de recursos familiares do SQL Server.|Você pode implantar rapidamente de uma biblioteca de imagens de máquinas virtuais.<br /><br /> Obtenha o conjunto completo de recursos do SQL Server.<br /><br /> Você economiza o custo de hardware e do software para servidores. Você paga apenas pelo uso por hora.|Você precisa configurar e gerenciar ambos o SQL Server e o software do sistema operacional.<br /><br /> <br /><br /> Para saber mais, confira [Visão geral do SQL Server em máquinas virtuais do Azure](https://azure.microsoft.com/documentation/articles/virtual-machines-sql-server-infrastructure-services/).<br /><br /> Para obter informações sobre a migração, consulte [Migrar um banco de dados para o SQL Server em uma VM do Azure](https://azure.microsoft.com/documentation/articles/virtual-machines-migrate-onpremises-database/).|  
|**Serviço de banco de dados hospedado do banco de dados SQL do Azure**<br /><br /> Considere esta opção se você quiser uma solução de baixo custo com menos manutenção.<br /><br /> Essa opção é especialmente apropriada para aplicativos que não exigem a mesma capacidade durante todo o tempo ou que devem fornecer acesso externo.|Você pode implantar rapidamente e escalar verticalmente com facilidade.<br /><br /> Você paga apenas pelo uso por hora.<br /><br /> O custo do serviço inclui não apenas armazenamento, mas alta disponibilidade e backups automáticos.|O banco de dados SQL do Azure não tem alguns recursos do SQL Server que não são aplicáveis em um ambiente de nuvem hospedado. Para obter mais informações, veja [Informações do Transact-SQL do Banco de Dados SQL do Azure](https://azure.microsoft.com/documentation/articles/sql-database-transact-sql-information/).<br /><br /> O banco de dados SQL do Azure também tem um tamanho máximo de 500 GB, em comparação com 524 PB para o SQL Server.<br /><br /> Para saber mais, confira [Banco de Dados SQL](https://azure.microsoft.com/services/sql-database/).<br /><br /> Para saber mais sobre a migração, confira [Migração de um banco de dados do SQL Server para um banco de dados SQL do Azure](https://azure.microsoft.com/documentation/articles/sql-database-cloud-migrate/).|  
  
 Você também pode desejar considerar uma solução não relacional ou NoSQL para determinados aplicativos e dados.  
  
|Solução não relacional|Benefícios|  
|------------------------------|--------------|  
|**Azure Cosmos DB**<br /><br /> Considere esta opção para aplicativos Web modernos, escalonáveis e móveis que usam dados JSON e exigem uma combinação de consultas robustas e processamento de dados transacional.<br /><br /> Para obter mais informações, consulte [Cosmos DB](http://azure.microsoft.com/services/cosmos-db/).<br /><br /> Para obter informações sobre como importar dados, consulte [Importar dados para o Cosmos DB](http://docs.microsoft.com/azure/cosmos-db/import-data/).|Os documentos são indexados e você pode usar uma sintaxe SQL familiar para consultá-los.<br /><br /> O banco de dados é livre de esquemas.<br /><br /> Você pode adicionar propriedades aos documentos sem precisar recompilar índices.<br /><br /> Você obtém suporte ao JSON e ao JavaScript dentro do mecanismo de banco de dados.<br /><br /> Você obtém suporte nativo para dados geoespaciais e integração com outros serviços do Azure, incluindo Pesquisa do Azure, HDInsight e Data Factory.<br /><br /> Obtenha armazenamento de baixa latência e alto desempenho com níveis de produtividade reservados.|  
|**Armazenamento de tabela do Azure**<br /><br /> Considere esta opção para armazenar petabytes de dados semiestruturados em uma solução econômica.<br /><br /> Para obter mais informações, consulte o [Armazenamento de Tabela](https://azure.microsoft.com/services/storage/tables/).|Você pode evoluir seus aplicativos e seu esquema de tabela sem colocar os dados offline.<br /><br /> Você pode escalar verticalmente sem fragmentar seu conjunto de dados.<br /><br /> Você obtém armazenamento com redundância geográfica que replica os dados por várias regiões.|  
  
## <a name="plan-your-upgrade"></a>Planejar sua atualização  
  
-   Leia sobre como planejar sua atualização na seguinte série de postagens no blog da equipe do SQL Server:  
  
    -   [Planejamento de uma atualização eficiente do SQL Server 2005: etapa 1 de 3](http://blogs.technet.com/b/dataplatforminsider/archive/2015/12/10/planning-an-efficient-upgrade-from-sql-server-2005-step-1-of-3.aspx)  
  
    -   [Planejamento de uma atualização eficiente do SQL Server 2005: etapa 2 de 3](http://blogs.technet.com/b/dataplatforminsider/archive/2015/12/15/planning-an-efficient-upgrade-from-sql-server-2005-step-2-of-3.aspx)  
  
    -   [Planejamento de uma atualização eficiente do SQL Server 2005: etapa 3 de 3](http://blogs.technet.com/b/dataplatforminsider/archive/2015/12/17/planning-an-efficient-upgrade-from-sql-server-2005-step-3-of-3.aspx)  
  
-   Examine os requisitos e as considerações em [Planejando uma instalação do SQL Server](../../sql-server/install/planning-a-sql-server-installation.md), incluindo os [Requisitos de hardware e software para a instalação do SQL Server](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md).  
  
-   Leia sobre como atualizar.  
  
    -   Analise os métodos de atualização disponíveis e saiba como planejar e testar no artigo [Atualizar Mecanismo de Banco de Dados](../../database-engine/install-windows/upgrade-database-engine.md).  
  
        > [!IMPORTANT]  
        >  Não é possível fazer upgrade de uma instância do SQL Server 2005 para um servidor do SQL Server 2017 in-loco. É necessário instalar uma instância do SQL Server 2017 e, em seguida, migrar os bancos de dados do SQL Server 2005 para a nova instalação. Para saber mais, confira a seção "Nova Atualização da Instalação" no artigo [Escolher um Método de Atualização de Mecanismo de Banco de Dados](../../database-engine/install-windows/choose-a-database-engine-upgrade-method.md).  
   
  
-   Para obter mais informações, diretrizes e ferramentas para planejar e automatizar sua migração ou atualização, consulte [Fim do suporte do SQL Server 2005](http://www.microsoft.com/en-us/server-cloud/products/sql-server-2005/).  
  
## <a name="get-sql-server"></a>Obtenha o SQL Server  
 Para baixar uma cópia de avaliação do SQL Server, [clique aqui](http://www.microsoft.com/evalcenter/evaluate-sql-server-2016).  
  
## <a name="next-steps"></a>Next Steps  
 [SQL Server 2017](http://www.microsoft.com/sql-server/sql-server-2017)   
 [Fim do suporte do SQL Server 2005](http://www.microsoft.com/en-us/server-cloud/products/sql-server-2005/)   
  
  
