---
title: Selecionar destino do backup | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
f1_keywords:
- sql12.swb.selectbackupdest.f1
ms.assetid: f79e824b-1525-45de-8ede-513563af41b6
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 5ffd1d2529dd13e42689bcf168c972d757fb5499
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84956536"
---
# <a name="select-backup-destination"></a>Selecionar destino do backup
  Use a caixa de diálogo **Selecionar Destino do Backup** para selecionar um dispositivo como seu destino de backup. Um destino de backup pode ser tanto um disco quanto um dispositivo de backup lógico.  
  
 **Para usar o SQL Server Management Studio para fazer o backup de um banco de dados**  
  
-   [Criar um backup completo de banco de dados &#40;SQL Server&#41;](create-a-full-database-backup-sql-server.md)  
  
-   [Criar um backup diferencial de banco de dados &#40;SQL Server&#41;](create-a-differential-database-backup-sql-server.md)  
  
-   [Fazer backup de arquivos e de grupos de arquivos &#40;SQL Server&#41;](back-up-files-and-filegroups-sql-server.md)  
  
-   [Fazer backup de um log de transações &#40;SQL Server&#41;](back-up-a-transaction-log-sql-server.md)  
  
## <a name="options"></a>Opções  
 As opções dessa caixa de diálogo dependem do fato de você estar selecionando um destino em disco ou em fita.  
  
 **Destino em disco**  
 Para especificar um destino de backup, escolha uma das opções a seguir.  
  
|||  
|-|-|  
|**Nome do arquivo**|Escolha esta opção para digitar na caixa de texto um arquivo local ou remoto como o destino de backup.<br /><br /> Para especificar um arquivo local, clique no botão Procurar à direita da caixa de texto e navegue para um arquivo nas unidades fixas do computador que está executando o servidor, ou digite diretamente o caminho completo e nome de arquivo; por exemplo, `C:\Program Files\Microsoft SQL Server\MSSQL\Backup\AdventureWorksBackup.bak`.<br /><br /> Para especificar um arquivo remoto como seu destino de backup, digite o nome da Convenção Universal de Nomenclatura (UNC) totalmente qualificada. Para obter mais informações, consulte [Dispositivos de backup &#40;SQL Server&#41;](backup-devices-sql-server.md).<br /><br /> **\*\* Importante \*\*** Backups de dados em uma rede podem estar sujeitos a erros de rede; assim, recomendamos que você verifique a operação de backup quando ela estiver concluída. Para obter mais informações, consulte [RESTORE VERIFYONLY &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-verifyonly-transact-sql).|  
|**Dispositivo de backup**|Escolha esta opção para selecionar um dispositivo de backup lógico.<br /><br /> Observação: para obter informações sobre como criar um dispositivo de backup em disco, consulte [Definir um dispositivo de backup lógico para um arquivo de disco &#40;SQL Server&#41;](define-a-logical-backup-device-for-a-disk-file-sql-server.md).|  
  
 **Destino em fita**  
 Especifique um destino de backup em uma unidade de fita conectada fisicamente ao computador que está executando o servidor (ou seja, a instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)]). Escolha uma das opções a seguir.  
  
|||  
|-|-|  
|**Unidade de fita**|Escolha esta opção para selecionar uma unidade de fita como destino de backup da lista de unidades de fita conectadas fisicamente ao computador que está executando a instância do servidor.<br /><br /> Observação: Dispositivos de backup em fita em computadores remotos não são destinos de backup válidos.|  
|**Dispositivo de backup**|Escolha esta opção para selecionar um dispositivo de backup lógico existente. Esses dispositivos de backup lógicos correspondem a unidades de fita conectadas fisicamente ao computador que está executando a instância do servidor.<br /><br /> Observação: para obter informações sobre como criar um dispositivo de backup em fita, consulte [Definir um dispositivo de backup lógico para uma unidade de fita &#40;SQL Server&#41;](define-a-logical-backup-device-for-a-tape-drive-sql-server.md).|  
  
## <a name="see-also"></a>Consulte Também  
 [Dispositivos de backup &#40;SQL Server&#41;](backup-devices-sql-server.md)   
 [Conjuntos de mídias, famílias de mídia e conjuntos de backup &#40;SQL Server&#41;](media-sets-media-families-and-backup-sets-sql-server.md)  
  
  
