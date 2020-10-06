---
title: Atualizações de versão e edição com suporte (SQL Server 2019)
description: As atualizações de versão e edição com suporte do SQL Server 2019.
ms.custom: ''
ms.date: 11/04/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
helpviewer_keywords:
- components [SQL Server], adding to existing installations
- versions [SQL Server], upgrading
- upgrading SQL Server, upgrades supported
- cross-language support
ms.assetid: 702359c4-6ca9-42a8-860c-a95a802898a1
author: MashaMSFT
ms.author: mathoma
monikerRange: '>=sql-server-2017||=sqlallproducts-allversions'
ms.openlocfilehash: 687f314e776dcc049f03cb4c8a164fb5fa84073e
ms.sourcegitcommit: 2f868a77903c1f1c4cecf4ea1c181deee12d5b15
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2020
ms.locfileid: "91670193"
---
# <a name="supported-version--edition-upgrades-sql-server-2019"></a>Atualizações de versão e edição com suporte (SQL Server 2019)

[!INCLUDE [SQL Server -Windows Only](../../includes/applies-to-version/sql-windows-only.md)]
  
  Você pode atualizar do [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)], [!INCLUDE[sssql16-md](../../includes/sssql16-md.md)]e [!INCLUDE[sssql17-md](../../includes/sssql17-md.md)]. Este artigo lista os caminhos de atualização compatíveis dessas versões do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e as atualizações de edição compatíveis para o [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)].  
  
## <a name="pre-upgrade-checklist"></a>Lista de verificação anterior à atualização  

- Antes de atualizar de uma edição do [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] para outra, verifique se há suporte à funcionalidade usada no momento na edição que você utilizará.  
- Verifique o [hardware e o software](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server-ver15.md) com suporte.
- Antes de atualizar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], habilite a Autenticação do Windows para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent e verifique a configuração padrão: se a conta de serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent é membro do grupo sysadmin do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .
- Para atualizar para o [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)], você deverá estar executando um sistema operacional com suporte. Para obter mais informações, consulte [Requisitos de hardware e software para a instalação do SQL Server](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server-ver15.md).  
- A atualização será bloqueada se houver uma reinicialização pendente.  
- A atualização será bloqueada, se o serviço do Windows Installer não estiver sendo executado.

## <a name="unsupported-scenarios"></a>Cenários com suporte

- Não há suporte a instâncias de várias versões do [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)]. Os números de versão dos componentes do [!INCLUDE[ssDE](../../includes/ssde-md.md)] devem ser os mesmos em uma instância do [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)].  
  
- O [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] está disponível apenas em plataformas de 64 bits. A atualização de plataforma cruzada não é suportada. Não é possível atualizar uma instância de 32 bits do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para uma nativa de 64 bits usando a Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . No entanto, será possível fazer backup de bancos de dados ou desanexá-los de uma instância de 32 bits do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]e, em seguida, restaurá-los ou anexá-los a uma nova instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (de 64 bits), se os bancos de dados não forem publicados na replicação. Você deverá recriar logons e outros objetos de usuário nos bancos de dados do sistema master, msdb e model.  
  
- Não é possível adicionar novos recursos durante a atualização da instância existente do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Depois de atualizar uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para o [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)], você poderá adicionar recursos usando a Instalação do [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)]. Para obter mais informações, consulte [Adicionar recursos a uma instância do SQL Server &#40;Instalação&#41;](./add-features-to-an-instance-of-sql-server-setup.md).  
 
## <a name="upgrades-from-earlier-versions-to-sssqlv15-md"></a>Atualizações de versões anteriores para o [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)]  
 
O [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] dá suporte ao upgrade das seguintes versões do SQL Server:

- [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP4 ou posterior
- [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] SP3 ou posterior
- [!INCLUDE[ssSQL16](../../includes/sssql16-md.md)] SP2 ou posterior
- [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)]

A tabela a seguir lista os cenários de atualização com suporte de versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para o [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)].  
  
|Atualização de|Caminho de atualização suportado|  
|:------|:------|  
|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP4 Enterprise|[!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Enterprise <br/> |  
|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP4 Developer|[!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Developer <br/> <br/> [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Standard <br/> <br/>[!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Web <br/> <br/> [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Enterprise <br/> |
|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP4 Standard|[!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Enterprise <br/><br/> [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Standard|  
|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP4 Web|[!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Enterprise <br/><br/> [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Standard <br/> <br/> [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Web|  
|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP4 Express |[!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Enterprise <br/><br/> [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Standard <br/> <br/> [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Web <br/> <br/> [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Express <br/> <br/> |  
|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP4 Business Intelligence|[!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Enterprise <br/> |  
|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP4 Evaluation|[!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Evaluation <br/> <br/> [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Enterprise <br/><br/> [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Standard <br/> <br/> [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Web <br/> <br/> [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Developer|  
|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] SP2 Enterprise|[!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Enterprise <br/> |  
|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] SP2 Developer|[!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Developer <br/> <br/> [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Standard <br/> <br/> [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Web <br/> <br/> [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Enterprise <br/> |  
|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] SP2 Standard|[!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Enterprise <br/><br/> [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Standard|  
|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] SP2 Web|[!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Enterprise <br/><br/> [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Standard <br/> <br/> [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Web|  
|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] SP2 Express |[!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Enterprise <br/><br/> [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Standard <br/> <br/> [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Web <br/> <br/> [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Express <br/> <br/> [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Developer|  
|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] SP2 Business Intelligence|[!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Enterprise <br/> |  
|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] SP2 Evaluation|[!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Evaluation <br/> <br/> [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Enterprise <br/><br/> [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Standard <br/> <br/> [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Web <br/> <br/> [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Developer|
|[!INCLUDE[ssSQL16](../../includes/sssql16-md.md)] 13.0.1601.5 Enterprise|[!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Enterprise <br/> |  
|[!INCLUDE[ssSQL16](../../includes/sssql16-md.md)] 13.0.1601.5 Developer|[!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Developer <br/> <br/> [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Standard <br/> <br/> [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Web <br/> <br/> [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Enterprise <br/> |  
|[!INCLUDE[ssSQL16](../../includes/sssql16-md.md)] 13.0.1601.5 Standard|[!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Enterprise <br/><br/> [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Standard|  
|[!INCLUDE[ssSQL16](../../includes/sssql16-md.md)] 13.0.1601.5 Web|[!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Enterprise <br/><br/> [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Standard <br/> <br/> [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Web|  
|[!INCLUDE[ssSQL16](../../includes/sssql16-md.md)] 13.0.1601.5 Express |[!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Enterprise <br/><br/> [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Standard <br/> <br/> [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Web <br/> <br/> [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Express <br/> <br/> [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Developer|  
|[!INCLUDE[ssSQL16](../../includes/sssql16-md.md)] 13.0.1601.5 Business Intelligence|[!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Enterprise <br/> |  
|[!INCLUDE[ssSQL16](../../includes/sssql16-md.md)] 13.0.1601.5 Evaluation|[!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Evaluation <br/> <br/> [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Enterprise <br/><br/> [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Standard <br/> <br/> [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Web <br/> <br/> [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Developer|
|[!INCLUDE[sssqlv14](../../includes/sssqlv14-md.md)] Enterprise|[!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Enterprise <br/> |  
|[!INCLUDE[sssqlv14](../../includes/sssqlv14-md.md)] Developer|[!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Developer <br/> <br/> [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Standard <br/> <br/> [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Web <br/> <br/> [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Enterprise <br/> |  
|[!INCLUDE[sssqlv14](../../includes/sssqlv14-md.md)] Standard|[!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Enterprise <br/><br/> [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Standard|  
|[!INCLUDE[sssqlv14](../../includes/sssqlv14-md.md)] Web|[!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Enterprise <br/><br/> [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Standard <br/> <br/> [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Web|  
|[!INCLUDE[sssqlv14](../../includes/sssqlv14-md.md)] Express |[!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Enterprise <br/><br/> [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Standard <br/> <br/> [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Web <br/> <br/> [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Express <br/> <br/> [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Developer|  
|[!INCLUDE[sssqlv14](../../includes/sssqlv14-md.md)] Business Intelligence|[!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Enterprise <br/> |  
|[!INCLUDE[sssqlv14](../../includes/sssqlv14-md.md)] Evaluation|[!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Evaluation <br/> <br/> [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Enterprise <br/><br/> [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Standard <br/> <br/> [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Web <br/> <br/> [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Developer|
|[!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] versão release candidate* |[!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Enterprise |  
|[!INCLUDE[sssqlv15_md](../../includes/sssqlv15-md.md)] Developer |[!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Enterprise | 

 \* O Suporte da Microsoft para atualização do software versão Release Candidate destina-se especificamente aos clientes que participaram do Programa de Usuário Pioneiro.

## <a name="migrate-to-sql-server-2019"></a>Migrar para o SQL Server 2019

Você pode migrar os bancos de dados de versões mais antigas. Por exemplo, pode migrar bancos de dados do [!INCLUDE [sskilimanjaro-md](../../includes/sskilimanjaro-md.md)] para o SQL Server 2019.

Para obter informações, confira o [Guia de migração de banco de dados do Azure](https://datamigration.microsoft.com/scenario/sql-to-sqlserver).

As seguintes dicas e ferramentas podem ajudar você a planejar e implementar sua migração.

- Ferramentas de migração: Há suporte para a migração por meio do [DMA (Assistente de Migração de Dados)](../../dma/dma-overview.md).
- Backup e restauração: Um backup feito no SQL Server 2008 ou no SQL Server 2008 R2 pode ser restaurado para o SQL Server 2019.
- Envio de logs: O envio de logs terá suporte se o primário estiver executando o SQL Server 2008 SP3 ou posterior (ou o SQL Server 2008 R2 SP2 ou posterior) e o secundário estiver executando o SQL Server 2019. 

   > [!WARNING]
   > Se ocorrer um failover automático ou manual e a instância do SQL Server 2019 se tornar a primária, a instância do SQL Server 2008 ou do SQL Server 2008 R2 se tornará a secundária e não poderá receber alterações do primário.

- Carregamento em massa: As tabelas podem ser copiadas em massa do SQL Server 2008 ou do SQL Server 2008 R2 para o SQL Server 2019.

## <a name="sssqlv15-md-edition-upgrade"></a>[!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Edition 

A tabela a seguir lista os cenários de atualização de edição com suporte no [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)].  

Para obter instruções passo a passo sobre como fazer um upgrade de edição, consulte [Fazer upgrade para outra edição do SQL Server &#40;Instalação&#41;](../../database-engine/install-windows/upgrade-to-a-different-edition-of-sql-server-setup.md).  
  
|Atualização de|Atualização para|  
|------------------|----------------|  
|[!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Enterprise (Licença Server+CAL e Baseada em Núcleo)**|[!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Enterprise |  
|[!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Evaluation Enterprise**|[!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Enterprise (Licença Server+CAL ou Baseada em Núcleo) <br/><br/> [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Standard <br/> <br/> [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Developer <br/> <br/> [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Web <br/> <br/> A atualização da Evaluation (uma edição gratuita) para qualquer uma das edições pagas tem suporte em instalações autônomas, mas não tem suporte em instalações clusterizadas. Essa limitação não se aplica a instâncias autônomas instaladas em um cluster de failover do Windows que participa de um grupo de disponibilidade. |  
|[!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Standard**|[!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Enterprise (Licença Server+CAL ou Baseada em Núcleo)|  
|[!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Developer**|[!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Enterprise (Licença Server+CAL ou Baseada em Núcleo) <br/><br/> [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Web <br/> <br/> [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Standard|  
|[!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Web|[!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Enterprise (Licença Server+CAL ou Baseada em Núcleo) <br/><br/> [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Standard|  
|[!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Express*|[!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Enterprise (Licença Server+CAL ou Baseada em Núcleo) <br/><br/> [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Developer <br/> <br/> [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Standard <br/> <br/> [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Web|  
  
 Além disso, você também pode executar uma atualização de edição entre o [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Enterprise (Licença Server+CAL) e [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Enterprise (Licença Baseada em Núcleo):  
  
|Atualização de edição do|Atualização de edição para|  
|--------------------------|------------------------|  
|[!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Enterprise (Licença Server+CAL)**|[!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Enterprise (Licença Baseada em Núcleo)|  
|[!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Enterprise (Licença Baseada em Núcleo)|[!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Enterprise (Licença Server+CAL)|  
  
 \* Também se aplica ao [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Express with Tools e ao [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Express with Advanced Services.  
  
 ** Alterar a edição de uma instância clusterizada do [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] limitado. Os cenários a seguir não têm suporte para clusters de failover do [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] :  
  
- [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Enterprise para [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Developer, Standard ou Evaluation.  
  
- [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Developer para [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Standard ou Evaluation.  
  
- [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Standard para [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Evaluation.  
  
- [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Evaluation para [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Standard.  
  
## <a name="see-also"></a>Consulte Também  

 [Edições e recursos com suporte do [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)]](../../sql-server/editions-and-components-of-sql-server-version-15.md)

 [Requisitos de hardware e software para a instalação do SQL Server](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server-ver15.md)

 [Atualizar o SQL Server](../../database-engine/install-windows/upgrade-sql-server.md)