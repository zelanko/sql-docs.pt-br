---
description: Desabilitar índices e restrições
title: Desabilitar índices e restrições | Microsoft Docs
ms.custom: ''
ms.date: 02/17/2017
ms.prod: sql
ms.prod_service: table-view-index, sql-database
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
f1_keywords:
- sql13.swb.disableindexes.f1
helpviewer_keywords:
- disabled indexes [SQL Server], index operations
- nonclustered indexes [SQL Server], disabling
- disabled indexes [SQL Server], guidelines
- clustered indexes, disabling
- constraints [SQL Server], disabling
- disabled indexes [SQL Server], viewing
- FOREIGN KEY constraints, disabling
- statistical information [SQL Server], indexes
- index disabling [SQL Server]
- indexed views [SQL Server], disabled indexes
ms.assetid: 2198f1af-fa44-47e9-92df-f4fde322ba18
author: MikeRayMSFT
ms.author: mikeray
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: d06bb8ed9286c22a2381f31a36814ea305642365
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97481167"
---
# <a name="disable-indexes-and-constraints"></a>Desabilitar índices e restrições
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  Este tópico descreve como desabilitar um índice ou restrições no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[tsql](../../includes/tsql-md.md)]. A desabilitação de um índice impede que o usuário o acesse, e que índices clusterizados acessem os dados da tabela subjacente. A definição do índice permanece nos metadados e as estatísticas do índice são mantidas em índices não clusterizados. A desabilitação de um índice não clusterizado ou clusterizado em uma exibição exclui fisicamente os dados do índice. A desabilitação de um índice clusterizado em uma tabela impede o acesso aos dados; os dados ainda permanecem na tabela, mas ficam indisponíveis para operações DML (linguagem de manipulação de dados) até que o índice seja descartado ou recriado.  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Limitações e restrições](#Restrictions)  
  
     [Segurança](#Security)  
  
-   **Para desabilitar um índice usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> Limitações e restrições  
  
-   O índice não é mantido enquanto estiver desabilitado.  
  
-   O otimizador de consulta não considera o índice desabilitado ao criar planos de execução de consulta. As consultas que referenciam o índice desabilitado com uma dica de tabela também falham.  
  
-   Você não pode criar um índice que usa o mesmo nome que um índice desabilitado existente.  
  
-   Um índice desabilitado pode ser cancelado.  
  
-   Ao desabilitar um índice exclusivo, a restrição PRIMARY KEY ou UNIQUE e todas as restrições FOREIGN KEY que referenciam as colunas indexadas de outras tabelas também são desabilitadas. Ao desabilitar um índice clusterizado, todas as restrições FOREIGN KEY de entrada e saída na tabela subjacente também são desabilitadas. Os nomes das restrições são listados em uma mensagem de aviso quando o índice é desabilitado. Depois de recompilar o índice, todas as restrições devem ser habilitadas manualmente usando a instrução ALTER TABLE CHECK CONSTRAINT.  
  
-   Os índices não clusterizados são desabilitados automaticamente quando o índice clusterizado associado é desabilitado. Eles não podem ser habilitados até o índice clusterizado na tabela ou exibição ser habilitado ou o índice clusterizado na tabela for cancelado. Os índices não clusterizados devem ser explicitamente habilitados, a menos que o índice clusterizado tenha sido habilitado usando a instrução ALTER INDEX ALL REBUILD.  
  
-   A instrução ALTER INDEX ALL REBUILD recompila e habilita todos os índices desabilitados na tabela, com exceção dos índices desabilitados nas exibições. Os índices em exibições devem ser habilitados em uma instrução ALTER INDEX ALL REBUILD separada.  
  
-   Desabilitar um índice clusterizado em uma tabela também desabilita todos os índices clusterizados e não clusterizados em exibições que referenciam essa tabela. Esses índices devem ser recompilados da mesma maneira que aqueles da tabela referenciada.  
  
-   As linhas de dados do índice clusterizado desabilitado não podem ser acessadas, exceto para cancelar ou recompilar o índice clusterizado.  
  
-   Você pode recompilar um índice não clusterizado desabilitado online quando a tabela não tiver um índice clusterizado desabilitado. Porém, sempre precisará recompilar um índice clusterizado desabilitado offline se você usar a instrução ALTER INDEX REBUILD ou CREATE INDEX WITH DROP_EXISTING. Para obter mais informações sobre operações de índice online, consulte [Executar operações de índice online](../../relational-databases/indexes/perform-index-operations-online.md).  
  
-   A instrução CREATE STATISTICS não pode ser executada com êxito em uma tabela que tem um índice clusterizado desabilitado.  
  
-   A opção de banco de dados AUTO_CREATE_STATISTICS cria novas estatísticas em uma coluna quando o índice é desabilitado e existem as seguintes condições:  
  
    -   AUTO_CREATE_STATISTICS é definido como ON  
  
    -   Não há nenhuma estatística existente para a coluna.  
  
    -   As estatísticas são exigidas durante a otimização da consulta.  
  
-   Se um índice clusterizado for desabilitado, [DBCC CHECKDB](../../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md) não poderá retornar informações sobre a tabela subjacente. Em vez disso, a instrução reportará que o índice clusterizado está desabilitado. [DBCC INDEXDEFRAG](../../t-sql/database-console-commands/dbcc-indexdefrag-transact-sql.md) não pode ser usado para desfragmentar um índice desabilitado; a instrução falha com uma mensagem de erro. Você pode usar [DBCC DBREINDEX](../../t-sql/database-console-commands/dbcc-dbreindex-transact-sql.md) para recriar um índice desabilitado.  
  
-   Criar um novo índice clusterizado habilita índices não clusterizados previamente desabilitados. Para obter mais informações, consulte [Enable Indexes and Constraints](../../relational-databases/indexes/enable-indexes-and-constraints.md).  
  
###  <a name="security"></a><a name="Security"></a> Segurança  
  
####  <a name="permissions"></a><a name="Permissions"></a> Permissões  
 Para executar ALTER INDEX, no mínimo, a permissão ALTER na tabela ou exibição é necessária.  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-disable-an-index"></a>Para desabilitar um índice  
  
1.  No Pesquisador de Objetos, clique no sinal de adição ao lado do banco de dados que contém a tabela na qual você deseja desabilitar um índice.  
  
2.  Clique no sinal de adição para expandir a pasta **Tabelas** .  
  
3.  Clique no sinal de adição ao lado da tabela na qual você deseja desabilitar um índice.  
  
4.  Clique no sinal de adição para expandir a pasta **Índices** .  
  
5.  Clique com o botão direito do mouse no índice a ser desabilitado e selecione **Desabilitar**.  
  
6.  Na caixa de diálogo **Desabilitar Índices** , verifique se o índice correto está na grade **Índices a serem desabilitados** e clique em **OK**.  
  
#### <a name="to-disable-all-indexes-on-a-table"></a>Para desabilitar todos os índices de uma tabela  
  
1.  No Pesquisador de Objetos, clique no sinal de adição para expandir o banco de dados que contém a tabela na qual você deseja desabilitar os índices.  
  
2.  Clique no sinal de adição para expandir a pasta **Tabelas** .  
  
3.  Clique no sinal de adição para expandir a tabela na qual você deseja desabilitar os índices.  
  
4.  Clique com o botão direito do mouse na pasta **Índices** e selecione **Desabilitar Todos**.  
  
5.  Na caixa de diálogo **Desabilitar Índices** , verifique se os índices corretos estão na grade **Índices a serem desabilitados** e clique em **OK**. Para remover um índice da grade **Índices a serem desabilitados** , selecione o índice e pressione a tecla Delete.  
  
 As informações a seguir estão disponíveis na caixa de diálogo **Desabilitar Índices** :  
  
 **Nome do Índice**  
 Exibe o nome do índice. Durante a execução, esta coluna exibe também um ícone que representa o status.  
  
 **Nome da tabela**  
 Exibe o nome da tabela ou exibição na qual o índice foi criado.  
  
 **Tipo de Índice**  
 Exibe o tipo de índice: **Clusterizado**, **Não clusterizado**, **Espacial** ou **XML**.  
  
 **Status**  
 Exibe o status atual da operação de desabilitação. Os possíveis valores após a execução são:  
  
-   Em branco  
  
     Antes de execução o **Status** fica em branco.  
  
-   **Em Andamento**  
  
     A desabilitação dos índices foi iniciada mas não está concluída.  
  
-   **Êxito**  
  
     A operação de desabilitação foi concluída com êxito.  
  
-   **Erro**  
  
     Foi encontrado um erro durante a operação de desabilitação do índice e a operação e a operação não foi concluída com êxito.  
  
-   **Parado**  
  
     A desabilitação do índice não foi concluída com êxito porque o usuário interrompeu a operação.  
  
 **Message**  
 Fornece o texto de mensagens de erro durante a operação de desabilitação. Durante a execução, os erros aparecem como hiperlinks. O texto dos hiperlinks descreve o corpo do erro. A coluna **Mensagem** raramente é grande o suficiente para acomodar o texto de mensagem completo. Há dois modos para obter o texto completo:  
  
-   Mova o ponteiro de mouse sobre a célula de mensagem para exibir uma dica de ferramenta com o texto do erro.  
  
-   Clique no hiperlink para exibir uma caixa de diálogo que exibe o erro completo.  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Usando o Transact-SQL  
  
#### <a name="to-disable-an-index"></a>Para desabilitar um índice  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**.  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    -- disables the IX_Employee_OrganizationLevel_OrganizationNode index  
    -- on the HumanResources.Employee table  
    ALTER INDEX IX_Employee_OrganizationLevel_OrganizationNode ON HumanResources.Employee  
    DISABLE;  
    ```  
  
#### <a name="to-disable-all-indexes-on-a-table"></a>Para desabilitar todos os índices de uma tabela  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**.  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    -- Disables all indexes on the HumanResources.Employee table.  
    ALTER INDEX ALL ON HumanResources.Employee  
    DISABLE;  
    ```  
  
 Para obter mais informações, consulte [ALTER INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md).  
  
  
