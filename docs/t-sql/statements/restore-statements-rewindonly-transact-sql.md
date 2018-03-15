---
title: RESTORE REWINDONLY (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 08/10/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- RESTORE_REWINDONLY_TSQL
- RESTORE REWINDONLY
dev_langs:
- TSQL
helpviewer_keywords:
- closing backup devices
- backup devices [SQL Server], rewinding
- media [SQL Server]
- open back devices
- rewinding backup devices
- RESTORE REWINDONLY statement
ms.assetid: 7f825b40-2264-4608-9809-590d0f09d882
caps.latest.revision: 
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: bf67d54e58f08296878c0781158e7b878b0b2a49
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/25/2018
---
# <a name="restore-statements---rewindonly-transact-sql"></a>Instruções RESTORE – REWINDONLY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Retrocede e fecha os dispositivos de fita especificados deixados abertos pelas instruções BACKUP ou RESTORE com a opção NOREWIND. Só há suporte para este comando em dispositivos de fita.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
RESTORE REWINDONLY   
FROM <backup_device> [ ,...n ]  
[ WITH {UNLOAD | NOUNLOAD}]  
}   
[;]  
  
<backup_device> ::=  
{   
   { logical_backup_device_name |  
      @logical_backup_device_name_var }  
   | TAPE = { 'physical_backup_device_name' |  
       @physical_backup_device_name_var }   
}   
```  
  
## <a name="arguments"></a>Argumentos  
 **\<backup_device> ::=** 
  
 Especifica os dispositivos de backup lógicos ou físicos a serem usados na operação de restauração.  
  
 { *logical_backup_device_name* | **@***logical_backup_device_name_var* } é o nome lógico, que precisa seguir as regras para identificadores, dos dispositivos de backup criados por **sp_addumpdevice** dos quais o banco de dados é restaurado. Se for fornecido como uma variável (**@***logical_backup_device_name_var*), o nome do dispositivo de backup poderá ser especificado como uma constante de cadeia de caracteres (**@***logical_backup_device_name_var* = *logical_backup_device_name*) ou como uma variável do tipo de dados de cadeia de caracteres, exceto os tipos de dados **ntext** ou **text**.  
  
 {DISK | TAPE } **=** { **'***physical_backup_device_name***'** | **@***physical_backup_device_name_var* } Permite que os backups sejam restaurados do dispositivo de disco ou de fita nomeado. Os tipos de dispositivo de disco e de fita devem ser especificados com o nome real (por exemplo, o caminho e o nome do arquivo completos) do dispositivo: DISK = 'C:\Program Files\Microsoft SQL Server\MSSQL\BACKUP\Mybackup.bak' ou TAPE = '\\\\.\TAPE0'. Se for especificado como uma variável (**@***physical_backup_device_name_var*), o nome do dispositivo poderá ser especificado como uma constante de cadeia de caracteres (**@***physical_backup_device_name_var* = '*physcial_backup_device_name*') ou como uma variável do tipo de dados de cadeia de caracteres, exceto para os tipos de dados **ntext** ou **text**.  
  
 Se usando um servidor de rede com um nome de UNC (que deve conter o nome de máquina), especifique um tipo de dispositivo de disco. Para obter mais informações de como usar os nomes UNC, confira [Dispositivos de backup &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-devices-sql-server.md).  
  
 A conta com a qual você está executando o Microsoft SQL Server precisa ter acesso READ ao computador remoto ou ao servidor de rede para executar uma operação RESTORE.  
  
 *n*  
 É um espaço reservado que indica vários dispositivos de backup e dispositivos de backup lógicos podem ser especificados. O número máximo de dispositivos de backup ou de dispositivos de backup lógicos é **64**.  
  
 Se uma sequência de restauração irá requerer tantos dispositivos de backup quantos foram usados para criar o conjunto de mídia ao qual o backup pertence depende de se a restauração é off-line ou on-line. A restauração off-line permite que um backup seja restaurado usando menos dispositivos que os usados para criar o backup. A restauração on-line requer todos os dispositivos de backup. Uma tentativa de restaurar com menos dispositivos falhará.  
  
 Para obter mais informações, consulte [Dispositivos de backup &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-devices-sql-server.md).  
  
> [!NOTE]  
>  Ao restaurar um backup de um conjunto de mídia espelhado, você pode especificar apenas um único espelho para cada família de mídia. Na presença de erros, entretanto, ter os outros espelhos permite a solução rápida de alguns problemas de restauração. Você pode substituir um volume de mídia danificado pelo volume correspondente de outro espelho. Observe que, para restaurações off-line, você pode restaurar a partir de menos dispositivos que as famílias de mídia, mas cada família é processada apenas uma vez.  
  
 **Opções WITH**  
  
 UNLOAD  
 Especifica que a fita é retrocedida e descarregada automaticamente quando RESTORE for concluído. UNLOAD é definido por padrão quando uma nova sessão de usuário é iniciada. Ele permanece definido até que NOUNLOAD seja especificado. Esta opção só é usada para dispositivos de fita. Se um dispositivo que não seja de fita estiver sendo usado para RESTORE, esta opção será ignorada.  
  
 NOUNLOAD  
 Especifica que a fita não descarregada automaticamente da unidade de fita após RESTORE. NOUNLOAD permanece definido até que UNLOAD seja especificado.  
  
 Especifica que a fita não descarregada automaticamente da unidade de fita após RESTORE. NOUNLOAD permanece definido até que UNLOAD seja especificado.  
  
## <a name="general-remarks"></a>Comentários gerais  
 RESTORE REWINDONLY é uma alternativa a RESTORE LABELONLY FROM TAPE = \<nome > WITH REWIND. Você pode obter uma lista de unidades de fita abertas na exibição de gerenciamento dinâmico [sys.dm_io_backup_tapes](../../relational-databases/system-dynamic-management-views/sys-dm-io-backup-tapes-transact-sql.md).  
  
## <a name="security"></a>Segurança  
  
### <a name="permissions"></a>Permissões  
 Qualquer usuário pode usar RESTORE REWINDONLY.  
  
## <a name="see-also"></a>Consulte Também  
 [BACKUP &#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)   
 [Conjuntos de mídias, famílias de mídia e conjuntos de backup &#40;SQL Server&#41;](../../relational-databases/backup-restore/media-sets-media-families-and-backup-sets-sql-server.md)   
 [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)   
 [Informações de histórico e cabeçalho de backup &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-history-and-header-information-sql-server.md)  
  
  

