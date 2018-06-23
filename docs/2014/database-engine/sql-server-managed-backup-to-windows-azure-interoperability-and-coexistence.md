---
title: 'SQL Server Backup gerenciado para Windows Azure: interoperabilidade e coexistência | Microsoft Docs'
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-backup-restore
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 78fb78ed-653f-45fe-a02a-a66519bfee1b
caps.latest.revision: 15
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 4da5bf7083be26f12a140bf5b3465882e150b215
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36011212"
---
# <a name="sql-server-managed-backup-to-windows-azure-interoperability-and-coexistence"></a>Backup Gerenciado do SQL Server para o Windows Azure: Interoperabilidade e coexistência
  Este tópico descreve a interoperabilidade e a coexistência do [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] em vários recursos do [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]. Esses recursos incluem: Grupos de Disponibilidade AlwaysOn, Espelhamento de Banco de Dados, Planos de Manutenção de Backup, Envio de Logs, Backups ad hoc, Desanexar Banco de Dados e Remover Banco de Dados.  
  
### <a name="alwayson-availability-groups"></a>Grupos de Disponibilidade AlwaysOn  
 Grupos de Disponibilidade AlwaysOn configurados como uma solução única do Windows Azure com suporte para [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]. Não há suporte para configurações Grupo de Disponibilidade AlwaysOn Híbrido ou somente no local. Para obter mais informações e outras considerações, consulte [Configurando o SQL Server Managed Backup to Windows Azure para grupos de disponibilidade](../../2014/database-engine/setting-up-sql-server-managed-backup-to-windows-azure-for-availability-groups.md)  
  
### <a name="database-mirroring"></a>Espelhamento de banco de dados  
 Há suporte para o [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] somente no banco de dados principal. Se o banco de dados principal e o banco de dados espelho estiverem configurados para usar o [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)], o banco de dados espelho será ignorado e não será incluído no backup. No entanto, se ocorrer um failover, o [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] iniciará o processo de backup depois que o espelho concluir a troca de função e estiver online. Os backups serão armazenados em um novo contêiner nesse caso. Se o espelho não estiver configurado para usar o [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)], no caso de um failover, nenhum backup será feito. É recomendável que você configure o [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] no banco de dados principal e no banco de dados espelho para que os backups continuem caso ocorra um failover.  
  
> [!TIP]  
>  Se você estiver criando um banco de dados espelho em uma instância com as configurações padrão do [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)], talvez seja preferível desabilitar os valores padrão de instância do [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)], para que eles não sejam aplicados ao banco de dados espelho e não habilitem novamente os valores padrão da instância após a configuração do banco de dados principal e do banco de dados espelho.  
  
### <a name="maintenance-plan"></a>Plano de Manutenção  
 Não há suporte ao uso de planos de manutenção para criar backups de um banco de dados quando o [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] está habilitado. Os planos de manutenção causarão a interrupção da cadeia de logs e o [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] talvez não possa oferecer suporte a uma capacidade de recuperação garantida do banco de dados durante a restauração. Isso também se aplica quando o [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] está habilitado no nível da instância.  
  
> [!TIP]  
>  Os Planos de Manutenção com Backups somente cópia somente têm suporte com o [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] configurado para o mesmo banco de dados ou instância.  
  
### <a name="log-shipping"></a>Envio de logs  
 Você não pode configurar o envio de logs e o [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] para o mesmo banco de dados ao mesmo tempo. Isso afetará a capacidade de recuperação do banco de dados usando qualquer uma das funcionalidades.  
  
### <a name="ad-hoc-backups-using-transact-sql-and-sql-server-management-studio"></a>Backups ad hoc usando Transact-SQL e SQL Server Management Studio  
 Os backups ad hoc ou de uma vez criados fora do [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] usando Transact-SQL ou SQL Server Management Studio podem afetar o processo do [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)], dependendo do tipo de backup e da mídia de armazenamento usados. Os backups de log para um armazenamento do Windows Azure diferente do qual o [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] está usando ou qualquer outro destino sem ser o serviço de armazenamento de Blob do Windows Azure causará uma interrupção da cadeia de logs. Recomendamos que você use o [smart_admin.sp_backup_on_demand &#40;Transact-SQL&#41; ](/sql/relational-databases/system-stored-procedures/managed-backup-sp-backup-on-demand-transact-sql) procedimento armazenado para iniciar um backup em bancos de dados com [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] habilitado. Você pode iniciar um banco de dados completo ou um backup de log usando esse procedimento armazenado.  
  
### <a name="drop-database-and-detach-database"></a>Remover Banco de Dados e Desanexar Banco de Dados  
 Se um banco de dados que tiver o [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] habilitado for desanexado ou removido, embora nenhum backup adicional seja possível, os backups anteriores permanecem no armazenamento até o fim do período de retenção, ponto no qual os backups serão limpos.  
  
### <a name="changes-to-recovery-model"></a>Alterações no modelo de recuperação  
  
-   Se você alterar o modelo de recuperação do banco de dados de **simples** para **completo** ou **Bulk-Logged**, você tem a opção de configuração [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] para o banco de dados. Isso será considerado como um novo banco de dados da perspectiva do [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)].  
  
-   Se você alterar o modelo de recuperação do banco de dados de **completo** ou **Bulk-Logged** para **simples**, que tem [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] deixará de ser habilitadas, o backup de operações agendado. A configuração de período de retenção ainda estará ativa e os arquivos de backup permanecerão na conta de armazenamento até que o período de retenção tenha decorrido. Se quiser reter os backups, é recomendável que você baixe os arquivos para uma conta de armazenamento diferente ou uma opção local. As definições de configuração são mantidas e podem ser reutilizadas se o modelo de recuperação for definido novamente como **completo** ou **Bulk-Logged** novamente.  
  
### <a name="log-backups-using-other-backup-tools-or-custom-scripts"></a>Backups de log usando outras ferramentas de backup ou scripts personalizados  
 Os dois backups que estiverem configurados para executar os backups de log no mesmo banco de dados causarão a interrupção na cadeia de logs de backup. Embora o [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] tente resolver a interrupção na cadeia de backup agendando backups completos quando uma interrupção na cadeia for detectada, isso significa acompanhar continuamente com interrupções periódicas e backups de log executados por duas ferramentas concorrentes. Isso também pode afetar potencialmente a recuperabilidade do banco de dados porque nenhuma ferramenta pode ter um conjunto completo de backups em sequência. Embora isso se aplique aos dois recursos ou ferramentas que executam os backups de log, é útil chamar exemplos específicos conforme descrito abaixo. Essa também é a base para os problemas com a configuração dos planos de manutenção ou envio de logs conforme descrito nas seções anteriores deste tópico.  
  
 **Backups com base em Data Protection Manager (DPM):** Microsoft Data Protection Manager permite que você faça backups completos e incrementais. Os backups incrementais são os backups de log que executam um truncamento de log depois de criar um backup de T-log. Para configurar o DPM e o [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] para o mesmo banco de dados não tem suporte.  
  
 **Ferramentas de terceiros ou Scripts:** qualquer ferramenta de terceiros ou scripts que realizam causando o truncamento de log é incompatível com os backups de log [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]e não é suportado.  
  
 Se você tiver [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] habilitada para uma instância de banco de dados, e você deseja fazer um backup ad hoc, você pode usar o [smart_admin.sp_backup_on_demand &#40;Transact-SQL&#41; ](/sql/relational-databases/system-stored-procedures/managed-backup-sp-backup-on-demand-transact-sql) procedimento armazenado conforme descrito no anterior seção. Se você também tiver uma necessidade de agendar backup periodicamente fora do [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)], poderá usar Copiar Somente Backup.  Para obter mais informações, veja [Backups somente cópia &#40;SQL Server&#41;](../relational-databases/backup-restore/copy-only-backups-sql-server.md).  
  
  
