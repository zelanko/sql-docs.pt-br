---
title: Reduzir um arquivo | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
f1_keywords:
- sql12.swb.shrinkfile.f1
helpviewer_keywords:
- shrinking files
- decreasing file size
- databases [SQL Server], shrinking
- reducing file size
- size [SQL Server], files
- file size [SQL Server]
ms.assetid: ce5c8798-c039-4ab2-81e7-90a8d688b893
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: f567c92632e99bef38fc1a6eb7a0179929f467c0
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52822540"
---
# <a name="shrink-a-file"></a>Reduzir um arquivo
  Este tópico descreve como reduzir um arquivo de dados ou de log no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 A redução de arquivos de dados recupera espaço com a movimentação de páginas de dados do final do arquivo para o espaço desocupado mais próximo à frente do arquivo. Quando espaço livre suficiente é criado no final do arquivo, as páginas de dados no final do arquivo podem ser desalocadas e retornadas para o sistema de arquivos.  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Limitações e restrições](#Restrictions)  
  
     [Recomendações](#Recommendations)  
  
     [Segurança](#Security)  
  
-   **Para reduzir um arquivo de dados ou de log, usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Restrictions"></a> Limitações e Restrições  
  
-   O arquivo de dados principal não pode ser menor que o arquivo principal no banco de dados modelo.  
  
###  <a name="Recommendations"></a> Recomendações  
  
-   Os dados movidos para reduzir um arquivo podem ser espalhados para qualquer local disponível no arquivo. Isso provoca uma fragmentação do índice e pode reduzir a velocidade do desempenho de consultas que pesquisam um intervalo do índice. Para eliminar a fragmentação, considere a recompilação dos índices no arquivo após a redução.  
  
###  <a name="Security"></a> Segurança  
  
####  <a name="Permissions"></a> Permissões  
 Exige associação à função de servidor fixa **sysadmin** ou à função de banco de dados fixa **db_owner** .  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-shrink-a-data-or-log-file"></a>Para reduzir um arquivo de dados ou de log  
  
1.  No Pesquisador de Objetos, conecte-se a uma instância do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] e expanda-a.  
  
2.  Expanda **Bancos de Dados** e clique com o botão direito do mouse no banco de dados que deseja reduzir.  
  
3.  Aponte para **Tarefas**, aponte para **Reduzir**e, então, clique em **Arquivos**.  
  
     **Backup de banco de dados**  
     Exibe o nome do banco de dados selecionado.  
  
     **Tipo de arquivo**  
     Seleciona o tipo de arquivo para o arquivo. As escolhas disponíveis são arquivos de **Dados** e de **Log** . A seleção padrão é **Dados**. Selecionar um tipo diferente de grupo de arquivos altera as seleções nos outros campos de acordo o tipo selecionado.  
  
     **Grupo de arquivos**  
     Selecione um grupo de arquivos da lista de grupos de arquivos associado com o **Tipo de arquivo** selecionado acima. Selecionar um grupo de arquivos diferente altera as seleções nos outros campos de acordo o grupo selecionado.  
  
     **Nome do arquivo**  
     Selecione um arquivo da lista de arquivos disponíveis do grupo de arquivos e tipo de arquivos selecionados.  
  
     **Local**  
     Exibe o caminho completo para o arquivo atualmente selecionado. O caminho não é editável, mas pode ser copiado para a área de transferência.  
  
     **Espaço alocado no momento**  
     Para arquivos de dados, exibe o espaço alocado no momento. Para arquivos de log, exibe o espaço alocado no momento computado da saída de DBCC SQLPERF(LOGSPACE).  
  
     **Espaço livre disponível**  
     Para arquivos de dados, exibe o espaço livre disponível no momento computado da saída de DBCC SHOWFILESTATS(fileid). Para arquivos de log, exibe o espaço livre disponível no momento computado da saída de DBCC SQLPERF(LOGSPACE).  
  
     **Liberar espaço não utilizado**  
     Faz com que qualquer espaço não utilizado nos arquivos seja liberado para o sistema operacional e reduz o arquivo para a última extensão alocada, reduzindo o tamanho do arquivo sem mover nenhum dado. Não é feita nenhuma tentativa para realocar linhas em páginas não alocadas.  
  
     **Reorganizar páginas antes de liberar espaço não utilizado**  
     Equivale a executar DBCC SHRINKFILE especificando o tamanho do arquivo de destino. Quando essa opção é selecionada, o usuário deve especificar um tamanho de arquivo de destino na **Reduzir arquivo a** .  
  
     **Reduzir arquivo a**  
     Especifica o tamanho do arquivo de destino para a operação de redução. O tamanho não pode ser menor do que o espaço alocado no momento nem mais do que a extensão total alocada para o arquivo. Digitar um valor abaixo do mínimo ou além do máximo fará com que ele reverta ao mínimo ou ao máximo assim que o foco for alterado ou quando você clicar em qualquer botão da barra de ferramentas.  
  
     **Esvaziar o arquivo migrando os dados para outros arquivos do mesmo grupo**  
     Migra todos os dados do arquivo especificado. Essa opção permite descartar o arquivo usando a instrução ALTER DATABASE. Essa opção é equivalente a executar DBCC SHRINKFILE com a opção de EMPTYFILE.  
  
4.  Selecione o tipo e o nome do arquivo.  
  
5.  Opcionalmente, marque a caixa de seleção **Liberar espaço não utilizado** .  
  
     Selecionar essa opção faz com que qualquer espaço não usado no arquivo seja liberado para o sistema operacional e reduz o arquivo à última extensão alocada. Isso reduz o tamanho do arquivo sem mover quaisquer dados.  
  
6.  Opcionalmente, marque a caixa de seleção **Reorganizar arquivos antes de liberar o espaço não utilizado** . Se isso for selecionado, o valor **Reduzir arquivo para** deve ser especificado. Por padrão, a opção fica desmarcada.  
  
     Selecionar essa opção faz com que qualquer espaço não usado no arquivo seja liberado para o sistema operacional e tenta realocar linhas a páginas não alocadas.  
  
7.  Opcionalmente, insira a porcentagem máxima de espaço livre a ser deixado no arquivo de banco de dados após o banco de dados ter sido reduzido. Os valores permitidos estão entre 0 e 99. Essa opção só está disponível quando **Reorganizar arquivos antes de liberar o espaço não utilizado** estiver habilitada.  
  
8.  Opcionalmente, marque a caixa de seleção **Esvaziar arquivo migrando os dados para outros arquivos no mesmo grupo de arquivos** .  
  
     Selecionar essa opção move todos os dados do arquivo especificado para outros arquivos no grupo de arquivos. O arquivo vazio pode, então, ser excluído. Essa opção é igual a executar DBCC SHRINKFILE com a opção de EMPTYFILE.  
  
9. Clique em **OK**.  
  
##  <a name="TsqlProcedure"></a> Usando Transact-SQL  
  
#### <a name="to-shrink-a-data-or-log-file"></a>Para reduzir um arquivo de dados ou de log  
  
1.  Conecte-se ao [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**. Este exemplo usa [DBCC SHRINKFILE](/sql/t-sql/database-console-commands/dbcc-shrinkfile-transact-sql) para reduzir o tamanho de um arquivo de dados denominado `DataFile1` no banco de dados `UserDB` para 7 MB.  
  
 [!code-sql[DBCC#DBCC_SHRINKFILE1](../../snippets/tsql/SQL14/tsql/dbcc/transact-sql/dbcc_other.sql#dbcc_shrinkfile1)]  
  
## <a name="see-also"></a>Consulte também  
 [DBCC SHRINKDATABASE &#40;Transact-SQL&#41;](/sql/t-sql/database-console-commands/dbcc-shrinkdatabase-transact-sql)   
 [Reduzir um banco de dados](shrink-a-database.md)   
 [Excluir arquivos de dados ou de log de um banco de dados](delete-data-or-log-files-from-a-database.md)   
 [sys.databases &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql)   
 [sys.database_files &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-database-files-transact-sql)  
  
  
