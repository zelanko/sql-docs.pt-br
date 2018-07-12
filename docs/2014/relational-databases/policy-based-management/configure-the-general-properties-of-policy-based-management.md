---
title: Configurar as propriedades gerais do gerenciamento baseado em políticas | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.swb.dmf.PolicyManagement.f1
helpviewer_keywords:
- Policy-Based Management, configure properties
ms.assetid: 6d1e0e37-29ea-408a-a055-384984d884be
caps.latest.revision: 8
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: e06b3431cee345d4cec6448fabe37ad6bbbd7476
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37162337"
---
# <a name="configure-the-general-properties-of-policy-based-management"></a>Configurar as propriedades gerais do gerenciamento baseado em políticas
  Este tópico descreve como configurar as propriedades para o Gerenciamento Baseado em Políticas no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Segurança](#Security)  
  
-   **Para configurar o Gerenciamento Baseado em Políticas usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Security"></a> Segurança  
  
####  <a name="Permissions"></a> Permissões  
 Requer a associação à função de banco de dados fixa PolicyAdministratorRole.  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-configure-policy-based-management"></a>Para configurar o Gerenciamento Baseado em Políticas  
  
1.  No **Pesquisador de Objetos**, clique no sinal de adição para expandir o servidor no qual você deseja configurar as propriedades do Gerenciamento Baseado em Políticas.  
  
2.  Clique no sinal de adição para expandir a pasta **Gerenciamento** .  
  
3.  Clique com o botão direito do mouse em **Gerenciamento de Política** e selecione **Propriedades**.  
  
     As opções a seguir estão disponíveis na caixa de diálogo **Propriedades de Gerenciamento de Política** .  
  
     **Enabled**  
     Especifica se o Gerenciamento Baseado em Políticas está habilitado.  
  
     **HistoryRetentionInDays**  
     Especifica o número de dias que o histórico de avaliação de política deve ser mantido. Se esse valor for 0 (o padrão), o histórico não será removido automaticamente.  
  
     **LogOnSuccess**  
     Especifica se o Gerenciamento Baseado em Políticas registra em log avaliações de política com êxito.  
  
    -   Quando esse valor é false (o padrão), somente são registradas em log as avaliações de política com falha.  
  
    -   Quando esse valor é verdadeiro, as avaliações de política bem-sucedidas e com falha são registradas em log.  
  
4.  Quando terminar, clique em **OK**.  
  
##  <a name="TsqlProcedure"></a> Usando Transact-SQL  
  
#### <a name="to-configure-policy-based-management"></a>Para configurar o Gerenciamento Baseado em Políticas  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**.  
  
    ```  
    -- enables Policy-Based Management   
    USE msdb;  
    GO  
    EXEC dbo.sp_syspolicy_configure   
         @name = N'Enabled',   
         @value = 1;  
    GO  
    ```  
  
 Para obter mais informações, veja [sp_syspolicy_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-syspolicy-configure-transact-sql).  
  
  
