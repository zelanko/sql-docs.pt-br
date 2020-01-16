---
title: Backup e restauração com o Armazenamento de Blobs do Azure
ms.custom: seo-lt-2019
ms.date: 12/17/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
ms.assetid: 6a0c9b6a-cf71-4311-82f2-12c445f63935
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: ba2574b4468742414d60c1f4e7db4a93380fba0e
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/19/2019
ms.locfileid: "75251130"
---
# <a name="sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service"></a>Backup e restauração do SQL Server com o Serviço de Armazenamento de Blobs do Microsoft Azure
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  ![Fazer backup no gráfico de blob do Azure](../../relational-databases/backup-restore/media/backup-to-azure-blob-graphic.png "Fazer backup no gráfico de blob do Azure")  
  
 Este tópico descreve como fazer backups e restaurações do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no [serviço de armazenamento de Blobs do Microsoft Azure](https://www.windowsazure.com/develop/net/how-to-guides/blob-storage/). Ele também fornece um resumo dos benefícios do uso do Serviço Blob do Microsoft Azure para armazenar backups do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 O SQL Server dá suporte ao armazenamento de backups no serviço de armazenamento de Blobs do Microsoft Azure, das seguintes maneiras:  
  
-   **Gerencie seus backups para o Microsoft Azure:** Usando os mesmos métodos usados para fazer backup em DISCO e FITA, agora você pode fazer backup do armazenamento do Microsoft Azure especificando a URL como destino do backup. Você pode usar esse recurso para fazer backup ou configurar manualmente sua própria estratégia de backup, como faria em um armazenamento local ou em outras opções fora do local. Esse recurso também é conhecido como **Backup do SQL Server para URL**. Para saber mais, confira [SQL Server Backup to URL](../../relational-databases/backup-restore/sql-server-backup-to-url.md). Esse recurso está disponível no SQL Server 2012 SP1 CU2 ou posterior. Esse recurso foi aprimorado no [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] para fornecer melhor desempenho e funcionalidade com o uso de blobs de bloco, assinaturas de acesso compartilhado e distribuição.  
  
    > [!NOTE]  
    >  Para as versões do SQL Server anteriores ao SQL Server 2012 SP1 CU2, você pode usar o suplemento Ferramenta de Backup do SQL Server para o Microsoft Azure para criar backups no armazenamento do Microsoft Azure com rapidez e facilidade. Para obter mais informações, consulte [centro de download](https://go.microsoft.com/fwlink/?LinkID=324399).  
  
-   **Backups de instantâneo de arquivo de arquivos de banco de dados no Armazenamento de Blogs do Azure** Com o uso de instantâneos do Azure, os Backups de Instantâneo de Arquivo do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] fornecem backups e restaurações instantâneos de arquivos de banco de dados armazenados por meio do serviço de armazenamento de Blobs do Azure. Essa funcionalidade permite que você simplifique as políticas de backup e restauração, e dá suporte à recuperação pontual. Para obter mais informações, consulte [Backups de instantâneo de arquivo para arquivos de banco de dados no Azure](../../relational-databases/backup-restore/file-snapshot-backups-for-database-files-in-azure.md). Esse recurso está disponível no SQL Server 2016 ou posterior.  
  
-   **Deixe o SQL Server gerenciar backups para o Microsoft Azure:** Configure o SQL Server para gerenciar a estratégia de backup e agende backups para um banco de dados individual ou vários bancos de dados, ou defina valores padrão no nível da instância. Esse recurso é conhecido como **[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]** . Para obter mais informações, veja [Backup gerenciado do SQL Server no Microsoft Azure](../../relational-databases/backup-restore/sql-server-managed-backup-to-microsoft-azure.md). Esse recurso está disponível no SQL Server 2014 ou posterior.  
  
## <a name="benefits-of-using-the-microsoft-azure-blob-service-for-includessnoversionincludesssnoversion-mdmd-backups"></a>Benefícios do uso do serviço Blob do Microsoft Azure para backups do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
-   Armazenamento externo flexível, confiável e ilimitado: Armazenar os backups no serviço Blob do Microsoft Azure pode ser uma opção conveniente, flexível e de fácil acesso externo. Criar o armazenamento externo para backups do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pode ser tão fácil quanto modificar scripts/trabalhos existentes. O armazenamento externo deve estar, normalmente, distante o suficiente do local do banco de dados de produção para evitar um único desastre que possa afetar os locais dos bancos de dados externo e de produção. Ao optar por replicar geograficamente o armazenamento de Blob, você terá uma camada adicional de proteção caso ocorra algum desastre que possa afetar a região inteira. Além disso, os backups estão disponíveis em qualquer lugar e a qualquer momento, e podem ser facilmente acessados para restaurações.  
  
    > [!IMPORTANT]  
    >  Com o uso de blobs de bloco no [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)], você pode distribuir o conjunto de backup para dar suporte a arquivos de backup com tamanho de até 12,8 TB.  
  
-   Arquivo de backup: O serviço de armazenamento de Blob do Microsoft Azure oferece uma alternativa melhor para a opção de fita geralmente usada para arquivar backups. O armazenamento em fita pode exigir o transporte físico para uma instalação externa e medidas para proteger a mídia. O armazenamento dos backups no armazenamento de Blobs do Microsoft Azure oferece uma opção de arquivamento imediata, altamente disponível e durável.  
  
-   Sem sobrecarga de gerenciamento de hardware: não há sobrecarga de gerenciamento de hardware nos serviços do Microsoft Azure. Os serviços do Microsoft Azure gerenciam o hardware e fornecem replicação geográfica para redundância e proteção contra falhas de hardware.  
  
-   No momento, para instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] executadas em uma máquina virtual do Microsoft Azure, o backup para os serviços de armazenamento de Blobs do Microsoft Azure pode ser feito através da criação de discos anexados. No entanto, há um limite para o número de discos que você pode anexar à máquina virtual do Microsoft Azure. O limite é 16 discos para uma instância grande adicional, e menos que isso para instâncias menores. Ao habilitar um backup direto para o armazenamento de Blobs do Microsoft Azure, você pode ignorar o limite de 16 discos.  
  
     Além disso, o arquivo de backup que, agora, é armazenado no serviço de armazenamento de Blobs do Microsoft Azure está diretamente disponível para um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] local ou outro [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em execução em uma Máquina Virtual do Microsoft Azure, sem que seja necessário anexar/desanexar o banco de dados ou baixar e anexar o VHD.  
  
-   Benefícios de custo: pague apenas pelo serviço usado. Pode ser tão econômico quanto uma opção de arquivamento externo e de backup. Consulte a seção [Considerações sobre cobrança do Microsoft Azure](#Billing) para obter mais informações e links.  
  
##  <a name="Billing"></a> Considerações sobre cobrança do Microsoft Azure:  
 Compreender os custos de armazenamento do Microsoft Azure habilita você a fazer uma previsão do custo da criação e do armazenamento de backups no Microsoft Azure.  
  
 A [calculadora de preços do Microsoft Azure](https://go.microsoft.com/fwlink/?LinkId=277060) pode ajudar a estimar os custos.  
  
 **Armazenamento:** os encargos baseiam-se no espaço usado e são calculados em uma escala graduada e no nível de redundância. Para obter mais detalhes e informações atualizadas, confira a seção **Gerenciamento de dados** do artigo [Detalhes de preço](https://go.microsoft.com/fwlink/?LinkId=277059) .  
  
 **Transferências de dados:** as transferências de dados de entrada para o Microsoft Azure são gratuitas. As transferências de saída são cobradas de acordo com o uso da largura de banda e calculadas com base em uma escala graduada específica de região. Para obter mais detalhes, consulte a seção [Transferências de dados](https://go.microsoft.com/fwlink/?LinkId=277061) do artigo Detalhes do preço.  
  
## <a name="see-also"></a>Consulte Também  

[Solução de problemas e melhores práticas de backup do SQL Server para URL](../../relational-databases/backup-restore/sql-server-backup-to-url-best-practices-and-troubleshooting.md)   

[Fazer backup e restaurar bancos de dados do sistema &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-and-restore-of-system-databases-sql-server.md)   

[Tutorial: Como usar o serviço de Armazenamento de Blobs do Microsoft Azure com os bancos de dados do SQL Server 2016](../tutorial-use-azure-blob-storage-service-with-sql-server-2016.md)

[Backup do SQL Server para URL](../../relational-databases/backup-restore/sql-server-backup-to-url.md)  
  
  
