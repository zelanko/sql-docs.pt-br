---
title: Restaurar um backup de banco de dados no modelo de recuperação simples (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- full backups [SQL Server]
- database restores [SQL Server], full backups
- backing up databases [SQL Server], full backups
- database backups [SQL Server], full backups
- restoring databases [SQL Server], full backups
ms.assetid: a928fa36-e285-476f-9a7b-6840a8bb7283
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: e2fd00fd96fe9b0bf7e1b605d935908970d0c1fc
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62875624"
---
# <a name="restore-a-database-backup-under-the-simple-recovery-model-transact-sql"></a>Restaurar um backup de banco de dados no modelo de recuperação simples (Transact-SQL)
  Este tópico explica como restaurar um backup de banco de dados completo.  
  
> [!IMPORTANT]  
>  O administrador do sistema que restaura o backup de banco de dados completo deve ser a única pessoa a usar o banco de dados a ser restaurado.  
  
## <a name="prerequisites-and-recommendations"></a>Pré-requisitos e recomendações  
  
-   Para restaurar um banco de dados criptografado, é necessário ter acesso ao certificado ou à chave assimétrica usada para criptografar o banco de dados. Sem o certificado ou a chave assimétrica, o banco de dados não pode ser restaurado. Como resultado, o certificado usado para criptografar a chave de criptografia do banco de dados deverá ser retido enquanto o backup for necessário. Para obter mais informações, consulte [SQL Server Certificates and Asymmetric Keys](../security/sql-server-certificates-and-asymmetric-keys.md).  
  
-   Por motivos de segurança, é recomendável não anexar ou restaurar bancos de dados de origens desconhecidas ou não confiáveis. Esses bancos de dados podem conter um código mal-intencionado que pode executar um código [!INCLUDE[tsql](../../includes/tsql-md.md)] inesperado ou provocar erros modificando o esquema ou a estrutura física do banco de dados. Antes de usar um banco de dados de origem desconhecida ou não confiável, execute [DBCC CHECKDB](/sql/t-sql/database-console-commands/dbcc-checkdb-transact-sql) no banco de dados, em um servidor que não seja de produção. Além disso, examine o código, como procedimentos armazenados ou outro código definido pelo usuário, no banco de dados.  
  
## <a name="database-compatibility-level-after-upgrade"></a>Nível de compatibilidade do banco de dados após a atualização  
 Os níveis de compatibilidade dos bancos de dados **tempdb**, **model**, **msdb** e **Resource** é definido para o nível de compatibilidade do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] após a atualização. O banco de dados do sistema **mestre** mantém o nível de compatibilidade que tinha antes da atualização, a menos que esse nível era inferior a 100. Se o nível de compatibilidade do **mestre** era inferior a 100 antes da atualização, ele será definido como 100 após a atualização.  
  
 Se o nível de compatibilidade de um banco de dados de usuário era 100 ou mais alto antes da atualização, ele permanecerá o mesmo depois da atualização. Se o nível de compatibilidade era 90 antes da atualização, no banco de dados atualizado, o nível de compatibilidade será definido como 100, que é o nível de compatibilidade mais baixo com suporte no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
> [!NOTE]  
>  Os novos bancos de dados de usuários herdam o nível de compatibilidade do banco de dados **model** .  
  
## <a name="procedures"></a>Procedimentos  
  
#### <a name="to-restore-a-full-database-backup"></a>Para restaurar um backup de banco de dados completo  
  
1.  Execute a instrução RESTORE DATABASE para restaurar o backup de banco de dados completo, especificando:  
  
    -   O nome do banco de dados a ser restaurado.  
  
    -   O dispositivo de backup a partir do qual o backup de banco de dados completo é restaurado.  
  
    -   A cláusula NORECOVERY, se você tiver um log de transações ou backup de banco de dados diferencial para aplicar após restaurar o backup de banco de dados completo.  
  
    > [!IMPORTANT]  
    >  Para restaurar um banco de dados criptografado, é necessário ter acesso ao certificado ou à chave assimétrica usada para criptografar o banco de dados. Sem o certificado ou a chave assimétrica, o banco de dados não pode ser restaurado. Como resultado, o certificado usado para criptografar a chave de criptografia do banco de dados deverá ser retido enquanto o backup for necessário. Para obter mais informações, consulte [SQL Server Certificates and Asymmetric Keys](../security/sql-server-certificates-and-asymmetric-keys.md).  
  
2.  Opcionalmente, especifique:  
  
    -   A cláusula FILE para identificar o conjunto de backup no dispositivo de banco de dados a ser restaurado.  
  
> [!NOTE]  
>  Se você restaurar um banco de dados da versão anterior para o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], o banco de dados será atualizado automaticamente. Normalmente, o banco de dados se torna disponível imediatamente. No entanto, se um banco de dados do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] tiver índices de texto completo, o processo de atualização importará, redefinirá ou recriará esses índices, dependendo da configuração da propriedade de servidor  **upgrade_option** . Se a opção de atualização for definida como importar (**upgrade_option** = 2) ou recriar (**upgrade_option** = 0), os índices de texto completo permanecerão indisponíveis durante a atualização. Dependendo da quantidade de dados a serem indexados, a importação pode levar várias horas, e a recriação pode ser até dez vezes mais demorada. Lembre-se também de que, quando a opção de atualização estiver definida para importar, os índices de texto completo associados serão recriados se um catálogo de texto completo não estiver disponível. Para alterar a configuração da propriedade de servidor **upgrade_option** , use [sp_fulltext_service](/sql/relational-databases/system-stored-procedures/sp-fulltext-service-transact-sql).  
  
## <a name="example"></a>Exemplo  
  
### <a name="description"></a>DESCRIÇÃO  
 Este exemplo restaura o backup de banco de dados completo [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] a partir da fita.  
  
### <a name="example"></a>Exemplo  
  
```  
USE master;  
GO  
RESTORE DATABASE AdventureWorks2012  
   FROM TAPE = '\\.\Tape0';  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Restaurações completas de banco de dados &#40;Modelo de recuperação completa&#41;](complete-database-restores-full-recovery-model.md)   
 [Restaurações completas de banco de dados &#40;Modelo de recuperação simples#41;](complete-database-restores-simple-recovery-model.md)   
 [Backups de bancos de dados completos &#40;SQL Server&#41;](full-database-backups-sql-server.md)   
 [RESTORE &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-transact-sql)   
 [Informações de histórico e cabeçalho de backup &#40;SQL Server&#41;](backup-history-and-header-information-sql-server.md)   
 [Recompilar bancos de dados do sistema](../databases/system-databases.md)  
  
  
