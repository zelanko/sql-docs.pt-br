---
title: Reverter um banco de dados para um instantâneo do banco de dados | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- database snapshots [SQL Server], reverting to
- reverting databases
ms.assetid: 8f74dd31-c9ca-4537-8760-0c7648f0787d
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: ef9bda4b8eeff394e44ba696e228b121015960b9
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52774348"
---
# <a name="revert-a-database-to-a-database-snapshot"></a>Reverter um banco de dados a um instantâneo do banco de dados
  Se os dados em um banco de dados online forem danificados, em alguns casos, reverter o banco de dados para um instantâneo do banco de dados que preceda o dano pode ser uma alternativa apropriada para restaurar o banco de dados de um backup. Por exemplo, reverter um banco de dados pode ser útil para reverter um erro sério recente de usuário, como uma tabela descartada. Porém, todas as mudanças feitas depois que o instantâneo foi criado serão perdidas.  
  
-   **Antes de começar:**  
  
     [Limitações e restrições](#Restrictions)  
  
     [Pré-requisitos](#Prerequisites)  
  
     [Segurança](#Security)  
  
-   **Para reverter um banco de dados para um instantâneo de banco de dados, usando:**  [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Restrictions"></a> Limitações e Restrições  
 Não há suporte para a reversão nas seguintes condições:  
  
-   O banco de dados deve ter somente um instantâneo do banco de dados no momento, para o qual você planeja reverter.  
  
-   Grupos de arquivos somente leitura ou compactados existem no banco de dados.  
  
-   Há algum arquivo offline agora, mas que estava online quando o instantâneo foi criado.  
  
 Antes de reverter um banco de dados, considere as seguintes limitações:  
  
-   Reverter não é destinado à recuperação de mídia. para obter informações sobre a ferramenta de configuração e recursos adicionais. Um instantâneo do banco de dados é uma cópia incompleta dos arquivos de banco de dados. Assim, se o banco de dados ou o instantâneo do banco de dados estiver corrompido, reverter de um instantâneo será praticamente impossível. Além disso, mesmo quando isso é possível, é improvável que a reversão corrija o problema no caso de corrupção. Portanto, é essencial fazer backups e testar regularmente seu plano de restauração para proteger um banco de dados. Para obter mais informações, consulte [Back Up and Restore of SQL Server Databases](../backup-restore/back-up-and-restore-of-sql-server-databases.md).  
  
    > [!NOTE]  
    >  Se você precisa ser capaz de restaurar o banco de dados de origem para o momento determinado em que o instantâneo do banco de dados foi criado, use um modelo de recuperação completo e implemente uma política de backup que permita fazer isso.  
  
-   O banco de dados de origem original é substituído pelo banco de dados revertido. Assim, as atualizações feitas no banco de dados desde a criação do instantâneo são perdidas.  
  
-   A operação de reversão também substitui o arquivo de log antigo e recria o log. Consequentemente, você não pode fazer roll forward do banco de dados revertido para o ponto do erro do usuário. Portanto, recomendamos que você faça backup do log antes de reverter um banco de dados.  
  
    > [!NOTE]  
    >  Embora você não possa restaurar o registro original para roll-forward do banco de dados, a informações no arquivo de log original pode ser útil para reconstruir os dados perdidos.  
  
-   A reversão quebra a cadeia de backup de log. Então, antes de fazer o backup de log do banco de dados revertido, você deve primeiro fazer um backup do banco de dados completo ou um backup de arquivo. Recomendamos um backup de banco de dados completo.  
  
-   Durante uma operação de reversão, o instantâneo e o banco de dados de origem ficam indisponíveis. O instantâneo e o banco de dados de origem são ambos marcados como “Em restauração”. Se ocorrer um erro durante a operação de reversão, quando o banco de dados for novamente inicializado, a operação de reversão tentará terminar a reversão.  
  
-   Os metadados de um banco de dados revertido são iguais aos metadados na hora do instantâneo.  
  
-   A reversão cancela todos os catálogos de texto completo.  
  
###  <a name="Prerequisites"></a> Pré-requisitos  
 Verifique se o banco de dados de origem e o instantâneo do banco de dados atendem aos seguintes pré-requisitos:  
  
-   Verifique se o banco de dados não foi corrompido.  
  
    > [!NOTE]  
    >  Se o banco de dados tiver sido corrompido, você precisará restaurá-lo de backups. Para obter mais informações, veja [Restaurações completas de banco de dados &#40;Modelo de recuperação simples#41;](../backup-restore/complete-database-restores-simple-recovery-model.md) ou [Restaurações completas de banco de dados &#40;Modelo de recuperação completa#41;](../backup-restore/complete-database-restores-full-recovery-model.md).  
  
-   Identifique um instantâneo recente que foi criado antes do erro. Para obter mais informações, consulte [Exibir um instantâneo de banco de dados &#40;SQL Server&#41;](view-a-database-snapshot-sql-server.md).  
  
-   Descarte todos os outros instantâneos que existem no banco de dados. Para obter mais informações, consulte [Remover um instantâneo do banco de dados &#40;Transact-SQL&#41;](drop-a-database-snapshot-transact-sql.md).  
  
###  <a name="Security"></a> Segurança  
  
####  <a name="Permissions"></a> Permissões  
 Qualquer usuário que tenha permissões RESTORE DATABASE no banco de dados de origem pode revertê-lo ao estado em que estava quando o instantâneo de banco de dados foi criado.  
  
##  <a name="TsqlProcedure"></a> Como reverter o banco de dados para um instantâneo do banco de dados (usando Transact-SQL)  
 **Para reverter um banco de dados a um instantâneo do banco de dados**  
  
> [!NOTE]  
>  Para obter um exemplo deste procedimento, consulte [Exemplos (Transact-SQL)](#TsqlExample), posteriormente nesta seção.  
  
1.  Identifique o instantâneo do banco de dados para o qual você quer reverter o banco de dados. É possível exibir os instantâneos em um banco de dados do [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] (veja [Exibir um instantâneo de banco de dados &#40;SQL Server&#41;](view-a-database-snapshot-sql-server.md)). Além disso, você pode identificar o banco de dados de origem em uma exibição da coluna **source_database_id** da exibição dr catálogo [sys.databases &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql) .  
  
2.  Cancele qualquer outro instantâneo do banco de dados.  
  
     Para obter informações sobre como remover instantâneos, veja [Remover um instantâneo do banco de dados &#40;Transact-SQL&#41;](drop-a-database-snapshot-transact-sql.md). Se o banco de dados usar o modelo de recuperação completa, antes de fazer a reversão, você deve fazer o backup do log. Para obter mais informações, veja [Fazer backup do log de transações &#40;SQL Server&#41;](../backup-restore/back-up-a-transaction-log-sql-server.md) ou [Fazer backup do log de transações quando o banco de dados está danificado &#40;SQL Server&#41;](../backup-restore/back-up-the-transaction-log-when-the-database-is-damaged-sql-server.md).  
  
3.  Execute a operação de reversão.  
  
     Uma operação de reversão requer permissões RESTORE DATABASE no banco de dados de origem. Para reverter o banco de dados, use a seguinte instrução Transact-SQL:  
  
     RESTORE DATABASE *database_name* FROM DATABASE_SNAPSHOT **=***database_snapshot_name*  
  
     Em que *database_name* é o banco de dados de origem e *database_snapshot_name* é o nome do instantâneo para o qual você deseja reverter o banco de dados. Observe que nessa instrução, você deve especificar um nome de instantâneo em vez de um dispositivo de backup.  
  
     Para obter mais informações, consulte [RESTORE &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-transact-sql).  
  
    > [!NOTE]  
    >  Durante a operação de reversão, o instantâneo e o banco de dados de origem estão indisponíveis. O instantâneo e o banco de dados de origem ficam ambos marcados como “Em restauração”. Se ocorrer um erro durante a operação de reversão, ela tentará terminar a reversão quando o banco de dados for novamente inicializado.  
  
4.  Se o proprietário do banco de dados mudou desde a criação do instantâneo do banco de dados, convém atualizar o proprietário do banco de dados do banco de dados revertido.  
  
    > [!NOTE]  
    >  O banco de dados revertido retém as permissões e configuração (como proprietário de banco de dados e modelo de recuperação) do instantâneo do banco de dados.  
  
5.  Inicie o banco de dados.  
  
6.  Opcionalmente, faça backup do banco de dados revertido, especialmente se usar o modelo de recuperação completa (ou registrada em massa). Para fazer backup de um banco de dados, veja [Criar um backup completo de banco de dados &#40;SQL Server&#41;](../backup-restore/create-a-full-database-backup-sql-server.md).  
  
###  <a name="TsqlExample"></a> Exemplos (Transact-SQL)  
 Esta seção contém os seguintes exemplos de reversão de um banco de dados para um instantâneo do banco de dados:  
  
-   A. [Revertendo um instantâneo no banco de dados AdventureWorks](#Reverting_AW)  
  
-   b. [Revertendo um instantâneo no banco de dados Sales](#Reverting_Sales)  
  
####  <a name="Reverting_AW"></a> A. Revertendo um instantâneo no banco de dados AdventureWorks  
 Este exemplo presume que existe apenas um instantâneo atualmente no banco de dados [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] . Por obter o exemplo que cria o instantâneo para o qual o banco de dados é revertido, veja [Criar um instantâneo de banco de dados &#40;Transact-SQL&#41;](create-a-database-snapshot-transact-sql.md).  
  
```  
USE master;  
-- Reverting AdventureWorks to AdventureWorks_dbss1800  
RESTORE DATABASE AdventureWorks from   
DATABASE_SNAPSHOT = 'AdventureWorks_dbss1800';  
GO  
```  
  
####  <a name="Reverting_Sales"></a> B. Revertendo um instantâneo no banco de dados Sales  
 Este exemplo presume que existem dois instantâneos atualmente no banco de dados **Sales** : **sales_snapshot0600** e **sales_snapshot1200**. O exemplo exclui o mais antigo dos instantâneos e reverte o banco de dados para o instantâneo mais recente.  
  
 Para obter o código para criar o banco de dados de exemplo e instantâneos dos quais esse exemplo depende, consulte:  
  
-   Para obter o banco de dados **Sales** e o instantâneo **sales_snapshot0600**, veja “Criando um banco de dados com grupos de arquivo” e “Criando um instantâneo de banco de dados” em [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](/sql/t-sql/statements/create-database-sql-server-transact-sql).  
  
-   Para obter o banco de dados **sales_snapshot1200** , veja “Criando um instantâneo do banco de dados Sales” em [Criar um instantâneo de banco de dados &#40;Transact-SQL&#41;](create-a-database-snapshot-transact-sql.md).  
  
```  
--Test to see if sales_snapshot0600 exists and if it   
-- does, delete it.  
IF EXISTS (SELECT dbid FROM sys.databases  
    WHERE NAME='sales_snapshot0600')  
    DROP DATABASE SalesSnapshot0600;  
GO  
-- Reverting Sales to sales_snapshot1200  
USE master;  
RESTORE DATABASE Sales FROM DATABASE_SNAPSHOT = 'sales_snapshot1200';  
GO  
```  
  
##  <a name="RelatedTasks"></a> Tarefas relacionadas  
  
-   [Criar um instantâneo de banco de dados &#40;Transact-SQL&#41;](create-a-database-snapshot-transact-sql.md)  
  
-   [Exibir um instantâneo de banco de dados &#40;SQL Server&#41;](view-a-database-snapshot-sql-server.md)  
  
-   [Remover um instantâneo do banco de dados &#40;Transact-SQL&#41;](drop-a-database-snapshot-transact-sql.md)  
  
## <a name="see-also"></a>Consulte também  
 [Instantâneos de banco de dados &#40;SQL Server&#41;](database-snapshots-sql-server.md)   
 [RESTORE &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-transact-sql)   
 [sys.databases &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql)   
 [Espelhamento de banco de dados e instantâneos de banco de dados &#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-and-database-snapshots-sql-server.md)  
  
  
