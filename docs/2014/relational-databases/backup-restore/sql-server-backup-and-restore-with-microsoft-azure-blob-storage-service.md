---
title: SQL Server Backup e restauração com o serviço de armazenamento de BLOBs do Azure | Microsoft Docs
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
ms.openlocfilehash: 82220ab3649cb3af858e5a61e4c3ddfc5116d661
ms.sourcegitcommit: 3b1f873f02af8f4e89facc7b25f8993f535061c9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/30/2019
ms.locfileid: "70175807"
---
# <a name="sql-server-backup-and-restore-with-azure-blob-storage-service"></a>Backup e restauração do SQL Server no serviço de Armazenamento de Blobs
  Este tópico apresenta [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] backups e a restauração do [serviço de armazenamento de BLOBs do Azure](http://www.windowsazure.com/develop/net/how-to-guides/blob-storage/). Ele também fornece um resumo dos benefícios de usar o serviço blob do Azure para armazenar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] backups.  
  
 O SQL Server dá suporte ao armazenamento de backups para o serviço de armazenamento de BLOBs do Azure das seguintes maneiras:  
  
-   **Gerencie seus backups no Azure:** Usando os mesmos métodos usados para fazer backup em disco e fita, agora você pode fazer backup no armazenamento do Azure especificando a URL como o destino do backup.  Você pode usar esse recurso para fazer backup ou configurar manualmente sua própria estratégia de backup, como faria em um armazenamento local ou em outras opções fora do local. Esse recurso também é conhecido como **Backup do SQL Server para URL**. Para obter mais informações, consulte [SQL Server Backup to URL](sql-server-backup-to-url.md). Esse recurso está disponível no SQL Server 2012 SP1 CU2 ou posterior.  
  
    > [!NOTE]  
    >  Para SQL Server versões anteriores a SQL Server 2014, você pode usar o suplemento SQL Server a ferramenta backup para Azure para criar backups de modo rápido e fácil para o armazenamento do Azure. Para obter mais informações, consulte [centro de download](https://go.microsoft.com/fwlink/?LinkID=324399).  
  
-   **Permitir que SQL Server gerencie backups no Azure:** Configure SQL Server para gerenciar a estratégia de backup e agendar backups de um único banco de dados ou de vários bancos ou definir padrões no nível da instância. Esse recurso é conhecido como **[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]** . Para obter mais informações, consulte [SQL Server Backup gerenciado no Azure](sql-server-managed-backup-to-microsoft-azure.md). Esse recurso está disponível no SQL Server 2014 ou posterior.  
  
## <a name="benefits-of-using-the-azure-blob-service-for-includessnoversionincludesssnoversion-mdmd-backups"></a>Benefícios de usar o serviço blob do Azure para backups [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
-   Armazenamento externo flexível, confiável e ilimitado: armazenar seus backups no serviço blob do Azure pode ser uma opção conveniente, flexível e fácil de acessar fora do local. Criar o armazenamento externo para backups do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pode ser tão fácil quanto modificar scripts/trabalhos existentes. O armazenamento externo deve estar, normalmente, distante o suficiente do local do banco de dados de produção para evitar um único desastre que possa afetar os locais dos bancos de dados externo e de produção. Ao optar por replicar geograficamente o armazenamento de Blob, você terá uma camada adicional de proteção caso ocorra algum desastre que possa afetar a região inteira. Além disso, os backups estão disponíveis em qualquer lugar e a qualquer momento, e podem ser facilmente acessados para restaurações.  
  
-   Arquivo de backup: o serviço de armazenamento de BLOBs do Azure oferece uma alternativa melhor à opção de fita usada com frequência para arquivar backups. O armazenamento em fita pode exigir o transporte físico para uma instalação externa e medidas para proteger a mídia. Armazenar os backups no armazenamento de BLOBs do Azure fornece uma opção de arquivamento instantânea, altamente disponível e durável.  
  
-   Sem sobrecarga de gerenciamento de hardware: não há sobrecarga de gerenciamento de hardware com os serviços do Azure. Os serviços do Azure gerenciam o hardware e fornecem replicação geográfica para redundância e proteção contra falhas de hardware.  
  
-   Atualmente, para instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em execução em uma máquina virtual do Azure, o backup em serviços de armazenamento de BLOBs do Azure pode ser feito criando discos anexados. No entanto, há um limite para o número de discos que você pode anexar a uma máquina virtual do Azure. O limite é 16 discos para uma instância grande adicional, e menos que isso para instâncias menores. Ao habilitar um backup direto para o armazenamento de BLOBs do Azure, você pode ignorar o limite de 16 discos.  
  
     Além disso, o arquivo de backup que agora é armazenado no serviço de armazenamento de BLOBs do Azure está diretamente disponível para um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] local ou outro [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em execução em uma máquina virtual do Azure, sem a necessidade de anexar/desanexar o banco de dados ou baixar e anexar o VHD.  
  
-   Benefícios do custo: pague apenas pelo serviço utilizado. Pode ser tão econômico quanto uma opção de arquivamento externo e de backup. Consulte a seção [considerações de cobrança do Azure](#Billing) para obter mais informações e links.  
  
##  <a name="Billing"></a>Considerações sobre cobrança do Azure:  
 Entender os custos de armazenamento do Azure permite prever o custo de criação e armazenamento de backups no Azure.  
  
 A [calculadora de preços do Azure](https://go.microsoft.com/fwlink/?LinkId=277060) pode ajudar a estimar seus custos.  
  
 **Armazenamento:** os encargos baseiam-se no espaço usado, e são calculados em uma escala graduada e no nível de redundância. Para obter mais detalhes e informações atualizadas, confira a seção **Gerenciamento de dados** do artigo [Detalhes de preço](https://go.microsoft.com/fwlink/?LinkId=277059) .  
  
 **Transferências de dados:** As transferências de dados de entrada para o Azure são gratuitas. As transferências de saída são cobradas de acordo com o uso da largura de banda e calculadas com base em uma escala graduada específica de região. Para obter mais detalhes, consulte a seção [Transferências de dados](https://go.microsoft.com/fwlink/?LinkId=277061) do artigo Detalhes do preço.  
  
## <a name="see-also"></a>Consulte também  
 [Práticas recomendadas e solução de problemas de backup do SQL Server para URL](sql-server-backup-to-url-best-practices-and-troubleshooting.md)   
 [Fazer backup e restaurar bancos de dados do sistema &#40;SQL Server&#41;](back-up-and-restore-of-system-databases-sql-server.md)   
 [Tutorial: SQL Server Backup e restauração para o serviço de armazenamento de BLOBs do Azure](../tutorial-sql-server-backup-and-restore-to-azure-blob-storage-service.md)   
 [Backup do SQL Server para URL](sql-server-backup-to-url.md)  
  
  
