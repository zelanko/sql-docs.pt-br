---
title: Definir um dispositivo de backup lógico – fita
description: Este artigo mostra como definir um dispositivo de backup lógico para uma unidade de fita no SQL Server usando o SQL Server Management Studio ou o Transact-SQL.
ms.custom: seo-lt-2019
ms.date: 12/17/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- backup devices [SQL Server], defining
- backup devices [SQL Server], tapes
- backing up databases [SQL Server], tapes
- database backups [SQL Server], tapes
- tape backup devices, creating
ms.assetid: 66f36e1d-0287-4fac-8a51-71f9f0d7ad5b
author: cawrites
ms.author: chadam
ms.openlocfilehash: ddb39f0d488becdcb7711ef05030bad4aff08aa5
ms.sourcegitcommit: 5a1ed81749800c33059dac91b0e18bd8bb3081b1
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/23/2020
ms.locfileid: "96127016"
---
# <a name="define-a-logical-backup-device-for-a-tape-drive-sql-server"></a>Definir um dispositivo de backup lógico para uma unidade de fita (SQL Server)
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  Este tópico descreve como definir um dispositivo de backup lógico para uma unidade de fita no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[tsql](../../includes/tsql-md.md)]. Um dispositivo lógico é um nome definido pelo usuário que aponta para um dispositivo de backup físico específico (um arquivo de disco ou uma unidade de fita).  A inicialização do dispositivo físico acontece depois, quando um backup é gravado no dispositivo de backups.  
  
> [!NOTE]  
>  O suporte a dispositivos de backup em fita será removido em uma versão futura do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam.  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Limitações e restrições](#Restrictions)  
  
     [Segurança](#Security)  
  
-   **Para definir um dispositivo de backup lógico para uma unidade de fita usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> Limitações e restrições  
  
-   A unidade ou as unidades de fita devem ter o suporte do sistema operacional Microsoft Windows.  
  
-   O dispositivo de fita deve estar conectado fisicamente ao computador que está executando uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. O backup em dispositivos de fita remotos não é suportado.  
  
###  <a name="security"></a><a name="Security"></a> Segurança  
  
####  <a name="permissions"></a><a name="Permissions"></a> Permissões  
 Requer associação na função de servidor fixa **diskadmin** .  
  
 Requer permissão para gravar no disco.  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-define-a-logical-backup-device-for-a-tape-drive"></a>Para definir um dispositivo de backup lógico para uma unidade de fita  
  
1.  Depois de se conectar à instância apropriada do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)], em Pesquisador de Objetos, clique no nome do servidor para expandir a árvore do servidor.  
  
2.  Expanda **Objetos de Servidor** e clique com o botão direito do mouse em **Dispositivos de Backup**.  
  
3.  Clique em **Novo Dispositivo de Backup**, que abre a caixa de diálogo **Dispositivo de Backup** .  
  
4.  Coloque um nome de dispositivo.  
  
5.  Para o destino, clique em **Fita** e selecione uma unidade de fita que ainda não esteja associada a outro dispositivo de backup. Se nenhuma das unidade de fita estiver disponível, a opção **Fita** estará inativa.  
  
6.  Para definir o dispositivo novo, clique em **OK**.  

 Para fazer backup neste novo dispositivo, adicione-o ao campo **Fazer backup em:** na caixa de diálogo **Backup de Banco de dados** (**Geral**). Para obter mais informações, veja [Criar um backup completo de banco de dados &#40;SQL Server&#41;](../../relational-databases/backup-restore/create-a-full-database-backup-sql-server.md).  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Usando o Transact-SQL  
  
#### <a name="to-define-a-logical-backup-device-for-a-tape-drive"></a>Para definir um dispositivo de backup lógico para uma unidade de fita  
  
1.  Conecte-se ao [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**. Este exemplo mostra como usar [sp_addumpdevice](../../relational-databases/system-stored-procedures/sp-addumpdevice-transact-sql.md) para definir um dispositivo de backup lógico para uma fita. O exemplo adiciona o dispositivo de backup em fita denominado `tapedump1`, com o nome físico `\\.\tape0`.  
  
```sql  
USE AdventureWorks2012 ;  
GO  
EXEC sp_addumpdevice 'tape', 'tapedump1', '\\.\tape0' ;  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [BACKUP &#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)   
 [sys.backup_devices &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-backup-devices-transact-sql.md)   
 [sp_addumpdevice &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addumpdevice-transact-sql.md)   
 [sp_dropdevice &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropdevice-transact-sql.md)   
 [Dispositivos de backup &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-devices-sql-server.md)   
 [Definir um dispositivo de backup lógico para um arquivo de disco &#40;SQL Server&#41;](../../relational-databases/backup-restore/define-a-logical-backup-device-for-a-disk-file-sql-server.md)   
 [Exibir as propriedades e o conteúdo de um dispositivo de backup lógico &#40;SQL Server&#41;](../../relational-databases/backup-restore/view-the-properties-and-contents-of-a-logical-backup-device-sql-server.md)  
  
  
