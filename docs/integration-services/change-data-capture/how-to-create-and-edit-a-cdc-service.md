---
title: Como criar e editar um serviço CDC | Microsoft Docs
ms.custom: ''
ms.date: 03/20/2017
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
ms.assetid: 1b3d47a5-dc89-482d-bbc7-fff04f194c43
caps.latest.revision: 7
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 00a86f55f97fefcc15e4bcc6a301a53dd0e58e87
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2018
---
# <a name="how-to-create-and-edit-a-cdc-service"></a>Como criar e editar um Serviço CDC
  Estes procedimentos descrevem como criar e editar um novo Serviço Oracle CDC a partir do Console de Configuração do Serviço CDC.  
  
 Este procedimento exige um usuário do Windows com privilégios de administrador no computador onde o serviço Oracle CDC está configurado.  
  
### <a name="to-create-a-new-cdc-service"></a>Para criar um novo serviço CDC  
  
1.  No menu **Iniciar** , selecione **Configuração do Serviço CDC para Oracle**.  
  
2.  No painel esquerdo, clique com o botão direito em Serviços Locais CDC e selecione Novo Serviço  
  
     Você também pode clicar em **Novo Serviço** no painel **Ações** .  
  
3.  Digite ou insira as informações necessárias na caixa de diálogo Novo Serviço Oracle CDC. Consulte [Create and Edit an Oracle CDC Service](../../integration-services/change-data-capture/create-and-edit-an-oracle-cdc-service.md) para obter informações sobre como inserir informações na caixa de diálogo Novo Serviço Oracle CDC.  
  
     O logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] fornecido na caixa de diálogo Novo Serviço Oracle CDC é usado pelo Serviço Oracle CDC quando o serviço é executado. Esse logon somente precisa ser um membro da função pública de servidor fixa, nenhum outro privilégio será necessário. Quando novas Instâncias do Oracle CDC são adicionadas, esse logon recebe acesso **db_owner** aos bancos de dados CDC do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] associados.  
  
4.  Quando você terminar de inserir as informações necessárias, clique em **OK**.  
  
     Para criar a definição de Serviço do Windows do Oracle CDC, o programa precisa de acesso de atualização ao banco de dados MSXDBCDC na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] associada. Quando você clica em **OK**, uma caixa de diálogo solicita que o usuário insira um logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] com um acesso de atualização para o banco de dados MSXDBCDC.  
  
     Para obter informações sobre os dados que você deverá digitar na caixa de diálogo Conecte-se ao SQL Server, consulte [Connection to SQL Server](../../integration-services/change-data-capture/connection-to-sql-server.md).  
  
5.  Clique em **OK** para fechar a caixa de diálogo Novo Serviço Oracle CDC.  
  
### <a name="to-edit-a-cdc-service"></a>Para editar um serviço CDC  
  
1.  No menu **Iniciar** , selecione **Configuração do Serviço CDC para Oracle**.  
  
2.  No painel esquerdo, selecione **Serviços Locais CDC** e clique com o botão direito do mouse no serviço local que você quer editar e selecione **Propriedades**.  
  
     Você pode selecionar o serviço com o qual você está trabalhando no meio e, no painel **Ações** , clique em **Propriedades**.  
  
3.  Digite ou insira as informações necessárias na caixa de diálogo Propriedades do Serviço CDC. Consulte [Create and Edit an Oracle CDC Service](../../integration-services/change-data-capture/create-and-edit-an-oracle-cdc-service.md) para obter informações sobre como inserir informações na caixa de diálogo Propriedades do Serviço CDC.  
  
4.  Quando você terminar de inserir as informações necessárias, clique em **OK**e a caixa de diálogo Conecte-se ao SQL Server será aberta.  
  
     Quando um logon sem permissão de gravação para o banco de dados MSXDBDCDC tenta criar uma nova instância Oracle CDC, uma mensagem de erro é exibida. Clique em **OK** nessa caixa de diálogo para exibir a caixa de diálogo Conecte-se ao SQL Server. Nesta caixa de diálogo, você deve inserir as credenciais para um logon que tem permissão de gravação ao banco de dados MSXDBCDC, como a função de banco de dados **db_owner** .  
  
     Para obter informações sobre os dados que você deverá digitar na caixa de diálogo Conecte-se ao SQL Server, consulte [Connection to SQL Server](../../integration-services/change-data-capture/connection-to-sql-server.md).  
  
5.  Clique em **OK** na caixa de diálogo Conectar ao Oracle. Ambas as caixas de diálogo fecham e o serviço é atualizado e registrado.  
  
## <a name="see-also"></a>Consulte Também  
 [Change Data Capture Designer para Oracle da Attunity](../../integration-services/change-data-capture/change-data-capture-designer-for-oracle-by-attunity.md)   
 [Criar e editar um serviço Oracle CDC](../../integration-services/change-data-capture/create-and-edit-an-oracle-cdc-service.md)  
  
  
