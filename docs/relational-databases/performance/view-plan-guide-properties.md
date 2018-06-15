---
title: Exibir propriedades de guia de plano | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: performance
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql13.swb.planguideprop.general.f1
helpviewer_keywords:
- plan guides [SQL Server], view plan guide properties
- viewing plan guide properties
ms.assetid: 8c0d2f39-59c1-4168-a649-65473f6a771b
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: a2f970aa633244f5c91a3b90fa51eca6a5e32c8a
ms.sourcegitcommit: ee661730fb695774b9c483c3dd0a6c314e17ddf8
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/19/2018
ms.locfileid: "34333427"
---
# <a name="view-plan-guide-properties"></a>Exibir propriedades de guia de plano
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Você pode exibir as propriedades dos guias de plano no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[tsql](../../includes/tsql-md.md)]  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Segurança](#Security)  
  
-   **Para exibir as propriedades dos guias de plano usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Security"></a> Segurança  
  
####  <a name="Permissions"></a> Permissões  
 A visibilidade dos metadados em exibições do catálogo está limitada aos protegíveis que pertencem a um usuário ou para os quais o usuário recebeu permissão.  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-view-the-properties-of-a-plan-guide"></a>Para visualizar as propriedades de um guia de plano  
  
1.  Clique no sinal de adição para expandir o banco de dados no qual você deseja exibir as propriedades de um guia de plano e clique no sinal de adição para expandir a pasta **Programação** .  
  
2.  Clique no sinal de adição para expandir a pasta **Guias de Plano** .  
  
3.  Clique com o botão direito do mouse no guia de plano do qual você deseja exibir as propriedades e selecione **Propriedades**.  
  
     As propriedades a seguir aparecem na caixa de diálogo **Propriedades do Guia de Plano** .  
  
     **Dicas**  
     Exibe as dicas de consulta ou plano de consulta a ser aplicado à instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] . Quando um plano de consulta é especificado como uma dica, a saída Plano de Execução XML para o plano é exibida.  
  
     **Está desabilitado**  
     Exibe o status da guia de plano. Os valores possíveis são **True** e **False**.  
  
     **Nome**  
     Exibe o nome do guia de plano.  
  
     **Parâmetros**  
     Quando o tipo de escopo é SQL ou TEMPLATE, são exibidos o nome e os tipos de dados de todos os parâmetros inseridos na instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] .  
  
     **Lote de escopo**  
     Exibe o texto de lote no qual a instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] é exibida.  
  
     **Nome do objeto de escopo**  
     Quando o tipo de escopo é OBJECT, exibi-se o nome do procedimento armazenado [!INCLUDE[tsql](../../includes/tsql-md.md)] , da função escalar definida pelo usuário, da função de valor de tabela de várias instruções ou do gatilho DML no qual a instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] é exibida.  
  
     **Nome do esquema de escopo**  
     Quando o tipo de escopo é OBJECT, exibe-se o nome do esquema no qual o objeto está contido.  
  
     **Tipo de escopo**  
     Exibe o tipo de entidade na qual a instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] é exibida. Isso especifica o contexto para se fazer a correspondência da instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] ao guia de plano. Os valores possíveis são **OBJECT**, **SQL**e **TEMPLATE**.  
  
     **Instrução**  
     Exibe a instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] na qual a guia de plano é aplicada.  
  
4.  Clique em **OK**.  
  
##  <a name="TsqlProcedure"></a> Usando o Transact-SQL  
  
#### <a name="to-view-the-properties-of-a-plan-guide"></a>Para visualizar as propriedades de um guia de plano  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**.  
  
    ```  
    -- If a plan guide named “Guide1” already exists in the AdventureWorks2012 database, delete it.  
    USE AdventureWorks2012;  
    GO  
    IF OBJECT_ID(N'Guide1') IS NOT NULL  
       EXEC sp_control_plan_guide N'DROP', N'Guide1';  
    GO  
    -- creates a plan guide named Guide1 based on a SQL statement  
    EXEC sp_create_plan_guide   
        @name = N'Guide1',   
        @stmt = N'SELECT TOP 1 *   
                  FROM Sales.SalesOrderHeader   
                  ORDER BY OrderDate DESC',   
        @type = N'SQL',  
        @module_or_batch = NULL,   
        @params = NULL,   
        @hints = N'OPTION (MAXDOP 1)';  
    GO  
    -- Gets the name, created date, and all other relevant property information on the plan guide created above.   
    SELECT name AS plan_guide_name,  
       create_date,  
       query_text,  
       scope_type_desc,  
       OBJECT_NAME(scope_object_id) AS scope_object_name,  
       scope_batch,  
       parameters,  
       hints,  
       is_disabled  
    FROM sys.plan_guides  
    WHERE name = N’Guide1’;  
    GO  
    ```  
  
 Para obter mais informações, veja [sys.plan_guides &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-plan-guides-transact-sql.md).  
  
  
