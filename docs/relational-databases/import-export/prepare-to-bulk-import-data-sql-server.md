---
title: Preparar para importar dados em massa (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: data-movement
ms.topic: conceptual
helpviewer_keywords:
- bulk importing [SQL Server], about bulk importing
- BULK INSERT statement, guidelines
- BULK INSERT statement, restrictions
- bcp utility [SQL Server], guidelines
- bcp utility [SQL Server], restrictions
- hidden characters
- OPENROWSET function, BCP guidelines
ms.assetid: a82ef43c-d006-4c71-bfca-f001a3ba1ba0
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 7d8685db3716ad495581ae64023bfbdd41975e2f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "64946630"
---
# <a name="prepare-to-bulk-import-data-sql-server"></a>Preparar para importar dados em massa (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  Você pode usar o comando **bcp** , a instrução BULK INSERT ou a função OPENROWSET(BULK) para a importação de dados em massa somente de um arquivo de dados.  
  
> [!NOTE]  
>  É possível gravar um aplicativo personalizado que importa dados em massa de objetos que não sejam arquivos de texto. Para a importação de dados em massa de buffers de memória, use as extensões bcp para a API do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client (ODBC) ou a interface OLE DB **IRowsetFastLoad** .  Para importar dados em massa de uma tabela de dados C#, use a API de cópia em massa do ADO.NET, **SqlBulkCopy**.  
  
> [!NOTE]  
>  A importação de dados em massa em uma tabela remota não é suportada.  
  
 Use as seguintes diretrizes ao exportar dados em massa de um arquivo de dados para uma instância do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  
  
-   Obtenha as permissões exigidas para sua conta do usuário.  
  
     A conta do usuário na qual você usa o utilitário **bcp**, a instrução BULK INSERT ou a instrução INSERT... SELECT * FROM OPENROWSET(BULK...) deve ter as permissões exigidas na tabela, que são atribuídas pelo proprietário de tabela. Para obter mais informações sobre as permissões necessárias para cada método, veja [Utilitário bcp](../../tools/bcp-utility.md), [OPENROWSET &#40;Transact-SQL&#41;](../../t-sql/functions/openrowset-transact-sql.md) e [BULK INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/bulk-insert-transact-sql.md).  
  
-   Use o modelo de recuperação bulk-logged  
  
     Esta diretriz é para um banco de dados que usa o modelo de recuperação completa. O modelo de recuperação bulk-logged é útil ao executar operações em massa em uma tabela não indexada (uma *heap*). O uso da recuperação com log de operações em massa ajuda a impedir que o log de transações fique sem espaço porque a recuperação com log de operações em massa não executa inserções de linhas de log. Para obter mais informações sobre o modelo de recuperação bulk-logged, veja [Modelos de recuperação &#40;SQL Server&#41;](../../relational-databases/backup-restore/recovery-models-sql-server.md).  
  
     Recomendamos que você altere o banco de dados para usar o modelo de recuperação bulk-logged imediatamente antes da operação de importação em massa. Imediatamente após, você deve reajustar o banco de dados para o modelo de recuperação completa. Para obter mais informações, veja [Exibir ou alterar o modelo de recuperação de um banco de dados &#40;SQL Server&#41;](../../relational-databases/backup-restore/view-or-change-the-recovery-model-of-a-database-sql-server.md).  
  
    > [!NOTE]  
    >  mais informações sobre como minimizar o log durante operações de importação em massa, veja [Pré-requisitos para log mínimo na importação em massa](../../relational-databases/import-export/prerequisites-for-minimal-logging-in-bulk-import.md).  
  
-   Faça backup após a importação de dados em massa.  
  
     Para um banco de dados que usa o modelo de recuperação simples, recomendamos que você faça um backup diferencial ou completo após a finalização da operação de importação em massa. Para obter mais informações, veja [Criar um backup completo de banco de dados &#40;SQL Server&#41;](../../relational-databases/backup-restore/create-a-full-database-backup-sql-server.md) ou [Criar um backup de banco de dados diferencial &#40;SQL Server&#41;](../../relational-databases/backup-restore/create-a-differential-database-backup-sql-server.md).  
  
     Um backup de log é suficiente para o modelo de recuperação completa ou o modelo de recuperação bulk-logged. Para obter mais informações, veja [Backups de log do transações &#40;SQL Server&#41;](../../relational-databases/backup-restore/transaction-log-backups-sql-server.md).  
  
-   Descarte os índices da tabela para melhorar o desempenho para grandes importações em massa.  
  
     Esta diretriz é para quando você estiver importando uma grande quantidade de dados em comparação à quantidade de dados que já está na tabela. Neste caso, descartar os índices da tabela antes de executar a operação da importação em massa pode aumentar significativamente o desempenho.  
  
    > [!NOTE]  
    >  Se você estiver carregando uma quantidade pequena de dados em comparação à quantidade de dados presente na tabela, descartar os índices será contraproducente. É provável que o tempo exigido para recriar os índices seja mais longo do que o tempo economizado durante a operação de importação em massa.  
  
-   Encontre e remova caracteres ocultos no arquivo de dados.  
  
     Muitos utilitários e editores de textos exibem caracteres ocultos que normalmente estão no final do arquivo de dados. Durante uma operação de importação em massa, os caracteres ocultos em um arquivo de dados ASCII podem causar problemas que provocam erro de "unexpected null found" Encontrar e remover todos os caracteres ocultos deve ajudar a evitar este problema.  
  
## <a name="see-also"></a>Consulte Também  
 [Importar e exportar dados em massa usando o utilitário bcp &#40;SQL Server&#41;](../../relational-databases/import-export/import-and-export-bulk-data-by-using-the-bcp-utility-sql-server.md)   
 [Importar dados em massa usando BULK INSERT ou OPENROWSET&#40;BULK...&#41; &#40;SQL Server&#41;](../../relational-databases/import-export/import-bulk-data-by-using-bulk-insert-or-openrowset-bulk-sql-server.md)   
 [Utilitário bcp](../../tools/bcp-utility.md)   
 [BULK INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/bulk-insert-transact-sql.md)   
 [Formatos de dados para importação ou exportação em massa &#40;SQL Server&#41;](../../relational-databases/import-export/data-formats-for-bulk-import-or-bulk-export-sql-server.md)   
 [OPENROWSET &#40;Transact-SQL&#41;](../../t-sql/functions/openrowset-transact-sql.md)  
  
  
