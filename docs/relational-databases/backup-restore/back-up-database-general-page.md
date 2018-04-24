---
title: Fazer backup do banco de dados (página Geral) | Microsoft Docs
ms.custom: ''
ms.date: 07/01/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: backup-restore
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-backup-restore
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql13.swb.backupdatabase.general.f1
ms.assetid: 5c344dfd-1ad3-41cc-98cd-732973b4a162
caps.latest.revision: 64
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: aaccb17dbf576074ac482092ae0ab4a2216f8ddd
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="back-up-database-general-page"></a>Backup do banco de dados (página Geral)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Use a página **Geral** da caixa de diálogo **Backup de Banco de Dados** para exibir ou modificar as configurações de uma operação de backup de banco de dados.  
  
 Para obter mais informações sobre os conceitos básicos de backup, veja [Visão geral de Backup &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-overview-sql-server.md).  
  
> [!NOTE]  
>  Ao especificar uma tarefa de backup usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], é possível gerar o script [!INCLUDE[tsql](../../includes/tsql-md.md)] [BACKUP](../../t-sql/statements/backup-transact-sql.md) correspondente clicando no botão **Script** e selecionando um destino para o script.  
  
 **Para usar o SQL Server Management Studio para criar um backup**  
  
-   [Criar um backup completo de banco de dados &#40;SQL Server&#41;](../../relational-databases/backup-restore/create-a-full-database-backup-sql-server.md)  
  
-   [Criar um backup diferencial de banco de dados &#40;SQL Server&#41;](../../relational-databases/backup-restore/create-a-differential-database-backup-sql-server.md)  
  
    > [!IMPORTANT]  
    >  Você pode definir um plano de manutenção de banco de dados para criar backups de banco de dados. Para obter mais informações, consulte [Planos de manutenção do banco de dados](http://msdn.microsoft.com/library/ms187658.aspx) nos Manuais Online do [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] .  
  
 **Para criar um backup parcial**  
  
-   Para obter um backup parcial, use a instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] [BACKUP](../../t-sql/statements/backup-transact-sql.md) com a opção PARTIAL.  
  
## <a name="options"></a>Opções  
  
### <a name="source"></a>Origem  
 As opções do painel **Origem** identificam o banco de dados e especificam o tipo de backup e o componente para a operação de backup.  
  
 **Backup de banco de dados**  
 Selecione o banco de dados do qual fazer backup.  
  
 **Modelo de recuperação**  
 Exiba o modelo de recuperação (SIMPLE, FULL ou BULK_LOGGED) exibido para o banco de dados selecionado.  
  
 **Tipo de backup**  
 Selecione o tipo de backup que você deseja executar no banco de dados especificado.  
  
|Tipo de backup|Disponível para|Restrictions|  
|-----------------|-------------------|------------------|  
|Completo|Bancos de dados, arquivos e grupos de arquivos|No banco de dados **mestre** , só backups completos são possíveis.<br /><br /> No Modelo de Recuperação Simples, backups de arquivos e grupos de arquivos estão disponíveis apenas para grupos de arquivos somente leitura.|  
|Diferencial|Bancos de dados, arquivos e grupos de arquivos|No Modelo de Recuperação Simples, backups de arquivos e grupos de arquivos estão disponíveis apenas para grupos de arquivos somente leitura.|  
|Log de Transações|Logs de transações|Os backups de log de transações não estão disponíveis no Modelo de Recuperação Simples.|  
  
 **Copiar Somente Backup**  
 Selecione para criar um backup somente cópia. Um *backup somente cópia* é um backup do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que não depende da sequência de backups convencionais do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obter mais informações, veja [Backups somente cópia &#40;SQL Server&#41;](../../relational-databases/backup-restore/copy-only-backups-sql-server.md).  
  
> [!NOTE]  
>  Quando a opção **Diferencial** está selecionada, você não pode criar um backup somente cópia.  
  
 **Componente de backup**  
 Selecione o componente de banco de dados do qual fazer backup. Se o **Log de Transações** estiver selecionado na lista de **Tipo de Backup** , essa opção não será ativada.  
  
 Selecione um destes botões de opção:  
  
|||  
|-|-|  
|**Backup de banco de dados**|Especifica que seja feito backup do banco de dados inteiro.|  
|**Arquivos e grupos de arquivos**|Especifica que seja feito backup dos arquivos e/ou grupos de arquivos especificados.<br /><br /> Selecione essa opção para abrir a caixa de diálogo **Selecionar Arquivos e Grupos de Arquivos** . Após selecionar os grupos de arquivos ou arquivos dos quais deseja fazer backup e clicar em **Ok**, suas seleções serão exibidas na caixa **Arquivos e grupos de arquivos** .|  
  
### <a name="destination"></a>Destino  
 As opções do painel **Destino** permitem especificar o tipo de dispositivo de backup para a operação de backup e encontrar um dispositivo de backup lógico ou físico existente.  
  
> [!NOTE]  
>  Para obter informações sobre os dispositivos de backup do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], veja [Dispositivos de backup &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-devices-sql-server.md).  
  
 **Fazer backup em**  
 Selecione um dos seguintes tipos de mídia em que fazer backup. Os destinos selecionados serão exibidos na lista **Fazer backup em** .  
  
|||  
|-|-|  
|**Disco**|Faz o backup em disco. Pode ser um arquivo de sistema ou um dispositivo de backup lógico baseado em disco criado para o banco de dados. Os discos atualmente selecionados são exibidos na lista **Backup em** . Você pode selecionar até 64 dispositivos de disco para a operação de backup.|  
|**Tape**|Faz o backup em fita. Pode ser uma unidade de fita local ou um dispositivo de backup lógico baseado em fita criado para o banco de dados. As fitas atualmente selecionadas são exibidas na lista **Backup em** . O número máximo é 64. Se não houver nenhum dispositivo de fita anexado ao servidor, essa opção será desativada. As fitas selecionadas são incluídas na lista **Backup em** .<br /><br /> Observação: o suporte para dispositivos de backup em fita será removido em uma versão futura do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam.|  
|**URL**|Faz backup no armazenamento de Blobs do Microsoft Azure.|  
  
 O próximo conjunto de opções exibido depende do tipo de destino selecionado. Se você selecionar Disco ou Fita, as opções a seguir são exibidas.  
  
 **Adicionar**  
 Adiciona um arquivo ou dispositivo à lista **Fazer backup em** . Você pode fazer backup em até 64 dispositivos simultaneamente em um disco local ou remoto. Para especificar um arquivo em um disco remoto, use o nome UNC totalmente qualificado. Para obter mais informações, consulte [Dispositivos de backup &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-devices-sql-server.md).  
 
 
  
 **Remover**  
 Remove um ou mais dispositivos atualmente selecionados na lista **Fazer backup em** .  
  
 **Sumário**  
Exibirá o conteúdo da mídia do dispositivo selecionado, se houver.  O botão não executa uma função quando uma **URL** é especificada. 
   
Caixa de diálogo**Selecionar Destino do Backup** A caixa de diálogo **Selecionar Destino do Backup** é exibida depois de selecionar **Adicionar**.   O conjunto de opções exibido depende do tipo de destino selecionado. 

Se você selecionou **Disco** ou **Fita** como destino de backup, a opção a seguir é exibida.  

*
  **Nome do Arquivo**  
    Especifique o nome do arquivo de backup.

Se você selecionou **URL** como destino de backup, as seguintes opções são exibidas:
*
  **Contêiner de armazenamento do Azure**  
  O nome do contêiner de armazenamento do Microsoft Azure no qual os arquivos de backup serão armazenados. 
   
*
  **Política de Acesso Compartilhado:**  
  Insira a assinatura de acesso compartilhado de um contêiner inserido manualmente.  Este campo não estará disponível se um contêiner existente tiver sido escolhido.
  
*
  **Arquivo de Backup:**  
  Nome do arquivo de backup.

*
  **Novo Contêiner:**  
Usado para registrar um contêiner existente para o qual não existe uma assinatura de acesso compartilhado.  Consulte [Connect to a Microsoft Azure Subscription](../../relational-databases/backup-restore/connect-to-a-microsoft-azure-subscription.md)(Conectar-se a uma assinatura do Microsoft Azure).
  
## <a name="see-also"></a>Consulte Também  
 [Fazer backup de um log de transações &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-a-transaction-log-sql-server.md)   
 [Fazer backup de arquivos e de grupos de arquivos &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-files-and-filegroups-sql-server.md)   
 [Definir um dispositivo de backup lógico para um arquivo de disco &#40;SQL Server&#41;](../../relational-databases/backup-restore/define-a-logical-backup-device-for-a-disk-file-sql-server.md)   
 [Definir um dispositivo de backup lógico para uma unidade de fita &#40;SQL Server&#41;](../../relational-databases/backup-restore/define-a-logical-backup-device-for-a-tape-drive-sql-server.md)   
 [Modelos de recuperação &#40;SQL Server&#41;](../../relational-databases/backup-restore/recovery-models-sql-server.md)  
  
  
