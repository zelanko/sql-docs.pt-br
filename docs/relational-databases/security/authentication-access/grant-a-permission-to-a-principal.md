---
title: "Conceder uma permissão a uma entidade de segurança | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Grant permission to a principal
ms.assetid: 4107389d-05b6-4aa3-9fa8-95b40cdf05dc
caps.latest.revision: 12
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: On Demand
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 969f70df2cdb72c1fa47e645580ae723fb519864
ms.contentlocale: pt-br
ms.lasthandoff: 06/22/2017

---
# <a name="grant-a-permission-to-a-principal"></a>Conceder uma permissão a uma entidade de segurança
  Este tópico descreve como conceder permissão a uma entidade de segurança no [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[tsql](../../../includes/tsql-md.md)].  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Limitações e restrições](#Restrictions)  
  
     [Segurança](#Security)  
  
-   **Para conceder permissão a uma entidade de segurança usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Restrictions"></a> Limitações e restrições  
 Considere as práticas recomendadas a seguir que podem facilitar o gerenciamento de permissões.  
  
-   Conceda permissão para funções, em vez de logons individuais ou usuários. Quando um indivíduo for substituído por outro, remova o indivíduo que está deixando a função e adicione o novo indivíduo a ela. As muitas permissões que podem ser associadas à função estarão automaticamente disponíveis para o novo indivíduo. Se várias pessoas em uma organização precisarem das mesmas permissões, adicionar cada uma dessas pessoas à função concederá as mesmas permissões.  
  
-   Configure protegíveis semelhantes (tabelas, exibições e procedimentos) para pertencer a um esquema e conceder permissões ao esquema. Por exemplo, o esquema de folha de pagamento pode possuir várias tabelas, exibições e procedimentos armazenados. Quando o acesso é concedido ao esquema, todas as permissões necessárias para executar a função de folha de pagamento podem ser concedidas ao mesmo tempo. Para obter mais informações sobre quais protegíveis podem receber permissões, consulte [Securables](../../../relational-databases/security/securables.md).  
  
###  <a name="Security"></a> Segurança  
  
####  <a name="Permissions"></a> Permissões  
 O concessor (ou o principal especificado com a opção AS) deve ter a permissão em si com GRANT OPTION ou uma permissão superior que implique na concessão da permissão. Membros da função de servidor fixa **sysadmin** podem conceder qualquer permissão.  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-grant-permission-to-a-principal"></a>Para conceder permissão a uma entidade de segurança  
  
1.  No Pesquisador de Objetos, expanda o banco de dados que contém o objeto para o qual você deseja conceder permissões.  
  
    > [!NOTE]  
    >  Estas etapas lidam especificamente com a concessão de permissões a um procedimento armazenado, mas você pode usar etapas semelhantes para adicionar permissões a tabelas, exibições, funções e assemblies, bem como a outro protegíveis. Para obter mais informações, veja [GRANT &#40;Transact-SQL&#41;](../../../t-sql/statements/grant-transact-sql.md)  
  
2.  Expanda a pasta **Programação** .  
  
3.  Expanda a pasta **Procedimentos Armazenados** .  
  
4.  Clique com o botão direito do mouse em um procedimento armazenado e selecione **Propriedades**.  
  
5.  Na caixa de diálogo **Propriedades do Procedimento Armazenado –***stored_procedure_name* , em selecionar uma página, selecione **Permissões**. Use essa página para adicionar usuários ou funções ao procedimento armazenado e especificar as permissões que esses usuários ou funções têm.  
  
6.  Quando terminar, clique em **OK**.  
  
##  <a name="TsqlProcedure"></a> Usando Transact-SQL  
  
#### <a name="to-grant-permission-to-a-principal"></a>Para conceder permissão a uma entidade de segurança  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDE](../../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**.  
  
    ```  
    -- Grants EXECUTE permission on stored procedure HumanResources.uspUpdateEmployeeHireInfo to an application role called Recruiting11.   
    USE AdventureWorks2012;  
    GO  
    GRANT EXECUTE ON OBJECT::HumanResources.uspUpdateEmployeeHireInfo  
        TO Recruiting11;  
    GO  
    ```  
  
 Para obter mais informações, veja [GRANT &#40;Transact-SQL&#41;](../../../t-sql/statements/grant-transact-sql.md) e [Permissões de objeto GRANT &#40;Transact-SQL&#41;](../../../t-sql/statements/grant-object-permissions-transact-sql.md).  
  
## <a name="see-also"></a>Consulte também  
 [Entidades &#40;Mecanismo de Banco de Dados&#41;](../../../relational-databases/security/authentication-access/principals-database-engine.md)  
  
  

