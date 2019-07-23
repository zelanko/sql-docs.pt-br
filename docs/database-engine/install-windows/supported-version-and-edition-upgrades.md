---
title: Upgrades de versão e edição com suporte | Microsoft Docs
ms.custom: ''
ms.date: 06/27/2016
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
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: 99b6522316928fcd7397d27c1a5c85d927a8e0b9
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67934868"
---
# <a name="supported-version-and-edition-upgrades"></a>Atualizações de versão e edição com suporte

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]
  
  Você pode atualizar do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]e [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]. Este artigo lista os caminhos de atualização compatíveis dessas versões do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e as atualizações de edição compatíveis para o [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)].  
  
## <a name="pre-upgrade-checklist"></a>Lista de verificação anterior à atualização  
  
-   Antes de atualizar de uma edição do [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] para outra, verifique se há suporte à funcionalidade usada no momento na edição que você utilizará.  
  
-   Antes de atualizar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], habilite a Autenticação do Windows para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent e verifique a configuração padrão: se a conta de serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent é membro do grupo sysadmin do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   Para atualizar para o [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)], você deverá estar executando um sistema operacional com suporte. Para obter mais informações, veja [Requisitos de hardware e software para a instalação do SQL Server 2016](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md).  
  
-   A atualização será bloqueada se houver uma reinicialização pendente.  
  
-   A atualização será bloqueada, se o serviço do Windows Installer não estiver sendo executado.  
  
## <a name="unsupported-scenarios"></a>Cenários com suporte  
  
-   Não há suporte a instâncias de várias versões do [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)]. Os números de versão dos componentes do [!INCLUDE[ssDE](../../includes/ssde-md.md)], [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]e do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] devem ser os mesmos em uma instância do [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)].  
  
-   O [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] está disponível apenas em plataformas de 64 bits. A atualização de plataforma cruzada não é suportada. Não é possível atualizar uma instância de 32 bits do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para uma nativa de 64 bits usando a Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . No entanto, será possível fazer backup de bancos de dados ou desanexá-los de uma instância de 32 bits do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]e, em seguida, restaurá-los ou anexá-los a uma nova instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (de 64 bits), se os bancos de dados não forem publicados na replicação. Você deverá recriar logons e outros objetos de usuário nos bancos de dados do sistema master, msdb e model.  
  
-   Não é possível adicionar novos recursos durante a atualização da instância existente do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Depois de atualizar uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para o [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)], você poderá adicionar recursos usando a Instalação do [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)]. Para obter mais informações, veja [Adicionar recursos a uma instância do SQL Server 2016 &#40;Instalação&#41;](../../database-engine/install-windows/add-features-to-an-instance-of-sql-server-2016-setup.md).  
 
-   Não há suporte para clusters de failover no modo WOW.  
  
-   Não há suporte para a atualização de uma edição de Avaliação de uma versão anterior do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .

-   Ao fazer upgrade do RC1 ou de versões anteriores do SQL Server 2016 para o RC3 ou versões posteriores, o PolyBase deve ser desinstalado antes do upgrade e reinstalado após o upgrade.
  
## <a name="upgrades-from-earlier-versions-to-includesssql15-mdincludessssql15-mdmd"></a>Atualizações de versões anteriores para o [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)]  
 
O SQL Server 2016 dá suporte à atualização das seguintes versões do SQL Server:
 
- [!INCLUDE[ssKatmai](../../includes/ssKatmai-md.md)] SP4 ou posterior
- [!INCLUDE[ssKilimanjaro](../../includes/ssKilimanjaro-md.md)] SP3 ou posterior
- [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP2 ou posterior
- [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] ou posterior 
 
> [!NOTE]  
> Para atualizar os bancos de dados no [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] , veja [Suporte para 2005](#SupportFor2005).  
  
A tabela a seguir lista os cenários de atualização com suporte de versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para o [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)].  
  
|Atualização de|Caminho de atualização suportado|  
|------------------|----------------------------|  
|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] SP4 Enterprise|[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Enterprise <br/> |  
|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] SP4 Developer|[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Developer|  
|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] SP4 Standard|[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Enterprise <br/><br/> [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Standard|  
|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] SP4 Small Business|[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Standard|  
|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] SP4 Web|[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Enterprise <br/><br/> [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Standard <br/> <br/> [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Web|  
|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] SP4 Workgroup|[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Enterprise <br/><br/> [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Standard|  
|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] SP4 Express |[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Enterprise <br/><br/> [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Standard <br/> <br/> [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Web <br/> <br/> [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Express|  
|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] SP3 Datacenter|[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Enterprise <br/> |  
|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] SP3 Enterprise|[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Enterprise <br/> |  
|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] SP3 Developer|[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Developer|  
|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] SP3 Small Business|[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Standard|  
|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] SP3 Standard|[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Enterprise <br/><br/> [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Standard|  
|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] SP3 Web|[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Enterprise <br/><br/> [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Standard <br/> <br/> [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Web|  
|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] SP3 Workgroup|[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Enterprise <br/><br/> [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Standard|  
|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] SP3 Express |[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Enterprise <br/><br/> [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Standard <br/> <br/> [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Web <br/> <br/> [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Express|  
|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP2 Enterprise|[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Enterprise <br/> |  
|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP2 Developer|[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Developer <br/> <br/> [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Standard <br/> <br/> [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Web <br/> <br/> [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Enterprise <br/> |  
|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP2 Standard|[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Enterprise <br/><br/> [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Standard|  
|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP1 Web|[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Enterprise <br/><br/> [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Standard <br/> <br/> [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Web|  
|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP2 Express |[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Enterprise <br/><br/> [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Standard <br/> <br/> [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Web <br/> <br/> [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Express <br/> <br/> |  
|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP2 Business Intelligence|[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Enterprise <br/> |  
|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP2 Evaluation|[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Evaluation <br/> <br/> [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Enterprise <br/><br/> [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Standard <br/> <br/> [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Web <br/> <br/> [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Developer|  
|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise|[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Enterprise <br/> |  
|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Developer|[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Developer <br/> <br/> [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Standard <br/> <br/> [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Web <br/> <br/> [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Enterprise <br/> |  
|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Standard|[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Enterprise <br/><br/> [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Standard|  
|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Web|[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Enterprise <br/><br/> [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Standard <br/> <br/> [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Web|  
|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Express |[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Enterprise <br/><br/> [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Standard <br/> <br/> [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Web <br/> <br/> [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Express <br/> <br/> [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Developer|  
|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Business Intelligence|[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Enterprise <br/> |  
|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Evaluation|[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Evaluation <br/> <br/> [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Enterprise <br/><br/> [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Standard <br/> <br/> [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Web <br/> <br/> [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Developer|  
|[!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] versão release candidate* |[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Enterprise |  
|[!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] Developer |[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Enterprise | 

 \* O suporte da Microsoft para atualização do software versão Release Candidate destina-se especificamente aos clientes que participaram do TAP (Technology Adoption Program). 
   
###  <a name="SupportFor2005"></a> [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Suporte para [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]  
Esta seção aborda o suporte do [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] para [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]. No [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)], você poderá fazer o seguinte:  
  
-   Anexar um banco de dados do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] (arquivos mdf/ldf) à instância do [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] do mecanismo de banco de dados.  
  
-   Restaurar um banco de dados do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] para a instância do [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] do mecanismo de banco de dados de um backup.  
  
-   Fazer backup de um cubo do [!INCLUDE[ssASversion2005](../../includes/ssasversion2005-md.md)] e restaurar no [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)].  
  
> [!NOTE]  
> Quando um banco de dados do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] é atualizado para [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)], o nível de compatibilidade do banco de dados é alterado de 90 para 100. No [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)], os valores válidos do nível de compatibilidade do banco de dados são 100, 110, 120 e 130. [ALTER DATABASE Compatibility Level &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md) aborda como a alteração do nível de compatibilidade pode afetar os aplicativos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
Os cenários não especificados na lista anterior não são suportados, incluindo, mas sem estar limitado, os seguintes:  
  
-   Instalando o [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] e [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] no mesmo computador (lado a lado).  
  
-   Usando uma instância do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] como um membro da topologia de replicação que envolve uma instância do [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)].  
  
-   Configurando o espelhamento de banco de dados entre as instâncias do [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] e do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] .  
  
-   Fazendo backup do registro de transações com envio de logs entre as instâncias do [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] e do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] .  
  
-   Configurando servidores vinculados entre as instâncias do [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] e do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] .  
  
-   Gerenciando uma instância do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] no [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Management Studio.  
  
-   Anexando um cubo do [!INCLUDE[ssASversion2005](../../includes/ssasversion2005-md.md)] no [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Management Studio.  
  
-   Conectando-se ao [!INCLUDE[ssISversion2005](../../includes/ssisversion2005-md.md)] a partir do [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Management Studio.  
  
-   Gerenciando um serviço do [!INCLUDE[ssISversion2005](../../includes/ssisversion2005-md.md)] no [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Management Studio.  
  
-   Suporte para componentes personalizados do Integration Services de terceiros do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] , como executar e atualizar.  
  
## <a name="includesssql15-mdincludessssql15-mdmd-edition-upgrade"></a>[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Edition  
A tabela a seguir lista os cenários de atualização de edição com suporte no [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)].  
  
Para obter instruções passo a passo sobre como executar uma atualização de edição, veja [Atualizar para outra edição do SQL Server 2016 &#40;Instalação&#41;](../../database-engine/install-windows/upgrade-to-a-different-edition-of-sql-server-setup.md).  
  
|Atualização de|Atualização para|  
|------------------|----------------|  
|[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Enterprise (Licença Server+CAL e Baseada em Núcleo)**|[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Enterprise |  
|[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Evaluation Enterprise**|[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Enterprise (Licença Server+CAL ou Baseada em Núcleo) <br/><br/> [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Standard <br/> <br/> [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Developer <br/> <br/> [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Web <br/> <br/> A atualização da Evaluation (uma edição gratuita) para qualquer uma das edições pagas tem suporte em instalações autônomas, mas não tem suporte em instalações clusterizadas.|  
|[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Standard**|[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Enterprise (Licença Server+CAL ou Baseada em Núcleo)|  
|[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Developer**|[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Enterprise (Licença Server+CAL ou Baseada em Núcleo) <br/><br/> [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Web <br/> <br/> [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Standard|  
|[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Web|[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Enterprise (Licença Server+CAL ou Baseada em Núcleo) <br/><br/> [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Standard|  
|[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Express*|[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Enterprise (Licença Server+CAL ou Baseada em Núcleo) <br/><br/> [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Developer <br/> <br/> [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Standard <br/> <br/> [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Web|  
  
Além disso, você também pode executar uma atualização de edição entre o [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Enterprise (Licença Server+CAL) e [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Enterprise (Licença Baseada em Núcleo):  
  
|Atualização de edição do|Atualização de edição para|  
|--------------------------|------------------------|  
|[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Enterprise (Licença Server+CAL)**|[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Enterprise (Licença Baseada em Núcleo)|  
|[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Enterprise (Licença Baseada em Núcleo)|[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Enterprise (Licença Server+CAL)|  
  
 \* Também se aplica ao [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Express with Tools e ao [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Express with Advanced Services.  
  
 ** A alteração da edição de um cluster de failover do [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] é limitada. Os cenários a seguir não têm suporte para clusters de failover do [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] :  
  
-   [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Enterprise para [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Developer, Standard ou Evaluation.  
  
-   [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Developer para [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Standard ou Evaluation.  
  
-   [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Standard para [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Evaluation.  
  
-   [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Evaluation para [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Standard.  
  
## <a name="see-also"></a>Consulte Também  

[Edições e recursos com suporte do SQL Server 2016](../../sql-server/editions-and-supported-features-for-sql-server-2016.md)     
[Requisitos de hardware e software para a instalação do SQL Server 2016](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)     
[Atualizar para o SQL Server 2016](../../database-engine/install-windows/upgrade-sql-server.md)    
  
  
