---
title: Upgrades de versão e edição com suporte | Microsoft Docs
ms.custom: ''
ms.date: 10/26/2015
ms.prod: sql-server-2014
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
manager: craigg
ms.openlocfilehash: 4a245aab71292e1482bd5a17bd32a27bded640ab
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62775212"
---
# <a name="supported-version-and-edition-upgrades"></a>Atualizações de versão e edição com suporte
  Você pode atualizar do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]e [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]e [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]. Este tópico lista os caminhos de atualização com suporte dessas versões do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e as atualizações de edição com suporte para o [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)].  
  
## <a name="pre-upgrade-checklist"></a>Lista de verificação anterior à atualização  
  
-   Antes de atualizar de uma edição do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] para outra, verifique se há suporte à funcionalidade usada no momento na edição que você utilizará.  
  
-   Antes de atualizar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], habilite a Autenticação do Windows para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent e verifique a configuração padrão: se a conta de serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent é membro do grupo sysadmin do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   Para atualizar para o [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)], você deverá estar executando um sistema operacional com suporte. Para obter mais informações, consulte [Hardware and Software Requirements for Installing SQL Server 2014](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md).  
  
-   A atualização será bloqueada se houver uma reinicialização pendente.  
  
-   A atualização será bloqueada, se o serviço do Windows Installer não estiver sendo executado.  
  
## <a name="unsupported-scenarios"></a>Cenários com suporte  
  
-   Não há suporte a instâncias de várias versões do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]. Os números de versão dos componentes do [!INCLUDE[ssDE](../../includes/ssde-md.md)], [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]e do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] devem ser os mesmos em uma instância do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
-   A atualização de plataforma cruzada não é suportada. Não é possível atualizar uma instância de 32 bits do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para uma nativa de 64 bits usando a Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . No entanto, será possível fazer backup de bancos de dados ou desanexá-los de uma instância de 32 bits do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]e, em seguida, restaurá-los ou anexá-los a uma nova instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (de 64 bits), se os bancos de dados não forem publicados na replicação. Você deverá recriar logons e outros objetos de usuário nos bancos de dados do sistema master, msdb e model.  
  
-   Não é possível adicionar novos recursos durante a atualização da instância existente do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Depois de atualizar uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], você poderá adicionar recursos usando a Instalação do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Para obter mais informações, consulte [adicionar recursos a uma instância do SQL Server 2014 &#40;instalação&#41;](add-features-to-an-instance-of-sql-server-setup.md).  
  
-   Não há suporte para clusters de failover no modo WOW.  
  
-   Não há suporte para a atualização de uma edição de Avaliação de uma versão anterior do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="upgrades-from-earlier-versions-to-includesssql14includessssql14-mdmd"></a>Atualizações de versões anteriores para o [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]  
  
> [!NOTE]  
>  O suporte para [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] é descrito com mais detalhes na próxima seção, 'suporte do[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] para [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]'.  
  
-   As edições de 32 bits do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] podem ser atualizadas para o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] no subsistema de 32 bits (WOW64) de um servidor de 64 bits.  
  
-   As versões de 64 bits do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] podem ser atualizadas para o servidor de 64 bits do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] somente.  
  
> [!NOTE]  
>  Quando você atualiza [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] de uma versão anterior do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Enterprise edition, escolha entre Enterprise Edition: Licenciamento baseado em núcleo e Enterprise Edition. Estas edições Enterprise só diferem com relação aos modos de licenciamento e o número máximo de núcleos com suporte. Para saber mais, confira [Compute Capacity Limits by Edition of SQL Server](../../sql-server/compute-capacity-limits-by-edition-of-sql-server.md).  
  
 O [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] dá suporte à atualização das seguintes versões do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  
  
-   [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] SP4 ou posterior  
  
-   [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] SP3 ou posterior  
  
-   [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] SP2 ou posterior  
  
-   [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP1 ou posterior  
  
 A tabela a seguir lista os cenários de atualização com suporte de versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para o [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)].  
  
|Atualização de|Caminho de atualização suportado|  
|------------------|----------------------------|  
|[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] SP4 Enterprise|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Business Intelligence|  
|[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] SP4 Developer|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Developer|  
|[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] SP4 Standard|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Business Intelligence<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Standard|  
|[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] SP4 Workgroup|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Business Intelligence<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Standard|  
|[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] SP4 Express,<br /><br /> [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] SP4 Express with Tools e<br /><br /> [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] SP4 Express with Advanced Services|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Business Intelligence<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Standard<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Web<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Express|  
|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] SP3 Enterprise|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Business Intelligence|  
|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] SP3 Developer|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Developer|  
|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] SP3 Standard|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Business Intelligence<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Standard|  
|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] SP3 Small Business|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Standard|  
|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] SP3 Web|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Business Intelligence<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Standard<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Web|  
|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] SP3 Workgroup|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Business Intelligence<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Standard|  
|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] SP3 Express,<br /><br /> [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] SP3 Express with Tools e<br /><br /> [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] SP3 Express with Advanced Services|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Business Intelligence<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Standard<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Web<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Express|  
|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] SP2 Datacenter|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Business Intelligence|  
|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] SP2 Enterprise|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Business Intelligence|  
|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] SP2 Developer|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Developer|  
|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] SP2 Small Business|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Standard|  
|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] SP2 Standard|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Business Intelligence<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Standard|  
|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] SP2 Web|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Business Intelligence<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Standard<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Web|  
|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] SP2 Workgroup|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Business Intelligence<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Standard|  
|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] SP2 Express,<br /><br /> [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] SP2 Express with Tools e<br /><br /> [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] SP2 Express with Advanced Services|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Business Intelligence<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Standard<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Web<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Express|  
|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP1 Enterprise|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Business Intelligence|  
|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP1 Developer|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Developer|  
|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP1 Standard|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Business Intelligence<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Standard|  
|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP1 Web|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Business Intelligence<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Standard<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Web|  
|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP1 Express,<br /><br /> [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP1 Express with Tools e<br /><br /> [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP1 Express Management Studio, e<br /><br /> [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP1 Express with Advanced Services|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Business Intelligence<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Standard<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Web<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Express|  
|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP1 Business Intelligence|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Business Intelligence|  
  
### <a name="includesssql14includessssql14-mdmd-support-for-includessversion2005includesssversion2005-mdmd"></a>[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]Suporte para [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]  
 Esta seção aborda o suporte do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] para [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]. No [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)], você poderá fazer o seguinte:  
  
-   Atualizar uma instância do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] do mecanismo de banco de dados para [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] executando a instalação do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] usando o assistente de instalação ou no prompt de comando.  
  
-   Anexar um banco de dados do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] (arquivos mdf/ldf) à instância do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] do mecanismo de banco de dados.  
  
-   Restaurar um banco de dados do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] para a instância do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] do mecanismo de banco de dados de um backup.  
  
-   Atualizar um pacote do [!INCLUDE[ssISversion2005](../../includes/ssisversion2005-md.md)] para o [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]. Executar pacotes com atualizações automáticas locais.  
  
-   Atualizar o [!INCLUDE[ssASversion2005](../../includes/ssasversion2005-md.md)] para [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] executando a instalação do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] .  
  
-   Fazer backup de um cubo do [!INCLUDE[ssASversion2005](../../includes/ssasversion2005-md.md)] e restaurar no [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)].  
  
-   Atualizar o [!INCLUDE[ssRSversion2005](../../includes/ssrsversion2005-md.md)] para [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] executando a instalação do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] .  
  
-   Conecte-se ao [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]usando o [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 2014.  
  
 Quando um banco de dados do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] é atualizado para [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)], o nível de compatibilidade do banco de dados é alterado de 90 para 100. (No [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)], os valores válidos para o nível de compatibilidade do banco de dados são 100, 110 e 120.) [ALTER DATABASE Compatibility Level &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql-compatibility-level) aborda como a alteração do nível de compatibilidade pode afetar os aplicativos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Os cenários não especificados na lista anterior não são suportados, incluindo, mas sem estar limitado, os seguintes:  
  
-   Instalando o [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] e [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] no mesmo computador (lado a lado).  
  
-   Usando uma instância do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] como um membro da topologia de replicação que envolve uma instância do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)].  
  
-   Configurando o espelhamento de banco de dados entre as instâncias do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] .  
  
-   Fazendo backup do registro de transações com envio de logs entre as instâncias do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] .  
  
-   Configurando servidores vinculados entre as instâncias do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] .  
  
-   Gerenciando uma instância do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] no [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Management Studio.  
  
-   Anexando um cubo do [!INCLUDE[ssASversion2005](../../includes/ssasversion2005-md.md)] no [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Management Studio.  
  
-   Conectando-se ao [!INCLUDE[ssISversion2005](../../includes/ssisversion2005-md.md)] a partir do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Management Studio.  
  
-   Gerenciando um serviço do [!INCLUDE[ssISversion2005](../../includes/ssisversion2005-md.md)] no [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Management Studio.  
  
-   Suporte para componentes personalizados do Integration Services de terceiros do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] , como executar e atualizar.  
  
## <a name="includesssql14includessssql14-mdmd-edition-upgrade"></a>[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Edition  
 A tabela a seguir lista os cenários de atualização de edição com suporte no [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)].  
  
 Para obter instruções passo a passo sobre como executar uma atualização de edição, consulte [atualizar para uma edição diferente do SQL Server 2014 &#40;instalação&#41;](upgrade-to-a-different-edition-of-sql-server-setup.md).  
  
|Atualização de|Atualização para|  
|------------------|----------------|  
|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise (Server + CAL e núcleo) <sup>2</sup>|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Business Intelligence|  
|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Business Intelligence|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise (Licença Server+CAL ou Baseada em Núcleo)|  
|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Evaluation Enterprise <sup>2</sup>|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise (Licença Server+CAL ou Baseada em Núcleo)<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Business Intelligence<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Standard<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Developer<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Web<br /><br /> A atualização da Evaluation Enterprise (uma edição gratuita) para qualquer uma das edições pagas é suportada para instalações autônomas, mas não é suportada para instalações clusterizadas.|  
|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Padrão <sup>2</sup>|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Business Intelligence<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise (Licença Server+CAL ou Baseada em Núcleo)|  
|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Desenvolvedor <sup>2</sup>|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise (Licença Server+CAL ou Baseada em Núcleo)<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Business Intelligence<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Web<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Standard|  
|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Web|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise (Licença Server+CAL ou Baseada em Núcleo)<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Business Intelligence<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Standard|  
|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Express <sup>1</sup>|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise (Licença Server+CAL ou Baseada em Núcleo)<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Business Intelligence<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Developer<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Standard<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Web|  
  
 Além disso, você também pode executar uma atualização de edição entre o [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise (Licença Server+CAL) e [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise (Licença Baseada em Núcleo):  
  
|Atualização de edição do|Atualização de edição para|  
|--------------------------|------------------------|  
|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise (licença Server + CAL) <sup>2</sup>|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise (Licença Baseada em Núcleo)|  
|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise (Licença Baseada em Núcleo)|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise (Licença Server+CAL)|  
  
 <sup>1</sup> também se aplica às [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Express with Tools e [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Express with Advanced Services.  
  
 <sup>2</sup> a alteração da edição de um [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] cluster de failover é limitada. Os cenários a seguir não têm suporte para clusters de failover do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] :  
  
-   SQL Server 2014 Enterprise para SQL Server 2014 Developer, Standard ou Enterprise Evaluation.  
  
-   SQL Server 2014 Developer para SQL Server 2014 Standard ou Enterprise Evaluation.  
  
-   SQL Server 2014 Standard para SQL Server 2014 Enterprise Evaluation.  
  
-   SQL Server 2014 Enterprise Evaluation para SQL Server 2014 Standard.  
  
## <a name="see-also"></a>Consulte também  
 [Recursos com suporte nas edições do SQL Server 2014](../../../2014/getting-started/features-supported-by-the-editions-of-sql-server-2014.md)   
 [Requisitos de hardware e Software para instalação do SQL Server 2014](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)   
 [Atualizar para o SQL Server 2014](upgrade-sql-server.md)   
 [Usar o Supervisor de Atualização para preparar para atualizações](../../../2014/sql-server/install/use-upgrade-advisor-to-prepare-for-upgrades.md)  
  
  
