---
title: Mover um índice existente para outro grupo de arquivos | Microsoft Docs
ms.custom: ''
ms.date: 02/17/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- moving tables
- switching filegroups for index
- moving indexes
- indexes [SQL Server], moving
- filegroups [SQL Server], switching
ms.assetid: 167ebe77-487d-4ca8-9452-4b2c7d5cb96e
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 3da52bc9b6014f5a2a553fc24e844299dd4ab4e8
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/28/2018
ms.locfileid: "52515777"
---
# <a name="move-an-existing-index-to-a-different-filegroup"></a>Mover um índice existente para um grupo de arquivos diferente
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  Este tópico descreve como mover um índice existente do seu grupo de arquivos atual para um grupo de arquivos diferente no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Limitações e restrições](#Restrictions)  
  
     [Segurança](#Security)  
  
-   **Para mover um índice existente para um grupo de arquivos diferente, usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Restrictions"></a> Limitações e restrições  
  
-   Se uma tabela tiver um índice clusterizado, mover o índice clusterizado a um novo grupo de arquivos moverá a tabela àquele grupo de arquivos.  
  
-   Você não pode mover índices criados usando uma restrição UNIQUE ou PRIMARY KEY usando [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]. Para mover esses índices, use a instrução [CREATE INDEX](../../t-sql/statements/create-index-transact-sql.md) com a opção (DROP_EXISTING=ON) no [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
###  <a name="Security"></a> Segurança  
  
####  <a name="Permissions"></a> Permissões  
 Requer a permissão ALTER na tabela ou exibição. O usuário deve ser membro da função de servidor fixa **sysadmin** ou das funções de banco de dados fixas **db_ddladmin** e **db_owner** .  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-move-an-existing-index-to-a-different-filegroup-using-table-designer"></a>Para mover um índice existente para um grupo de arquivos diferente, usando o Designer de Tabelas  
  
1.  No Pesquisador de Objetos, clique no sinal de adição para expandir a tabela que contém o índice que você quer mover.  
  
2.  Clique no sinal de adição para expandir a pasta **Tabelas** .  
  
3.  Clique com o botão direito do mouse na tabela que contém o índice que você quer mover e selecione **Design**.  
  
4.  No menu **Designer de Tabela** , clique em **Índices/Chaves**.  
  
5.  Selecione o índice a ser movido.  
  
6.  Na grade principal, expanda **Especificação de Espaço de Dados**.  
  
7.  Selecione **Nome do Esquema de Partição ou Grupo de Arquivos** e selecione da lista o grupo de arquivos ou esquema de partição para onde você deseja mover o índice.  
  
8.  Clique em **Fechar**.  
  
9. No menu **Arquivo** , selecione **Salvar**_table_name_.  
  
#### <a name="to-move-an-existing-index-to-a-different-filegroup-in-object-explorer"></a>Para mover um índice existente a um grupo de arquivos diferente no Pesquisador de Objetos  
  
1.  No Pesquisador de Objetos, clique no sinal de adição para expandir a tabela que contém o índice que você quer mover.  
  
2.  Clique no sinal de adição para expandir a pasta **Tabelas** .  
  
3.  Clique no sinal de adição para expandir a tabela que contém o índice a ser movido.  
  
4.  Clique no sinal de adição para expandir a pasta **Índices** .  
  
5.  Clique com o botão direito do mouse no índice a ser movido e selecione **Propriedades**.  
  
6.  Em **Selecione uma página**, selecione **Armazenamento**.  
  
7.  Selecione o grupo de arquivos para onde mover o índice.  
  
     Se a tabela ou o índice for particionado, selecione o esquema de partição no qual mover o índice. Para obter mais informações sobre índices particionados, consulte [Partitioned Tables and Indexes](../../relational-databases/partitions/partitioned-tables-and-indexes.md).  
  
     Se você estiver movendo um índice clusterizado, poderá usar o processamento online. O processamento online permite o acesso simultâneo de usuários aos dados subjacentes e a índices não clusterizados durante a operação de índice. Para obter mais informações, consulte [Perform Index Operations Online](../../relational-databases/indexes/perform-index-operations-online.md).  
  
     Em computadores multiprocessadores que usam o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], é possível configurar o número de processadores usados para executar a instrução de índice especificando um grau máximo de valor de paralelismo. O recurso de operações de índice paralelas não está disponível em todas as edições do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obter uma lista dos recursos com suporte nas edições do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], consulte Recursos com suporte nas edições do SQL Server 2016. Para obter mais informações sobre as operações indexadas paralelas, consulte [Configurar operações de índice paralelo](../../relational-databases/indexes/configure-parallel-index-operations.md).  
  
8.  Clique em **OK**.  
  
 As informações a seguir estão disponíveis na página **Armazenamento** da caixa de diálogo **Propriedades do Índice –** *index_name*:  
  
 **Grupo de arquivos**  
 Armazena o índice no grupo de arquivos especificado. A lista exibe apenas grupos de arquivos padrão (linha). A seleção de lista padrão é o grupo de arquivos PRIMARY do banco de dados.  
  
 **Grupos de Arquivos do Fluxo de Arquivos**  
 Especifica o grupo de arquivos para obter dados de FILESTREAM. Essa lista exibe apenas grupos de arquivos FILESTREAM. A seleção de lista padrão é o grupo de arquivos PRIMARY FILESTREAM.  
  
 **Esquema de partição**  
 Armazena o índice em um esquema de partição. Clicando em **Esquema de Partição** a grade abaixo é habilitada. A seleção de lista padrão é o esquema de partição usado para armazenar os dados de tabela. Ao selecionar um esquema de partição diferente na lista, a informações na grade é atualizada.  
  
 A opção de esquema de partição fica indisponível se não houver nenhum esquema de partição no banco de dados.  
  
 **Esquema de Partição do Fluxo de Arquivos**  
 Especifica o esquema de partição para dados FILESTREAM. O esquema de partição deve ser simétrico com o esquema especificado na opção **Esquema de partição** .  
  
 Se a tabela não for particionada, o campo fica em branco.  
  
 **Parâmetro do Esquema de Partição**  
 Exibe o nome da coluna que participa do esquema de partição.  
  
 **Coluna de tabela**  
 Selecione a tabela ou exiba para mapear para o esquema de partição.  
  
 **Tipo de dados da coluna**  
 Exibe informações de tipo de dados sobre a coluna.  
  
> [!NOTE]  
>  Se a coluna de tabela for uma coluna computada, **Tipo de Dados da Coluna** exibirá "coluna computada."  
  
 **Permitir o processamento online de instruções DML ao mover o índice**  
 Permite aos usuários acessar a tabela subjacente ou dados de índice clusterizado associados a quaisquer índices não clusterizados durante a operação de índice.  
  
> [!NOTE]  
>  Esta opção não está disponível para índices XML ou se o índice for um índice clusterizadoF desabilitado.  
  
 **Definir grau máximo de paralelismo**  
 Limita o número de processadores a serem usados durante execução do plano paralelo. O valor padrão, 0, usa o número real de CPUs disponíveis. A definição do valor como 1 elimina a geração em plano paralelo; a definição do valor como um número maior que 1 restringe o número máximo de processadores usados por uma única execução da consulta. Esta opção ficará disponível apenas se a caixa de diálogo estiver no estado **Recriar** ou **Recriar** .  
  
> [!NOTE]  
>  Se um valor maior que o número de CPUs disponíveis for especificado, será usado o número real de CPUs disponíveis.  
  
##  <a name="TsqlProcedure"></a> Usando o Transact-SQL  
  
#### <a name="to-move-an-existing-index-to-a-different-filegroup"></a>Para mover um índice existente para um grupo de arquivos diferente  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**.  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    -- Creates the TransactionsFG1 filegroup on the AdventureWorks2012 database  
    ALTER DATABASE AdventureWorks2012  
    ADD FILEGROUP TransactionsFG1;  
    GO  
    /* Adds the TransactionsFG1dat3 file to the TransactionsFG1 filegroup. Please note that you will have to change the filename parameter in this statement to execute it without errors.  
    */  
    ALTER DATABASE AdventureWorks2012   
    ADD FILE   
    (  
        NAME = TransactionsFG1dat3,  
        FILENAME = 'C:\Program Files\Microsoft SQL Server\MSSQL13\MSSQL\DATA\TransactionsFG1dat3.ndf',  
        SIZE = 5MB,  
        MAXSIZE = 100MB,  
        FILEGROWTH = 5MB  
    )  
    TO FILEGROUP TransactionsFG1;  
    GO  
    /*Creates the IX_Employee_OrganizationLevel_OrganizationNode index  
      on the TransactionsPS1 filegroup and drops the original IX_Employee_OrganizationLevel_OrganizationNode index.  
    */  
    CREATE NONCLUSTERED INDEX IX_Employee_OrganizationLevel_OrganizationNode  
        ON HumanResources.Employee (OrganizationLevel, OrganizationNode)  
        WITH (DROP_EXISTING = ON)  
        ON TransactionsFG1;  
    GO  
    ```  
  
 Para obter mais informações, consulte [CREATE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md).  
  
  
