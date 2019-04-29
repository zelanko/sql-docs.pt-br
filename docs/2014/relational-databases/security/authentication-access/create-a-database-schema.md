---
title: Criar um esquema de banco de dados | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
f1_keywords:
- sql12.swb.schemas.general.f1
helpviewer_keywords:
- creating schemas with Management Studio
- CREATE SCHEMA [Management Studio]
- database schemas
- schemas [SQL Server], creating
ms.assetid: ed2a5522-f4d2-4111-95a4-d3e1e5081739
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: 3c3747149b23c6217f321eff9d19621189b89b66
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63011983"
---
# <a name="create-a-database-schema"></a>Criar um esquema de banco de dados
  Este tópico descreve como criar um esquema no [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[tsql](../../../includes/tsql-md.md)].  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Limitações e restrições](#Restrictions)  
  
     [Segurança](#Security)  
  
-   **Para criar um esquema usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Restrictions"></a> Limitações e restrições  
  
-   O esquema novo é de propriedade de uma das seguintes entidades de segurança em nível de banco de dados: usuário de banco de dados, função de banco de dados ou função de aplicativo. Os objetos criados em um esquema são de propriedade do proprietário do esquema e têm **principal_id** NULL em **sys.objects**. A propriedade dos objetos contidos pelo esquema pode ser transferida para qualquer entidade de segurança no nível de banco de dados, mas o proprietário do esquema sempre retém a permissão CONTROL nos objetos do esquema.  
  
-   Ao criar um objeto de banco de dados, se você especificar uma entidade de segurança de domínio válida (usuário ou grupo) como proprietária do objeto, a entidade de segurança de domínio será adicionada ao banco de dados como um esquema. O novo esquema pertencerá a essa entidade de segurança de domínio.  
  
###  <a name="Security"></a> Segurança  
  
####  <a name="Permissions"></a> Permissões  
  
-   Requer a permissão CREATE SCHEMA no banco de dados.  
  
-   Para especificar outro usuário como o proprietário do esquema que está sendo criado, o chamador deve ter a permissão IMPERSONATE no usuário em questão. Se uma função de banco de dados for especificada como o proprietário, o chamador deve ter o seguinte: associação na função ou a permissão ALTER na função.  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
##### <a name="to-create-a-schema"></a>Para criar um esquema  
  
1.  No Pesquisador de Objetos, expanda a pasta **Bancos de Dados** .  
  
2.  Expanda o banco de dados no qual o novo esquema de banco de dados será criado.  
  
3.  Clique com o botão direito do mouse na pasta **Segurança** , aponte para **Novo**e selecione **Esquema**.  
  
4.  Na caixa de diálogo **Esquema – Novo** , na página **Geral** , insira um nome do novo esquema na caixa **Nome do esquema** .  
  
5.  Na caixa **Proprietário do esquema** , digite o nome de um usuário de banco de dados ou função para ser o proprietário da propriedade do esquema. Como alternativa, clique em **Pesquisar** para abrir a caixa de diálogo **Pesquisar Funções e Usuários** .  
  
6.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
### <a name="additional-options"></a>Opções adicionais  
 A caixa de diálogo **Schema- New** também oferece opções em duas páginas adicionais: **Permissões** e **Propriedades Estendidas**.  
  
-   A página **Permissões** lista todos os protegíveis e as permissões possíveis nesses protegíveis que podem ser concedidos ao logon.  
  
-   A página **Propriedades estendidas** permite adicionar propriedades personalizadas a usuários de banco de dados.  
  
##  <a name="TsqlProcedure"></a> Usando o Transact-SQL  
  
#### <a name="to-create-a-schema"></a>Para criar um esquema  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDE](../../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**.  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    -- Creates the schema Sprockets owned by Annik that contains table NineProngs.   
    -- The statement grants SELECT to Mandar and denies SELECT to Prasanna.  
  
    CREATE SCHEMA Sprockets AUTHORIZATION Annik  
        CREATE TABLE NineProngs (source int, cost int, partnumber int)  
        GRANT SELECT ON SCHEMA::Sprockets TO Mandar  
        DENY SELECT ON SCHEMA::Sprockets TO Prasanna;  
    GO  
    ```  
  
 Para obter mais informações, veja [CREATE SCHEMA &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-schema-transact-sql).  
  
  
