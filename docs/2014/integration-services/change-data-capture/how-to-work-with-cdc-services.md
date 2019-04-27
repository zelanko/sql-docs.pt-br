---
title: Como trabalhar com os serviços CDC | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: db5c718a-6e7f-48ec-82a3-9d5b131716e5
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: d047d1c584e176f5446361dd29821eb4ff18aa74
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62771205"
---
# <a name="how-to-work-with-cdc-services"></a>Como trabalhar com os serviços CDC
  Este procedimento descreve como usar o Console de Configuração do Serviço CDC para preparar uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para trabalhar com os Serviços Oracle CDC e criar um novo serviço CDC.  
  
### <a name="to-work-with-cdc-services"></a>Para trabalhar com serviços CDC  
  
1.  No menu **Iniciar** , selecione **Configuração do Serviço CDC para Oracle**.  
  
2.  No painel esquerdo, **Serviços Locais CDC** (o nível raiz).  
  
3.  Execute uma das seguintes tarefas ou ambas:  
  
    -   **Preparar SQL Server**  
  
         Selecione esta opção no painel **Ações** no lado direito do Console de Configuração do Serviço CDC.  
  
         Você também pode clicar com o botão direito do mouse em **Local CDC Services (Serviços Locais de CDC)** e selecionar **Prepare SQL Server (Preparar SQL Server)**.  
  
         A caixa de diálogo Preparando a Instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para Oracle CDC é aberta.  
  
         Para preparar a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para os serviços Oracle CDC, o logon deve ter um logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] com a função de servidor fixa `dbcreator` . Este logon é usado para criar o banco de dados MSXDBCDC necessário para adicionar os Serviços Oracle CDC e, posteriormente, Instâncias Oracle CDC.  
  
         Para obter informações sobre como usar essa caixa de diálogo, consulte [Prepare SQL Server for CDC](prepare-sql-server-for-cdc.md). Para obter informações sobre como habilitar uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para CDC, consulte [Como preparar o SQL Server para CDC](how-to-prepare-sql-server-for-cdc.md).  
  
    -   **Criar um novo serviço CDC**  
  
         Clique em **Novo Serviço** no painel **Ações** no lado direito do Console de Configuração do Serviço CDC.  
  
         Você também pode clicar com o botão direito do mouse em **Serviços Locais de CDC** e selecionar **Novo Serviço**.  
  
         O caixa de diálogo Novo Serviço do Oracle CDC é aberta.  
  
         Para obter informações sobre como usar essa caixa de diálogo, consulte [Create and Edit an Oracle CDC Service](create-and-edit-an-oracle-cdc-service.md). Para obter informações sobre como criar ou editar um serviço CDC, consulte [Como criar e editar um Serviço CDC](how-to-create-and-edit-a-cdc-service.md).  
  
         O logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usado pelo Serviço Oracle CDC somente precisa ser um membro da função `public` de servidor fixa, nenhum outro privilégio será necessário. Porém, para criar o Serviço Oracle CDC, o logon deve ter permissão de gravação no banco de dados MSXDBCDC, por exemplo, a função de banco de dados **db_owner** deve ser atribuída ao logon. Quando um logon sem permissão de gravação para o banco de dados MSXDBDCDC tenta criar uma nova instância Oracle CDC, uma mensagem de erro é exibida. Clique em **OK** nessa caixa de diálogo para exibir a caixa de diálogo Conecte-se ao SQL Server.  
  
         Para obter informações sobre como inserir as credenciais para um logon que tem permissão de gravação ao banco de dados MSXDBCDC, como a função de banco de dados **db_owner** , consulte [Criar e editar um serviço Oracle CDC](create-and-edit-an-oracle-cdc-service.md) e [Conexão com o SQL Server](connection-to-sql-server.md).  
  
## <a name="see-also"></a>Consulte também  
 [Trabalhar com serviços CDC](work-with-cdc-services.md)  
  
  
