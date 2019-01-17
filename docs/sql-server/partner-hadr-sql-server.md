---
title: Parceiros de alta disponibilidade e recuperação de desastre do SQL Server | Microsoft Docs
description: Lista de parceiros terceirizados com soluções para monitorar o servidor.
services: sql-server
ms.topic: conceptual
ms.custom: ''
ms.date: 09/17/2017
ms.prod: sql
ms.author: mikeray
author: MikeRayMSFT
manager: craigg
ms.openlocfilehash: 1849328d008a6b995d2242a1e00aa9c0040e8d05
ms.sourcegitcommit: 0bb306da5374d726b1e681cd4b5459cb50d4a87a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2018
ms.locfileid: "53732043"
---
# <a name="sql-server-high-availability-and-disaster-recovery-partners"></a>Parceiros de alta disponibilidade e recuperação de desastre do SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
Para fornecer alta disponibilidade e recuperação de desastres para seus serviços do SQL Server, escolha entre as várias ferramentas do setor.  Este artigo destaca empresas parceiras da Microsoft com soluções de recuperação de desastres e disponibilidade alta com suporte ao Microsoft SQL Server.

## <a name="high-availability-and-disaster-recovery-partners"></a>Parceiros de alta disponibilidade e recuperação de desastre
<!--|![PartnerShortName][1] |**PartnerShortName**<br>PartnerShortName Brief description of the type of products that partner provides. <br><br>List of supported versions of SQL Server, OS, OS platforms/distros  Server 2005 SP4 - SQL Server 2016 on Windows |[Datasheet][PartnerShortName_datasheet]<br>[Marketplace][PartnerShortName_marketplace]<br>[Website][PartnerShortName_website]<br>[Twitter][PartnerShortName_twitter]<br>[Video][PartnerShortName_youtube]|[![veem_video](./media/partner-hadr-sql-server/PartnerShortName_video.png)](https://www.youtube.com/channel/**************)
-->

| Partner (parceiro) | Descrição | Links | 
| --- | --- | --- |
|![Azure][5] |**Azure Site Recovery**<br>Site Recovery replica as cargas de trabalho em execução em servidores físicos ou máquinas virtuais para que permaneçam disponíveis em um local secundário se o site primário não estiver disponível. Você pode duplicar e realizar failover das máquinas virtuais do SQL Server do data center local para o Azure ou para outro data center local ou de um dos data centers do Azure para outro data center do Azure.<br><br> Edições Enterprise e Standard do SQL Server 2008 R2- SQL Server 2016|[Site][azure_website]<br>[Marketplace][azure_marketplace]<br>[Folha de dados][azure_datasheet]<br>[Twitter][azure_twitter]<br>[Vídeo][azure_youtube]|
|![DH2i][2] |**DH2i**<br>DxEnterprise é software de Disponibilidade Inteligente para Windows, Linux e Docker que ajuda você a alcançar o tempo de inatividade planejado ou não planejado praticamente nulo, permite grande economia nos custos, simplifica drasticamente o gerenciamento e permite uma consolidação física e lógica.<br><br>SQL Server 2005+, Windows Server 2008R2+, Ubuntu 16+, RHEL 7+, CentOS 7+|[Site][dh2i_website]<br>[Folha de dados][dh2i_datasheet]<br>[Twitter][dh2i_twitter]<br>[Vídeo][dh2i_youtube]|
|![HPE][4] |**HPE Serviceguard**<br>Proteja suas cargas críticas de trabalho do SQL Server 2017 no Linux®, de tempo de inatividade planejado ou não até uma grande quantidade de falhas de infraestrutura e de aplicativos em ambientes físicos e virtuais, em qualquer distância, com o HPE Serviceguard para Linux (SGLX). O HPE SGLX A.12.20.00 e posterior oferece opções de monitoramento e recuperação sensíveis ao contexto para a Instância de Cluster de Failover e as cargas de trabalho dos Grupos de Disponibilidade Always On do SQL Server. Maximize o tempo de atividade com HPE SGLX sem comprometer a integridade de dados e o desempenho.<br><br>SQL Server 2017 no Linux – RedHat 7.3, 7.4, SUSE 12 SP2, SP3|[Site][hpe_website]<br>[Folha de dados][hpe]<br>[Baixar a avaliação][hpe_download]<br>[Blog][hpe_download]<br>[Twitter][hpe_twitter]
|![IDERA][3]|**IDERA**<br>SQL Safe Backup é uma solução de backup e recuperação de alto desempenho para o SQL Server que economiza dinheiro, reduz o tempo de backup do banco de dados e o tamanho do arquivo de backup, além de fornecer acesso instantâneo a leitura e gravação para bancos de dados em arquivos de backup.<br><br>Microsoft SQL Server: 2005 SP1 ou posterior, 2008, 2008 R2, 2012, 2014, 2016; todas as edições |[Site][idera_website]|
|![NEC][7]|**NEC**<br>O ExpressCluster é uma solução abrangente e totalmente automatizada de alta disponibilidade e recuperação de desastres para todas as falhas principais, incluindo falhas de hardware, software, rede e site para o SQL Server e para aplicativos associados em execução em máquinas virtuais ou físicas locais ou em ambientes de nuvem.<br><br>Microsoft SQL Server: 2005 ou posterior; todas as edições |[Site][necec_website]<br>[Folha de dados][necec_datasheet]<br>[Vídeo][necec_youtube]<br>[Download][necec_download]|
|![Portworx][6] |**Portworx**<br>Portworx é a solução para contêineres com monitoramento de estado em execução na produção. Com Portworx, os usuários podem gerenciar qualquer banco de dados ou o serviço de monitoramento de estado em qualquer infraestrutura usando qualquer agendador de contêiner, incluindo Kubernetes, Mesosphere DC/OS e Docker Swarm. Portworx resolve as cinco ocorrências mais comuns que as equipes de DevOps encontram ao executar bancos de dados em contêineres e outros serviços com monitoramento de estado na produção: persistência, alta disponibilidade, automação de data, suporte para vários repositórios de dados e infraestrutura, e a segurança.<br><br>SQL Server 2017 no Docker |[Site][portworx_website]<br>[Documentação][portworx_docs]<br>[Vídeo][portworx_youtube]|
|![SIOS][8] |**SIOS**<br>A tecnologia SIOS oferece soluções econômicas de alta disponibilidade e recuperação de desastres para o SQL Server no Windows ou no Linux. O clustering SIOS SANless elimina a necessidade de uma SAN de armazenamento compartilhado, oferecendo total flexibilidade para proteger os aplicativos mais importantes em configurações de nuvem híbrida, nuvem, virtual e física em ambientes de sites exclusivos ou múltiplos.<br><br>Adicione o SIOS DataKeeper ao ambiente de clustering de failover do Windows Server para criar um recurso de volume SANless que substitua o armazenamento compartilhado tradicional, facilitando a execução do WSFC no Azure.<br><br>A SIOS Protection Suite é uma solução de clustering totalmente flexível que protege aplicativos críticos do Linux, como SQL Server, SAP, HANA, Oracle e muitos outros.|[Site][sios_website]<br>[Folha de dados][sios_datasheet]<br>[Twitter][sios_twitter]<br>[Marketplace][sios_marketplace]<br>[Vídeo][sios_youtube]|
|![Veeam][1] |**Veeam**<br>Veeam Backup & Replication é uma solução de backup e disponibilidade avançada, fácil de usar e acessível. Ela fornece recuperação de dados e aplicações de forma rápida, flexível e confiável, reunindo backup de VM (máquina virtual) e replicação em uma solução única de software e aplicativos virtualizados. Veeam Backup & Replication oferece suporte premiada para os ambientes virtuais de VMware vSphere e Microsoft Hyper-V.<br><br>SQL Server 2005 SP4 – SQL Server 2016 no Windows |[Site][veeam_website]<br>[Folha de dados][veeam_datasheet]<br>[Twitter][veeam_twitter]<br>[Vídeo][veeam_youtube]|

## <a name="next-steps"></a>Próximas etapas
Para saber mais sobre outros parceiros, confira [monitoramento][mon_partners], [parceiros de gerenciamento][management_partners] e [parceiros de desenvolvimento][dev_partners].

<!--Image references-->
[1]: ./media/partner-hadr-sql-server/Veeam_green_logo.png
[2]: ./media/partner-hadr-sql-server/dh2i_logo.png
[3]: ./media/partner-hadr-sql-server/idera_logo.png
[4]: ./media/partner-hadr-sql-server/hpe_pri_grn_pos_rgb.png
[5]: ./media/partner-hadr-sql-server/azure_logo.png
[6]: ./media/partner-hadr-sql-server/portworx_logo.png
[7]: ./media/partner-hadr-sql-server/nec_logo.png
[8]: ./media/partner-hadr-sql-server/sios_logo.png

<!--Article links-->
[mon_partners]: ./partner-monitor-sql-server.md
[management_partners]: ./partner-management-sql-server.md
[dev_partners]: ./partner-dev-sql-server.md

<!--Website links -->
[veeam_website]:https://www.veeam.com/
[dh2i_website]:https://dh2i.com
[idera_website]:https://www.idera.com/productssolutions/sqlserver
[hpe_website]: https://www.hpe.com/us/en/product-catalog/detail/pip.376220.html
[azure_website]: https://docs.microsoft.com/azure/site-recovery/site-recovery-sql
[necec_website]: https://www.necam.com/ExpressCluster/
[portworx_website]: https://portworx.com/
[sios_website]: https://us.sios.com/

<!--Get Started Links-->

<!--Datasheet Links-->
[veeam_datasheet]:https://www.veeam.com/veeam_backup_9_5_datasheet_en_ds.pdf
[dh2i_datasheet]:https://dh2i.com/wp-content/uploads/DxE-Win-QuickFacts.pdf
[hpe]:https://www.hpe.com/h20195/v2/default.aspx?cc=us&lc=en&oid=376220
[necec_datasheet]: https://www.necam.com/docs/?id=0d9ef7a7-f935-4909-b6bb-20a47b3
[azure_datasheet]: https://docs.microsoft.com/azure/site-recovery/site-recovery-sql#site-recovery-support
[sios_datasheet]: https://us.sios.com/solutions/high-availability-cluster-software-cloud/

<!--Marketplace Links -->
[azure_marketplace]: https://azuremarketplace.microsoft.com/marketplace/apps?search=site%20recovery&page=1
[sios_marketplace]: https://azuremarketplace.microsoft.com/marketplace/apps/sios_datakeeper.sios-datakeeper-8
<!--Press links-->
<!--[veeam_press]:-->

<!--YouTube links-->
[veeam_youtube]:https://www.youtube.com/user/YouVeeam
[dh2i_youtube]:https://www.youtube.com/user/dh2icompany 
[idera_youtube]:https://www.idera.com/resourcecentral/videos/sql-safe-overview
[azure_youtube]: https://mva.microsoft.com/en-US/training-courses/is-your-lack-of-a-disaster-recovery-site-keeping-you-up-at-night-8680?l=oF7YrFH1_7504984382
[necec_youtube]: https://www.youtube.com/watch?v=9La3Cw1Q1Jk
[portworx_youtube]: https://www.youtube.com/channel/UCSexpvQ9esSRgiS_Q9_3mLQ 
[sios_youtube]: https://www.youtube.com/watch?v=U3M44gJNWQE

<!--Twitter links-->
[veeam_twitter]:https://twitter.com/veeam
[dh2i_twitter]:https://twitter.com/dh2i
[hpe_twitter]:https://twitter.com/hpe
[azure_twitter]:https://twitter.com/hashtag/azuresiterecovery
[sios_twitter]:https://www.twitter.com/SIOSTech

<!--Docs links>-->
[portworx_docs]: https://docs.portworx.com/

<!--Download links-->
[hpe_download]: https://h20392.www2.hpe.com/portal/swdepot/displayProductInfo.do?productNumber=SGLX-DEMO
[necec_download]: https://www.necam.com/ExpressCluster/30daytrial/
<!--Blog links-->
[hpe_blog]: https://community.hpe.com/t5/Servers-The-Right-Compute/SQL-Server-for-Linux-Is-Here-and-A-New-Chapter-for-Mission/ba-p/6977571#.WiHWW0xFwUE
