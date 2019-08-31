---
title: 'SQL Server Backup gerenciado no Azure: Interoperabilidade e coexistência | Microsoft Docs'
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
ms.assetid: 78fb78ed-653f-45fe-a02a-a66519bfee1b
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 70d941786fd06e48bf071b8448b84c8f4857f8c8
ms.sourcegitcommit: 3b1f873f02af8f4e89facc7b25f8993f535061c9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/30/2019
ms.locfileid: "70176068"
---
# <a name="sql-server-managed-backup-to-azure-interoperability-and-coexistence"></a>SQL Server Backup gerenciado no Azure: Interoperabilidade e coexistência
  Este tópico descreve a interoperabilidade e a coexistência do [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] em vários recursos do [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]. Entre esses recursos estão: Grupos de Disponibilidade AlwaysOn, espelhamento de banco de dados, planos de manutenção de backup, envio de logs, backups ad hoc, desanexar banco de dados e remover banco de dados.  
  
### <a name="alwayson-availability-groups"></a>Grupos de Disponibilidade AlwaysOn  
 Grupos de Disponibilidade AlwaysOn configuradas como uma solução somente do Azure com suporte [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]para o. Não há suporte para configurações Grupo de Disponibilidade AlwaysOn Híbrido ou somente no local. Para obter mais informações e outras considerações, consulte Configurando [SQL Server Backup gerenciado para o Azure para grupos de disponibilidade](../../2014/database-engine/setting-up-sql-server-managed-backup-to-windows-azure-for-availability-groups.md)  
  
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
 Os backups ad hoc ou de uma vez criados fora do [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] usando Transact-SQL ou SQL Server Management Studio podem afetar o processo do [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)], dependendo do tipo de backup e da mídia de armazenamento usados. Os backups de log para uma conta de armazenamento [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] do Azure diferente do que está usando, ou qualquer outro destino que o serviço de armazenamento de BLOBs do Azure, causarão uma interrupção de cadeia de logs. Recomendamos que você use o procedimento armazenado [Transact &#40;-SQL&#41; smart_admin. sp_backup_on_demand](/sql/relational-databases/system-stored-procedures/managed-backup-sp-backup-on-demand-transact-sql) para iniciar um backup em bancos de dados que tenham [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] sido habilitados. Você pode iniciar um banco de dados completo ou um backup de log usando esse procedimento armazenado.  
  
### <a name="drop-database-and-detach-database"></a>Remover Banco de Dados e Desanexar Banco de Dados  
 Se um banco de dados que tiver o [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] habilitado for desanexado ou removido, embora nenhum backup adicional seja possível, os backups anteriores permanecem no armazenamento até o fim do período de retenção, ponto no qual os backups serão limpos.  
  
### <a name="changes-to-recovery-model"></a>Alterações no modelo de recuperação  
  
-   Se você alterar o modelo de recuperação de um banco de dados de **simples** para **completo** ou **bulk-logged**, terá a opção [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] de configurar para o banco de dados. Isso será considerado como um novo banco de dados da perspectiva do [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)].  
  
-   Se você alterar o modelo de recuperação de um banco de dados de log **completo** ou **em massa** para **simples**, que tenha sido [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] habilitado, as operações de backup não serão mais agendadas. A configuração de período de retenção ainda estará ativa e os arquivos de backup permanecerão na conta de armazenamento até que o período de retenção tenha decorrido. Se quiser reter os backups, é recomendável que você baixe os arquivos para uma conta de armazenamento diferente ou uma opção local. As definições de configuração são mantidas e podem ser reutilizadas se o modelo de recuperação for definido novamente como **completo** ou **registrado em massa** novamente.  
  
### <a name="log-backups-using-other-backup-tools-or-custom-scripts"></a>Backups de log usando outras ferramentas de backup ou scripts personalizados  
 Os dois backups que estiverem configurados para executar os backups de log no mesmo banco de dados causarão a interrupção na cadeia de logs de backup. Embora o [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] tente resolver a interrupção na cadeia de backup agendando backups completos quando uma interrupção na cadeia for detectada, isso significa acompanhar continuamente com interrupções periódicas e backups de log executados por duas ferramentas concorrentes. Isso também pode afetar potencialmente a recuperabilidade do banco de dados porque nenhuma ferramenta pode ter um conjunto completo de backups em sequência. Embora isso se aplique aos dois recursos ou ferramentas que executam os backups de log, é útil chamar exemplos específicos conforme descrito abaixo. Essa também é a base para os problemas com a configuração dos planos de manutenção ou envio de logs conforme descrito nas seções anteriores deste tópico.  
  
 **Backups baseados no Data Protection Manager (DPM):** O Microsoft Data Protection Manager permite que você faça backups completos e incrementais. Os backups incrementais são os backups de log que executam um truncamento de log depois de criar um backup de T-log. Para configurar o DPM e o [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] para o mesmo banco de dados não tem suporte.  
  
 **Scripts ou ferramentas de terceiros:** Qualquer ferramenta de terceiros ou scripts que executam backups de log que causam truncamento de [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]log é incompatível com o e não tem suporte.  
  
 Se você tiver [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] habilitado o para uma instância de banco de dados e desejar fazer um backup ad hoc, poderá usar o procedimento armazenado [Transact &#40;-SQL&#41; smart_admin. sp_backup_on_demand](/sql/relational-databases/system-stored-procedures/managed-backup-sp-backup-on-demand-transact-sql) , conforme descrito na seção anterior. Se você também tiver uma necessidade de agendar backup periodicamente fora do [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)], poderá usar Copiar Somente Backup.  Para obter mais informações, veja [Backups somente cópia &#40;SQL Server&#41;](../relational-databases/backup-restore/copy-only-backups-sql-server.md).  
  
  
