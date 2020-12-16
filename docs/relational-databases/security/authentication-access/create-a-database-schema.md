---
title: Criar um esquema de banco de dados | Microsoft Docs
description: Saiba como criar um esquema em um SQL Server usando o SQL Server Management Studio ou o Transact-SQL, incluindo limitações e restrições.
ms.custom: ''
ms.date: 07/05/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
f1_keywords:
- sql13.swb.schemas.general.f1
helpviewer_keywords:
- creating schemas with Management Studio
- CREATE SCHEMA [Management Studio]
- database schemas
- schemas [SQL Server], creating
ms.assetid: ed2a5522-f4d2-4111-95a4-d3e1e5081739
author: VanMSFT
ms.author: vanto
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: bfb3ee2b9dee35b5154c019f47a25570b6f7eeae
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97468577"
---
# <a name="create-a-database-schema"></a>Criar um esquema de banco de dados
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
  Este tópico descreve como criar um esquema no [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[tsql](../../../includes/tsql-md.md)].  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> Limitações e restrições  
  
-   O esquema novo é de propriedade de uma das seguintes entidades de segurança em nível de banco de dados: usuário de banco de dados, função de banco de dados ou função de aplicativo. Os objetos criados em um esquema são de propriedade do proprietário do esquema e têm **principal_id** NULL em **sys.objects**. A propriedade dos objetos contidos pelo esquema pode ser transferida para qualquer entidade de segurança no nível de banco de dados, mas o proprietário do esquema sempre retém a permissão CONTROL nos objetos do esquema.  
  
-   Ao criar um objeto de banco de dados, se você especificar uma entidade de segurança de domínio válida (usuário ou grupo) como proprietária do objeto, a entidade de segurança de domínio será adicionada ao banco de dados como um esquema. O novo esquema pertence a essa entidade de segurança de domínio.  
  
###  <a name="security"></a><a name="Security"></a> Segurança  
  
####  <a name="permissions"></a><a name="Permissions"></a> Permissões  
  
-   Requer a permissão CREATE SCHEMA no banco de dados.  
  
-   Para especificar outro usuário como o proprietário do esquema que está sendo criado, o chamador deve ter a permissão IMPERSONATE no usuário em questão. Se uma função de banco de dados for especificada como o proprietário, o chamador deverá atender a um dos critérios a seguir: associação na função ou a permissão ALTER na função.  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
##### <a name="to-create-a-schema"></a>Para criar um esquema  
  
1.  No Pesquisador de Objetos, expanda a pasta **Bancos de Dados** .  
  
2.  Expanda o banco de dados no qual o novo esquema de banco de dados será criado.  
  
3.  Clique com o botão direito do mouse na pasta **Segurança** , aponte para **Novo** e selecione **Esquema**.  
  
4.  Na caixa de diálogo **Esquema – Novo** , na página **Geral** , insira um nome do novo esquema na caixa **Nome do esquema** .  
  
5.  Na caixa **Proprietário do esquema** , digite o nome de um usuário de banco de dados ou função para ser o proprietário da propriedade do esquema. Como alternativa, clique em **Pesquisar** para abrir a caixa de diálogo **Pesquisar Funções e Usuários** .  
  
6.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  

> [!NOTE]
> Uma caixa de diálogo não aparecerá se você estiver criando um esquema usando o SSMS em um **Banco de Dados SQL do Azure** ou **Azure Synapse Analytics**. Você precisará executar a Instrução T-SQL Criar Modelo de Esquema que é gerada.
  
### <a name="additional-options"></a>Opções adicionais  
 A caixa de diálogo **Schema- New** também oferece opções em duas páginas adicionais: **Permissões** e **Propriedades Estendidas**.  
  
-   A página **Permissões** lista todos os protegíveis e as permissões possíveis nesses protegíveis que podem ser concedidos ao logon.  
  
-   A página **Propriedades estendidas** permite adicionar propriedades personalizadas a usuários de banco de dados.  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Usando o Transact-SQL  
  
#### <a name="to-create-a-schema"></a>Para criar um esquema  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDE](../../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  O exemplo a seguir cria um esquema denominado `Chains` e, em seguida, cria uma tabela denominada `Sizes`.  
    ```sql  
    CREATE SCHEMA Chains;
    GO
    CREATE TABLE Chains.Sizes (ChainID int, width dec(10,2));
    ```

4.  Opções adicionais podem ser executadas em uma única instrução. O exemplo a seguir cria o esquema `Sprockets` pertencente a Annik que contém a tabela `NineProngs`. A instrução concede `SELECT` para Mandar e nega `SELECT` a Prasanna.  

    ```sql  
    CREATE SCHEMA Sprockets AUTHORIZATION Annik  
        CREATE TABLE NineProngs (source int, cost int, partnumber int)  
        GRANT SELECT ON SCHEMA::Sprockets TO Mandar  
        DENY SELECT ON SCHEMA::Sprockets TO Prasanna;  
    GO  
    ```  
5. Execute a instrução a seguir, para exibir os esquemas neste banco de dados:

   ```sql
   SELECT * FROM sys.schemas;
   ```

 Para obter mais informações, veja [CREATE SCHEMA &#40;Transact-SQL&#41;](../../../t-sql/statements/create-schema-transact-sql.md).  
  
  
