---
title: Como gerenciar um serviço CDC local | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.service: ''
ms.component: change-data-capture
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 7f9be649-cd93-40c1-bc48-0480106f207c
caps.latest.revision: 6
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: b319fb60e8b3e2d9a657fd7e710359ed274587ba
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2018
---
# <a name="how-to-manage-a-local-cdc-service"></a>Como gerenciar um serviço CDC local
  Este procedimento descreve como usar o Console de Configuração do Serviço CDC para gerenciar os serviços CDC específicos.  
  
### <a name="to-manage-a-specific-cdc-service"></a>Para gerenciar um Serviço CDC específico  
  
1.  No menu **Iniciar** , selecione **Configuração do Serviço CDC para Oracle**.  
  
2.  No painel esquerdo no Console de Configuração do Serviço CDC, expanda **Serviços Locais de CDC**.  
  
3.  Selecione o serviço CDC com o qual você deseja trabalhar.  
  
     Você também pode clicar com o botão direito no serviço CDC com o qual você deseja trabalhar e selecionar a ação desejada.  
  
     **OU**  
  
     Selecione **Serviços Locais CDC** no painel esquerdo no Console de Configuração do Serviço CDC e selecione o serviço com o qual você quer trabalhar na seção do meio.  
  
     Você também pode clicar com o botão direito no serviço CDC com o qual você deseja trabalhar e selecionar a ação desejada.  
  
4.  Você pode realizar as seguintes tarefas ao trabalhar com um serviço CDC.  
  
    -   **Excluir o serviço**  
  
         No painel **Ações** no lado direito do Console de Configuração do Serviço CDC, clique em **Excluir** para excluir o serviço.  
  
         Você também pode clicar com o botão direito do mouse no serviço CDC que deseja excluir e selecionar **Excluir**.  
  
         **Observação**: se o serviço estiver sendo executado ao excluir o serviço, ele será parado antes de ser excluído.  
  
         Para excluir uma definição de Serviço do Windows do Oracle CDC, o programa precisa de acesso de atualização ao banco de dados MSXDBCDC na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] associada. Quando você clicar em **OK** para excluir o serviço, o programa tentará excluir o registro do Serviço Oracle CDC no banco de dados MSXDBCDC. Se falhar devido à falta de permissões, uma caixa de diálogo será exibida para pedir que o usuário insira um logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] com um acesso de atualização para o banco de dados MSXDBCDC.  
  
         Para obter informações sobre os dados que você deverá inserir na caixa de diálogo Conecte-se ao SQL Server, consulte [Manage an Oracle CDC Service](../../integration-services/change-data-capture/manage-an-oracle-cdc-service.md) e [Connection to SQL Server for Delete](../../integration-services/change-data-capture/connection-to-sql-server-for-delete.md).  
  
    -   **Editar as propriedades de serviço CDC**  
  
         No painel **Ações** no lado direito do Console de Configuração do Serviço CDC, clique em **Propriedades**.  
  
         Você também pode clicar com o botão direito do mouse no serviço CDC em que deseja editar as propriedades e selecionar **Propriedades**.  
  
## <a name="see-also"></a>Consulte Também  
 [Manage an Oracle CDC Service](../../integration-services/change-data-capture/manage-an-oracle-cdc-service.md)  
  
  
