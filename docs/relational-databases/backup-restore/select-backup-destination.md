---
title: Selecionar destino do backup | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: backup-restore
ms.reviewer: 
ms.suite: sql
ms.technology:
- dbe-backup-restore
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.swb.selectbackupdest.f1
ms.assetid: f79e824b-1525-45de-8ede-513563af41b6
caps.latest.revision: 
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 08a629ac319f874312d6bb3878c721d783a5fe12
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/18/2018
---
# <a name="select-backup-destination"></a>Selecionar destino do backup
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  Use a caixa de diálogo **Selecionar Destino do Backup** para selecionar um dispositivo como seu destino de backup. Um destino de backup pode ser tanto um disco quanto um dispositivo de backup lógico.  
  
 **Para usar o SQL Server Management Studio para fazer o backup de um banco de dados**  
  
-   [Criar um backup completo de banco de dados &#40;SQL Server&#41;](../../relational-databases/backup-restore/create-a-full-database-backup-sql-server.md)  
  
-   [Criar um backup diferencial de banco de dados &#40;SQL Server&#41;](../../relational-databases/backup-restore/create-a-differential-database-backup-sql-server.md)  
  
-   [Fazer backup de arquivos e de grupos de arquivos &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-files-and-filegroups-sql-server.md)  
  
-   [Fazer backup de um log de transações &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-a-transaction-log-sql-server.md)  
  
## <a name="options"></a>Opções  
 As opções dessa caixa de diálogo dependem do fato de você estar selecionando um destino em disco ou em fita.  
  
 **Destino em disco**  
 Para especificar um destino de backup, escolha uma das opções a seguir.  
  
|||  
|-|-|  
|**Nome do arquivo**|Escolha esta opção para digitar na caixa de texto um arquivo local ou remoto como o destino de backup para:<br /><br /> especificar um arquivo local, clique no botão Procurar à direita da caixa de texto e navegue para um arquivo nas unidades fixas do computador que está executando o servidor, ou digite diretamente o caminho completo e nome de arquivo; por exemplo, `C:\Program Files\Microsoft SQL Server\MSSQL\Backup\AdventureWorksBackup.bak`.<br /><br /> Para especificar um arquivo remoto como seu destino de backup, digite o nome da UNC (Convenção de Nomenclatura Universal) totalmente qualificado. Para obter mais informações, consulte [Dispositivos de backup &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-devices-sql-server.md).<br /><br /> <br /><br /> **\*\* Importante \*\*** Backups de dados em uma rede podem estar sujeitos a erros de rede; assim, recomendamos que você verifique a operação de backup quando ela estiver concluída. Para obter mais informações, consulte [RESTORE VERIFYONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-verifyonly-transact-sql.md).|  
|**Dispositivo de backup**|Escolha esta opção para selecionar um dispositivo de backup lógico.<br /><br /> Observação: para obter informações sobre como criar um dispositivo de backup em disco, consulte [Definir um dispositivo de backup lógico para um arquivo de disco &#40;SQL Server&#41;](../../relational-databases/backup-restore/define-a-logical-backup-device-for-a-disk-file-sql-server.md).|  
  
 **Destino em fita**  
 Especifique um destino de backup em uma unidade de fita conectada fisicamente ao computador que está executando o servidor (ou seja, a instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)]). Escolha uma das opções a seguir.  
  
|||  
|-|-|  
|**Unidade de fita**|Escolha esta opção para selecionar uma unidade de fita como destino de backup da lista de unidades de fita conectadas fisicamente ao computador que está executando a instância do servidor.<br /><br /> Observação: dispositivos de backup em fita em computadores remotos não são destinos de backup válidos.|  
|**Dispositivo de backup**|Escolha esta opção para selecionar um dispositivo de backup lógico existente. Esses dispositivos de backup lógicos correspondem a unidades de fita conectadas fisicamente ao computador que está executando a instância do servidor.<br /><br /> Observação: para obter informações sobre como criar um dispositivo de backup em fita, consulte [Definir um dispositivo de backup lógico para uma unidade de fita &#40;SQL Server&#41;](../../relational-databases/backup-restore/define-a-logical-backup-device-for-a-tape-drive-sql-server.md).|  
  
## <a name="see-also"></a>Consulte Também  
 [Dispositivos de backup &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-devices-sql-server.md)   
 [Conjuntos de mídias, famílias de mídia e conjuntos de backup &#40;SQL Server&#41;](../../relational-databases/backup-restore/media-sets-media-families-and-backup-sets-sql-server.md)  
  
  
