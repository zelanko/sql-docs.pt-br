---
title: Habilitar ou desabilitar um guia de plano | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- plan guides [SQL Server], disabling
- enabling plan guides
- plan guides [SQL Server], enabling
- disabling plan guides
ms.assetid: b00ab550-5308-4cb8-8330-483cd1d25654
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 34f88b49dd0c7ef93d586c404a212a79a7ec5243
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47834900"
---
# <a name="enable-or-disable-a-plan-guide"></a>Habilitar ou desabilitar um guia de plano
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Você pode desabilitar e habilitar guias de plano no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[tsql](../../includes/tsql-md.md)]. Um único ou todos os guias de plano de um banco de dados podem ser habilitados ou desabilitados.  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Limitações e restrições](#Restrictions)  
  
     [Segurança](#Security)  
  
-   **Para desabilitar e habilitar guias de plano usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Restrictions"></a> Limitações e restrições  
  
-   A tentativa de cancelar ou modificar uma função, procedimento armazenado ou gatilho DML referenciado por um guia de plano, habilitado ou desabilitado, provoca um erro. Sempre verifique se há dependências antes de cancelar ou modificar qualquer um dos objetos listados acima.  
  
-   A desabilitação de um guia de plano desabilitado ou a habilitação de um guia de plano habilitado não tem nenhum efeito e ocorre sem erro.  
  
###  <a name="Security"></a> Segurança  
  
####  <a name="Permissions"></a> Permissões  
 A habilitação ou desabilitação de um guia de plano OBJECT exige a permissão ALTER no objeto (por exemplo: função, procedimento armazenado) que é referenciado pelo guia de plano. Todos os outros guias de plano requerem permissão ALTER DATABASE.  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-disable-or-enable-a-plan-guide"></a>Para habilitar ou desabilitar um guia de plano  
  
1.  Clique no sinal de adição para expandir o banco de dados no qual você deseja desabilitar ou habilitar um guia de plano e clique no sinal de adição para expandir a pasta **Programação** .  
  
2.  Clique no sinal de adição para expandir a pasta **Guias de Plano** .  
  
3.  Clique com o botão direito do mouse no guia de plano que você deseja habilitar ou desabilitar e selecione **Habilitar** ou **Desabilitar**.  
  
4.  Na caixa de diálogo **Desabilitar Guia de Plano** ou **Habilitar Guia de Plano** , verifique se a ação escolhida foi bem-sucedida e clique em **Fechar**.  
  
#### <a name="to-disable-or-enable-all-plan-guides-in-a-database"></a>Para desabilitar ou habilitar todos os guias de plano de um banco de dados  
  
1.  Clique no sinal de adição para expandir o banco de dados no qual você deseja desabilitar ou habilitar um guia de plano e clique no sinal de adição para expandir a pasta **Programação** .  
  
2.  Clique com o botão direito do mouse na pasta **Guias de Plano** e selecione **Habilitar Tudo** ou **Desabilitar Tudo**.  
  
3.  Na caixa de diálogo **Desabilitar Todos os Guias de Plano** ou **Habilitar Todos os Guias de Plano** , verifique se a ação escolhida foi bem-sucedida e clique em **Fechar**.  
  
##  <a name="TsqlProcedure"></a> Usando o Transact-SQL  
  
#### <a name="to-disable-or-enable-a-plan-guide"></a>Para habilitar ou desabilitar um guia de plano  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**.  
  
    ```  
    --Create a procedure on which to define the plan guide.  
    IF OBJECT_ID(N'Sales.GetSalesOrderByCountry', N'P') IS NOT NULL  
        DROP PROCEDURE Sales.GetSalesOrderByCountry;  
    GO  
    CREATE PROCEDURE Sales.GetSalesOrderByCountry   
        (@Country nvarchar(60))  
    AS  
    BEGIN  
        SELECT *  
        FROM Sales.SalesOrderHeader AS h   
        INNER JOIN Sales.Customer AS c ON h.CustomerID = c.CustomerID  
        INNER JOIN Sales.SalesTerritory AS t ON c.TerritoryID = t.TerritoryID  
        WHERE t.CountryRegionCode = @Country;  
    END  
    GO  
    --Create the plan guide.  
    EXEC sp_create_plan_guide N'Guide3',  
        N'SELECT *  
        FROM Sales.SalesOrderHeader AS h   
        INNER JOIN Sales.Customer AS c ON h.CustomerID = c.CustomerID  
        INNER JOIN Sales.SalesTerritory AS t ON c.TerritoryID = t.TerritoryID  
        WHERE t.CountryRegionCode = @Country',  
        N'OBJECT',  
        N'Sales.GetSalesOrderByCountry',  
        NULL,  
        N'OPTION (OPTIMIZE FOR (@Country = N''US''))';  
    --Disable the plan guide.  
    EXEC sp_control_plan_guide N'DISABLE', N'Guide3';  
    GO  
    --Enable the plan guide.  
    EXEC sp_control_plan_guide N'ENABLE', N'Guide3';  
    GO  
  
    ```  
  
#### <a name="to-disable-or-enable-all-plan-guides-in-a-database"></a>Para desabilitar ou habilitar todos os guias de plano de um banco de dados  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**.  
  
    ```  
    --Disable all plan guides in the database.  
    EXEC sp_control_plan_guide N'DISABLE ALL';  
    GO  
    --Enable all plan guides in the database.  
    EXEC sp_control_plan_guide N'ENABLE ALL';  
    GO  
  
    ```  
  
 Para obter mais informações, veja [sp_control_plan_guide &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-control-plan-guide-transact-sql.md).  
  
  
