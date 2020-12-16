---
title: Atualizações de versão e edição com suporte (SQL Server 2017)
description: As atualizações de versão e edição com suporte do SQL Server 2017.
ms.custom: seo-lt-2019
ms.date: 12/13/2019
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
author: cawrites
ms.author: chadam
monikerRange: '>=sql-server-2016'
ms.openlocfilehash: 5c0d8067de4a045d6884258f88c09947c27c09c0
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97463577"
---
# <a name="supported-version--edition-upgrades-sql-server-2017"></a>Atualizações de versão e edição com suporte (SQL Server 2017)

[!INCLUDE [SQL Server -Windows Only](../../includes/applies-to-version/sql-windows-only.md)]
  
  É possível fazer upgrade do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)]. Este artigo lista os caminhos de atualização compatíveis dessas versões do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e as atualizações de edição compatíveis para o [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)].  
  
## <a name="pre-upgrade-checklist"></a>Lista de verificação anterior à atualização  
  
-   Antes de atualizar de uma edição do [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] para outra, verifique se há suporte à funcionalidade usada no momento na edição que você utilizará.  
  
-   Antes de atualizar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], habilite a Autenticação do Windows para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent e verifique a configuração padrão: se a conta de serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent é membro do grupo sysadmin do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   Para atualizar para o [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)], você deverá estar executando um sistema operacional com suporte. Para obter mais informações, consulte [Requisitos de hardware e software para a instalação do SQL Server](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md).  
  
-   A atualização será bloqueada se houver uma reinicialização pendente.  
  
-   A atualização será bloqueada, se o serviço do Windows Installer não estiver sendo executado.  
  
## <a name="unsupported-scenarios"></a>Cenários com suporte  
  
-   Não há suporte a instâncias de várias versões do [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)]. Os números de versão dos componentes do [!INCLUDE[ssDE](../../includes/ssde-md.md)] devem ser os mesmos em uma instância do [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)].  
  
-   O [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] está disponível apenas em plataformas de 64 bits. A atualização de plataforma cruzada não é suportada. Não é possível atualizar uma instância de 32 bits do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para uma nativa de 64 bits usando a Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . No entanto, será possível fazer backup de bancos de dados ou desanexá-los de uma instância de 32 bits do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]e, em seguida, restaurá-los ou anexá-los a uma nova instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (de 64 bits), se os bancos de dados não forem publicados na replicação. Você deverá recriar logons e outros objetos de usuário nos bancos de dados do sistema master, msdb e model.  
  
-   Não é possível adicionar novos recursos durante a atualização da instância existente do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Depois de atualizar uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para o [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)], você poderá adicionar recursos usando a Instalação do [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)]. Para obter mais informações, consulte [Adicionar recursos a uma instância do SQL Server &#40;Instalação&#41;](./add-features-to-an-instance-of-sql-server-setup.md).  
 
-   Não há suporte para clusters de failover no modo WOW.  
    
## <a name="upgrades-from-earlier-versions-to-sssqlv14-md"></a>Atualizações de versões anteriores para o [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)]  
 
O [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] dá suporte ao upgrade das seguintes versões do SQL Server:
 
- SQL Server 2008 SP4 ou posterior
- SQL Server 2008 R2 SP3 ou posterior
- SQL Server 2012 SP2 ou posterior
- SQL Server 2014 ou posterior 
- SQL Server 2016 ou posterior
 

  
> [!NOTE]  
>  Para atualizar os bancos de dados no [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] , veja [Suporte para 2005](#SupportFor2005).  
  
 A tabela a seguir lista os cenários de atualização com suporte de versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para o [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)].  
  
|Atualização de|Caminho de atualização suportado|  
|:------|:------|  
|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] SP4 Enterprise|[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Enterprise <br/> |  
|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] SP4 Developer|[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Developer|  
|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] SP4 Standard|[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Enterprise <br/><br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Standard|  
|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] SP4 Small Business|[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Standard|  
|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] SP4 Web|[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Enterprise <br/><br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Standard <br/> <br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Web|  
|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] SP4 Workgroup|[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Enterprise <br/><br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Standard|  
|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] SP4 Express |[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Enterprise <br/><br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Standard <br/> <br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Web <br/> <br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Express|  
|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] SP3 Datacenter|[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Enterprise <br/> |  
|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] SP3 Enterprise|[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Enterprise <br/> |  
|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] SP3 Developer|[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Developer|  
|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] SP3 Small Business|[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Standard|  
|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] SP3 Standard|[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Enterprise <br/><br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Standard|  
|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] SP3 Web|[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Enterprise <br/><br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Standard <br/> <br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Web|  
|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] SP3 Workgroup|[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Enterprise <br/><br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Standard|  
|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] SP3 Express |[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Enterprise <br/><br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Standard <br/> <br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Web <br/> <br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Express|  
|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP2 Enterprise|[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Enterprise <br/> |  
|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP2 Developer|[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Developer <br/> <br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Standard <br/> <br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Web <br/> <br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Enterprise <br/> |  
|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP2 Standard|[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Enterprise <br/><br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Standard|  
|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP1 Web|[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Enterprise <br/><br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Standard <br/> <br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Web|  
|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP2 Express |[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Enterprise <br/><br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Standard <br/> <br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Web <br/> <br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Express <br/> <br/> |  
|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP2 Business Intelligence|[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Enterprise <br/> |  
|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP2 Evaluation|[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Evaluation <br/> <br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Enterprise <br/><br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Standard <br/> <br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Web <br/> <br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Developer|  
|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise|[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Enterprise <br/> |  
|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Developer|[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Developer <br/> <br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Standard <br/> <br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Web <br/> <br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Enterprise <br/> |  
|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Standard|[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Enterprise <br/><br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Standard|  
|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Web|[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Enterprise <br/><br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Standard <br/> <br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Web|  
|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Express |[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Enterprise <br/><br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Standard <br/> <br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Web <br/> <br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Express <br/> <br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Developer|  
|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Business Intelligence|[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Enterprise <br/> |  
|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Evaluation|[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Evaluation <br/> <br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Enterprise <br/><br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Standard <br/> <br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Web <br/> <br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Developer|
|[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] Enterprise|[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Enterprise <br/> |  
|[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] Developer|[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Developer <br/> <br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Standard <br/> <br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Web <br/> <br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Enterprise <br/> |  
|[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] Standard|[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Enterprise <br/><br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Standard|  
|[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] Web|[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Enterprise <br/><br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Standard <br/> <br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Web|  
|[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] Express |[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Enterprise <br/><br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Standard <br/> <br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Web <br/> <br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Express <br/> <br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Developer|  
|[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] Business Intelligence|[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Enterprise <br/> |  
|[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] Evaluation|[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Evaluation <br/> <br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Enterprise <br/><br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Standard <br/> <br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Web <br/> <br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Developer|
|[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] versão release candidate* |[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Enterprise |  
|[!INCLUDE[sssqlv14_md](../../includes/sssqlv14-md.md)] Developer |[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Enterprise | 

 \* O suporte da Microsoft para atualização do software versão Release Candidate destina-se especificamente aos clientes que participaram do TAP (Technology Adoption Program). 

   
###  <a name="sssqlv14-md-support-for-ssversion2005"></a><a name="SupportFor2005"></a> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Suporte para [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]  
 Esta seção aborda o suporte do [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] para [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]. No [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)], você poderá fazer o seguinte:  
  
-   Anexar um banco de dados do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] (arquivos mdf/ldf) à instância do [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] do mecanismo de banco de dados.  
  
-   Restaurar um banco de dados do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] para a instância do [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] do mecanismo de banco de dados de um backup.  
  
-   Fazer backup de um cubo do [!INCLUDE[ssASversion2005](../../includes/ssasversion2005-md.md)] e restaurá-lo no [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)].  
  
Quando um banco de dados do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] é atualizado para [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)], o nível de compatibilidade do banco de dados é alterado de 90 para 100. (No [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)], os valores válidos do nível de compatibilidade do banco de dados são 100, 110, 120, 130 e 140.) [ALTER DATABASE Compatibility Level &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md) aborda como a alteração do nível de compatibilidade pode afetar os aplicativos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
Os cenários não especificados na lista anterior não são suportados, incluindo, mas sem estar limitado, os seguintes:  
  
- Instalando o [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] e [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] no mesmo computador (lado a lado).  
  
- Usando uma instância do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] como um membro da topologia de replicação que envolve uma instância do [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)].  
  
- Configurando o espelhamento de banco de dados entre as instâncias do [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] e do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] .  
  
- Fazendo backup do registro de transações com envio de logs entre as instâncias do [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] e do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] .  
  
- Configurando servidores vinculados entre as instâncias do [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] e do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] .  
  
- Gerenciando uma instância do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] no [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Management Studio.  
  
- Anexando um cubo do [!INCLUDE[ssASversion2005](../../includes/ssasversion2005-md.md)] no [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Management Studio.  
  
- Conectando-se ao [!INCLUDE[ssISversion2005](../../includes/ssisversion2005-md.md)] a partir do [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Management Studio.  
  
- Gerenciando um serviço do [!INCLUDE[ssISversion2005](../../includes/ssisversion2005-md.md)] no [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Management Studio.  
  
- Suporte para componentes personalizados do Integration Services de terceiros do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] , como executar e atualizar.  
  
## <a name="sssqlv14-md-edition-upgrade"></a>[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Edition  
A tabela a seguir lista os cenários de atualização de edição com suporte no [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)].  
  
Para obter instruções passo a passo sobre como fazer um upgrade de edição, consulte [Fazer upgrade para outra edição do SQL Server &#40;Instalação&#41;](../../database-engine/install-windows/upgrade-to-a-different-edition-of-sql-server-setup.md).  
  
|Atualização de|Atualização para|  
|------------------|----------------|  
|[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Enterprise (Licença Server+CAL e Baseada em Núcleo)**|[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Enterprise |  
|[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Evaluation Enterprise**|[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Enterprise (Licença Server+CAL ou Baseada em Núcleo) <br/><br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Standard <br/> <br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Developer <br/> <br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Web <br/> <br/> A atualização da Evaluation (uma edição gratuita) para qualquer uma das edições pagas tem suporte em instalações autônomas, mas não tem suporte em instalações clusterizadas. Essa limitação não se aplica a instâncias autônomas instaladas em um cluster de failover do Windows que participa de um grupo de disponibilidade.|  
|[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Standard**|[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Enterprise (Licença Server+CAL ou Baseada em Núcleo)|  
|[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Developer**|[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Enterprise (Licença Server+CAL ou Baseada em Núcleo) <br/><br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Web <br/> <br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Standard|  
|[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Web|[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Enterprise (Licença Server+CAL ou Baseada em Núcleo) <br/><br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Standard|  
|[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Express*|[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Enterprise (Licença Server+CAL ou Baseada em Núcleo) <br/><br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Developer <br/> <br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Standard <br/> <br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Web|  
  
 Além disso, você também pode executar uma atualização de edição entre o [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Enterprise (Licença Server+CAL) e [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Enterprise (Licença Baseada em Núcleo):  
  
|Atualização de edição do|Atualização de edição para|  
|--------------------------|------------------------|  
|[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Enterprise (Licença Server+CAL)**|[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Enterprise (Licença Baseada em Núcleo)|  
|[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Enterprise (Licença Baseada em Núcleo)|[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Enterprise (Licença Server+CAL)|  
  
 \* Também se aplica ao [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Express with Tools e ao [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Express with Advanced Services.  
  
 ** A alteração da edição de um cluster de failover do [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] é limitada. Os cenários a seguir não têm suporte para clusters de failover do [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] :  
  
-   [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Enterprise para [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Developer, Standard ou Evaluation.  
  
-   [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Developer para [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Standard ou Evaluation.  
  
-   [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Standard para [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Evaluation.  
  
-   [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Evaluation para [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Standard.  
  
## <a name="see-also"></a>Consulte Também  

 [Edições e recursos com suporte do SQL Server 2017](../../sql-server/editions-and-components-of-sql-server-2017.md)
 
 [Requisitos de Hardware e Software para a Instalação do SQL Server](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)   
 
 [Atualizar o SQL Server](../../database-engine/install-windows/upgrade-sql-server.md)  
  
