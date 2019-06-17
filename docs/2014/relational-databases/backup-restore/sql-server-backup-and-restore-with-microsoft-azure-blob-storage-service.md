---
title: Serviço de armazenamento de BLOBs do SQL Server Backup e restauração com o Windows Azure | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
ms.assetid: 6a0c9b6a-cf71-4311-82f2-12c445f63935
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 52f1bdf9e748625e1310210c98beeb4401a5dd81
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62920691"
---
# <a name="sql-server-backup-and-restore-with-windows-azure-blob-storage-service"></a>Backup e restauração do SQL Server com o serviço de armazenamento de Blob do Windows Azure
  Este tópico apresenta [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] backups e restaurações do [serviço de armazenamento de Blob do Windows Azure](http://www.windowsazure.com/develop/net/how-to-guides/blob-storage/). Ele fornece também um resumo dos benefícios do uso do serviço de Blob do Windows Azure para armazenar backups do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 O SQL Server oferece suporte ao armazenamento de backups no serviço de armazenamento de Blob do Windows Azure da seguinte maneira:  
  
-   **Gerencie seus backups para o Windows Azure:** Usando os mesmos métodos usados para fazer backup em disco e fita, você pode agora fazer backup no armazenamento do Windows Azure especificando a URL como destino de backup.  Você pode usar esse recurso para fazer backup ou configurar manualmente sua própria estratégia de backup, como faria em um armazenamento local ou em outras opções fora do local. Esse recurso também é conhecido como **Backup do SQL Server para URL**. Para obter mais informações, consulte [SQL Server Backup to URL](sql-server-backup-to-url.md). Esse recurso está disponível no SQL Server 2012 SP1 CU2 ou posterior.  
  
    > [!NOTE]  
    >  Para as versões do SQL Server anteriores ao SQL Server 2014, você pode usar o suplemento SQL Server Backup to Windows Azure Tool para criar backups no armazenamento do Windows Azure com rapidez e facilidade. Para obter mais informações, consulte [centro de download](https://go.microsoft.com/fwlink/?LinkID=324399).  
  
-   **Deixe o SQL Server gerenciar os backups para o Windows Azure:** Configure o SQL Server para gerenciar os backups de estratégia e agendamento de backup para um banco de dados único ou vários bancos de dados, ou defina valores padrão no nível da instância. Esse recurso é conhecido como **[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]** . Para obter mais informações, consulte [SQL Server Managed Backup to Windows Azure](sql-server-managed-backup-to-microsoft-azure.md). Esse recurso está disponível no SQL Server 2014 ou posterior.  
  
## <a name="benefits-of-using-the-windows-azure-blob-service-for-includessnoversionincludesssnoversion-mdmd-backups"></a>Benefícios do uso do serviço de Blob do Windows Azure para backups do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
-   Armazenamento de externo flexível, confiável e ilimitado: Armazenar os backups no serviço de Blob do Windows Azure pode ser um conveniente, flexível e fácil de acessar a opção fora do site. Criar o armazenamento externo para backups do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pode ser tão fácil quanto modificar scripts/trabalhos existentes. O armazenamento externo deve estar, normalmente, distante o suficiente do local do banco de dados de produção para evitar um único desastre que possa afetar os locais dos bancos de dados externo e de produção. Ao optar por replicar geograficamente o armazenamento de Blob, você terá uma camada adicional de proteção caso ocorra algum desastre que possa afetar a região inteira. Além disso, os backups estão disponíveis em qualquer lugar e a qualquer momento, e podem ser facilmente acessados para restaurações.  
  
-   Arquivamento do backup: O serviço de armazenamento de Blob do Windows Azure oferece uma alternativa melhor para a opção de fita geralmente usada para arquivar backups. O armazenamento em fita pode exigir o transporte físico para uma instalação externa e medidas para proteger a mídia. O armazenamento dos backups no armazenamento de Blob do Windows Azure oferece uma opção de arquivamento imediata, altamente disponível e durável.  
  
-   Sem sobrecarga de gerenciamento de hardware: não há sobrecarga de gerenciamento de hardware nos serviços do Windows Azure. Os serviços do Windows Azure gerenciam o hardware e fornecem replicação geográfica para redundância e proteção contra falhas de hardware.  
  
-   No momento, para instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] executadas em uma máquina virtual do Windows Azure, o backup para os serviços de armazenamento de Blob do Windows Azure pode ser feito através da criação de discos conectados. No entanto, há um limite para o número de discos que você pode anexar à máquina virtual do Windows Azure. O limite é 16 discos para uma instância grande adicional, e menos que isso para instâncias menores. Ao habilitar um backup direto para o armazenamento de Blob do Windows Azure, você poderá ignorar o limite de 16 discos.  
  
     Além disso, o arquivo de backup que, agora, é armazenado no serviço de armazenamento de Blob do Windows Azure está diretamente disponível para um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no local ou outro [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em execução em uma máquina virtual do Windows Azure, sem que seja necessário anexar/desanexar o banco de dados ou baixar e anexar o VHD.  
  
-   Benefícios de custo: Pague apenas o serviço que é usado. Pode ser tão econômico quanto uma opção de arquivamento externo e de backup. Consulte a [considerações sobre cobrança do Azure Windows](#Billing) seção para obter mais informações e links.  
  
##  <a name="Billing"></a> Cobrança do Windows Azure considerações:  
 Se você compreender os custos de armazenamento do Windows Azure, conseguirá fazer uma previsão do custo da criação e do armazenamento de backups no Windows Azure.  
  
 O [Calculadora de preços do Windows Azure](https://go.microsoft.com/fwlink/?LinkId=277060) pode ajudar a estimar os custos.  
  
 **Armazenamento:** Os encargos baseiam-se no espaço usado e são calculados em uma escala graduada e no nível de redundância. Para obter mais detalhes e informações atualizadas, confira a seção **Gerenciamento de dados** do artigo [Detalhes de preço](https://go.microsoft.com/fwlink/?LinkId=277059) .  
  
 **Transferências de dados:** Transferências de dados de entrada para o Windows Azure são gratuitas. As transferências de saída são cobradas de acordo com o uso da largura de banda e calculadas com base em uma escala graduada específica de região. Para obter mais detalhes, consulte a seção [Transferências de dados](https://go.microsoft.com/fwlink/?LinkId=277061) do artigo Detalhes do preço.  
  
## <a name="see-also"></a>Consulte também  
 [Práticas recomendadas e solução de problemas de backup do SQL Server para URL](sql-server-backup-to-url-best-practices-and-troubleshooting.md)   
 [Fazer backup e restaurar bancos de dados do sistema &#40;SQL Server&#41;](back-up-and-restore-of-system-databases-sql-server.md)   
 [Tutorial: SQL Server Backup e restauração para o serviço de armazenamento de BLOBs do Azure do Windows](../tutorial-sql-server-backup-and-restore-to-azure-blob-storage-service.md)   
 [Backup do SQL Server para URL](sql-server-backup-to-url.md)  
  
  
