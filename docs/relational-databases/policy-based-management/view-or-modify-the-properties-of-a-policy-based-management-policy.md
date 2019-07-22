---
title: Exibir ou modificar as propriedades de uma política de gerenciamento baseado em políticas | Microsoft Docs
ms.custom: ''
ms.date: 10/06/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Policy-Based Management, modify policies
- Policy-Based Management, view policies
ms.assetid: ba805504-5db5-4731-a8da-a0e89cb20c37
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: cadd1acbe5092aee4460a9ffe1d36bfa50a3a9f5
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67908151"
---
# <a name="view-or-modify-the-properties-of-a-policy-based-management-policy"></a>Exibir ou modificar as propriedades de uma política de gerenciamento baseado em políticas
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Este tópico descreve como exibir ou modificar as propriedades de uma política de gerenciamento baseado em políticas [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
  
####  <a name="Permissions"></a> Permissões  
 Requer a associação à função PolicyAdministratorRole no banco de dados msdb.  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-view-the-properties-of-all-policies-on-an-object"></a>Para exibir as propriedades de todas as políticas em um objeto  
  
1.  Em Pesquisador de Objetos, clique com o botão direito do mouse em um servidor, objeto de servidor, banco de dados ou objeto de banco de dados, aponte para **Políticas** e selecione **Exibir**. Para obter mais informações sobre as opções disponíveis na caixa de diálogo **Exibir políticas-** _nome_do_objeto_, confira [Caixa de diálogo Exibir Políticas](../../relational-databases/policy-based-management/view-policies-dialog-box.md).  
  
2.  Quando terminar, clique em **Fechar**.  
  
#### <a name="to-view-or-modify-a-specific-policys-properties"></a>Para exibir ou modificar as propriedades de uma política específica  
  
1.  No **Pesquisador de Objetos**, clique no sinal de adição para expandir o servidor que contém a Política de Gerenciamento Baseado em Políticas que você deseja exibir ou modificar.  
  
2.  Clique no sinal de adição para expandir a pasta **Gerenciamento** .  
  
3.  Clique no sinal de adição para expandir a pasta **Gerenciamento de Política**.  
  
4.  Clique no sinal de adição para expandir a pasta **Políticas** .  
  
5.  Clique com o botão direito do mouse na política que você deseja exibir ou modificar e selecione **Propriedades**. Para obter mais informações sobre as opções disponíveis na caixa de diálogo **Abrir Política -** _nome_da_política_, confira [Caixa de diálogo Criar Política ou Abrir Política, página Geral](../../relational-databases/policy-based-management/create-new-policy-or-open-policy-dialog-box-general-page.md) e [Caixa de diálogo Criar Política ou Abrir Política, página Descrição](../../relational-databases/policy-based-management/create-new-policy-or-open-policy-dialog-box-description-page.md).  
  
6.  Quando terminar, clique em **OK**.  
  
##  <a name="TsqlProcedure"></a> Usando o Transact-SQL  
  
#### <a name="to-view-a-policys-properties"></a>Para exibir as propriedades de uma política  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**.  
  
    ```  
    USE msdb;  
    GO  
    SELECT name,  
       execution_mode,  
       description,  
       is_enabled,  
       job_id  
    FROM syspolicy_policies;  
    GO  
    ```  
  
 Para obter mais informações, veja [syspolicy_policies &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/syspolicy-policies-transact-sql.md).  
  
  
