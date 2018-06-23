---
title: Gerenciar a tabela suspect_pages (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-backup-restore
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- 824 (Database Engine error)
- restoring pages [SQL Server]
- pages [SQL Server], suspect
- pages [SQL Server], restoring
- suspect_pages system table
- suspect pages [SQL Server]
- restoring [SQL Server], pages
ms.assetid: f394d4bc-1518-4e61-97fc-bf184d972e2b
caps.latest.revision: 54
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: a404c6e4a7ace75d1d17f8ca6dfda0eaf603ea92
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36116179"
---
# <a name="manage-the-suspectpages-table-sql-server"></a>Gerenciar a tabela suspect_pages (SQL Server)
  Este tópico descreve como gerenciar a tabela **suspect_pages** no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou [!INCLUDE[tsql](../../includes/tsql-md.md)]. A tabela **suspect_pages** é usada para manter informações sobre páginas suspeitas e é relevante para ajudar a decidir se a restauração é necessária. A tabela [suspect_pages](/sql/relational-databases/system-tables/suspect-pages-transact-sql) reside no [banco de dados msdb](../databases/msdb-database.md).  
  
 Uma página é considerada "suspeita" quando o [!INCLUDE[ssDEnoversion](../../../includes/ssdenoversion-md.md)] encontra um dos seguintes erros ao tentar ler uma página de dados:  
  
-   Um [erro 823](../errors-events/mssqlserver-823-database-engine-error.md) causado por uma CRC (verificação de redundância cíclica) emitida por um sistema operacional como, por exemplo, um erro de disco (alguns erros de hardware)  
  
-   Um [erro 824](../errors-events/mssqlserver-824-database-engine-error.md), como uma página interrompida (qualquer erro lógico)  
  
 A ID de cada página suspeita é registrada na tabela **suspect_pages** . O [!INCLUDE[ssDE](../../includes/ssde-md.md)] registra qualquer página suspeita encontrada durante o processamento regular, como o seguinte:  
  
-   Uma consulta precisa ler uma página.  
  
-   Durante uma operação DBCC CHECKDB.  
  
-   Durante uma operação de backup.  
  
 A tabela **suspect_pages** também é atualizada conforme necessário durante uma operação de restauração, uma operação de reparo DBCC ou uma operação de remoção de banco de dados.  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Recomendações](#Recommendations)  
  
     [Segurança](#Security)  
  
-   **Para gerenciar a tabela suspect_pages usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Recommendations"></a> Recomendações  
  
-   **Erros registrados na tabela suspect_pages**  
  
     A tabela **suspect_pages** contém uma linha por página que falhou com um erro 824 até o limite de 1.000 linhas. A tabela a seguir mostra erros registrados na coluna **event_type** da tabela **suspect_pages** .  
  
    |Descrição do erro|Valor**event_type** |  
    |-----------------------|---------------------------|  
    |Erro 823 causado por um erro CRC de sistema operacional ou erro 824 diferente de uma soma de verificação inválida ou uma página danificada (por exemplo, uma ID de página inválida).|1|  
    |Soma de verificação inválida|2|  
    |Página danificada|3|  
    |Restaurada (a página foi restaurada depois de marcada como inválida)|4|  
    |Reparada (DBCC, AlwaysOn ou espelhamento reparou a página)|5|  
    |Desalocada pelo DBCC|7|  
  
     A tabela **suspect_pages** também registra erros temporários. Fontes de erros temporários incluem um erro de E/S (por exemplo, um cabo desconectado) ou uma página que temporariamente falha em um teste de soma de verificação repetido.  
  
-   **Como o Mecanismo de Banco de Dados atualiza a tabela suspect_pages**  
  
     O [!INCLUDE[ssDE](../../includes/ssde-md.md)] realiza as seguintes ações na tabela **suspect_pages** :  
  
    -   Se a tabela não estiver completa, a cada erro 824 ela será atualizada para indicar a ocorrência de um erro, e o contador de erros será incrementado. Se uma página tiver um erro consertado pela restauração, restaurado ou desalocado, sua contagem de **number_of_errors** será incrementada e sua coluna **last_update** será atualizada  
  
    -   Depois que uma página listada for corrigida por uma operação de restauração ou reparo, a operação atualizará a linha **suspect_pages** para indicar que a página foi reparada (**event_type** = 5) ou restaurada (**event_type** = 4).  
  
    -   Se uma verificação DBCC for executada, a verificação marcará as páginas sem-erros como reparadas (**event_type** = 5) ou desalocadas (**event_type** = 7).  
  
-   **Atualizações automáticas na tabela suspect_pages**  
  
     Um parceiro de espelhamento de banco de dados ou réplica de disponibilidade AlwaysOn atualiza a tabela **suspect_pages** quando a tentativa de ler uma página de um arquivo de dados falha por uma das razões a seguir.  
  
    -   Um erro 823 causado por um erro CRC do sistema operacional.  
  
    -   Um erro 824 (dano lógico como uma página corrompida).  
  
     As ações a seguir também atualizam automaticamente as linhas na tabela **suspect_pages** .  
  
    -   DBCC CHECKDB REPAIR_ALLOW_DATA_LOSS atualiza a tabela **suspect_pages** para indicar cada página que deve ser desalocada ou reparada.  
  
    -   Uma RESTORE completa, de página ou de arquivo marca as entradas de página como restauradas.  
  
     As ações a seguir excluem automaticamente as linhas da tabela **suspect_pages** .  
  
    -   ALTER DATABASE REMOVE FILE  
  
    -   DROP DATABASE  
  
-   **Função de manutenção do administrador de banco de dados**  
  
     Os administradores de banco de dados são responsáveis por gerenciar a tabela, principalmente excluindo linhas antigas. A tabela **suspect_pages** é limitada em tamanho e, quando está cheia, os erros novos não são registrados. Para impedir que a tabela fique cheia, o administrador do banco de dados ou do sistema deve limpar manualmente as entradas antigas dessa tabela excluindo as linhas. Portanto, recomendamos que você exclua periodicamente ou arquive linhas com **event_type** restaurado ou reparado ou linhas com valor de **last_update** antigo.  
  
     Para monitorar a atividade na tabela suspect_pages, é possível usar a [Classe de evento Database Suspect Data Page](../event-classes/database-suspect-data-page-event-class.md). Às vezes, são adicionadas linhas à tabela **suspect_pages** devido a erros temporários. Contudo, se muitas linhas estiverem sendo adicionadas à tabela, talvez haja um problema com o subsistema de E/S. Se você perceber um aumento repentino no número de linhas que estão sendo adicionadas à tabela, recomendamos que investigue os possíveis problemas em seu subsistema de E/S.  
  
     Um administrador de banco de dados pode também inserir ou atualizar registros. Por exemplo, a atualização de uma linha pode ser útil quando o administrador do banco de dados sabe que uma determinada página suspeita está realmente intacta, mas quer preservar o registro por algum tempo.  
  
###  <a name="Security"></a> Segurança  
  
####  <a name="Permissions"></a> Permissões  
 Qualquer pessoa com acesso ao **msdb** pode ler os dados na tabela **suspect_pages** . Qualquer um com permissão UPDATE na tabela suspect_pages pode atualizar seus registros. Os membros da função de banco de dados fixa **db_owner** no **msdb** ou da função de servidor fixa **sysadmin** podem inserir, atualizar e excluir registros.  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-manage-the-suspectpages-table"></a>Para gerenciar a tabela suspect_pages  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDEnoversion](../../../includes/ssdenoversion-md.md)], expanda essa instância e expanda **Bancos de Dados**.  
  
2.  Expanda **Bancos de Dados do Sistema**, expanda **msdb**, expanda **Tabelas**e então expanda **Tabelas do Sistema**.  
  
3.  Expanda **dbo.suspect_pages** e clique com o botão direito do mouse em **Editar 200 Primeiras Linhas**.  
  
4.  Na janela de consulta, edite, atualize ou exclua as linhas desejadas.  
  
##  <a name="TsqlProcedure"></a> Usando o Transact-SQL  
  
#### <a name="to-manage-the-suspectpages-table"></a>Para gerenciar a tabela suspect_pages  
  
1.  Conecte-se ao [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole os exemplos a seguir na janela de consulta e clique em **Executar**. Este exemplo exclui algumas das linhas da tabela `suspect_pages` .  
  
```  
-- Delete restored, repaired, or deallocated pages.  
DELETE FROM msdb..suspect_pages  
   WHERE (event_type = 4 OR event_type = 5 OR event_type = 7);  
GO  
  
```  
  
 Este exemplo retorna as páginas incorretas na tabela `suspect_pages` .  
  
```  
-- Select nonspecific 824, bad checksum, and torn page errors.  
SELECT * FROM msdb..suspect_pages  
   WHERE (event_type = 1 OR event_type = 2 OR event_type = 3);  
GO  
  
```  
  
## <a name="see-also"></a>Consulte também  
 [DROP DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/drop-database-audit-specification-transact-sql)   
 [RESTORE &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-transact-sql)   
 [BACKUP &#40;Transact-SQL&#41;](/sql/t-sql/statements/backup-transact-sql)   
 [DBCC &#40;Transact-SQL&#41;](/sql/t-sql/database-console-commands/dbcc-transact-sql)   
 [Restaurar páginas &#40;SQL Server&#41;](restore-pages-sql-server.md)   
 [suspect_pages &#40;Transact-SQL&#41;](/sql/relational-databases/system-tables/suspect-pages-transact-sql)   
 [MSSQLSERVER_823](../errors-events/mssqlserver-823-database-engine-error.md)   
 [MSSQLSERVER_824](../errors-events/mssqlserver-824-database-engine-error.md)  
  
  
