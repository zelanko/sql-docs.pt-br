---
title: 'Etapa 3: adicionar e configurar um gerenciador de conexões OLE DB | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: e7b74cba-a0e5-4478-af12-3f81b9484e9e
author: chugugrace
ms.author: chugu
ms.openlocfilehash: e7ba771b404ac7d0fad5721fa6056333634e7246
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/26/2020
ms.locfileid: "85436073"
---
# <a name="step-3-adding-and-configuring-an-ole-db-connection-manager"></a>Etapa 3: Adicionar e configurar um gerenciador de conexões OLE DB
  Depois de ter adicionado um gerenciador de conexões de arquivo simples para conectar-se à origem de dados, a próxima tarefa é adicionar um gerenciador de conexões OLE DB para conectar-se ao destino. Um gerenciador de conexões OLE DB permite que um pacote extraia dados de qualquer fonte de dados compatível com OLE DB ou carregue dados nela. Usando o gerenciador de conexões OLE DB, você pode especificar o servidor, o método de autenticação e o banco de dados padrão para a conexão.  
  
 Nesta lição, você aprenderá a criar um gerenciador de conexões OLE DB que usa a Autenticação do Windows para se conectar à instância local do **AdventureWorksDB2012**. O gerenciador de conexões OLE DB que você criar também será referenciado por outros componentes que você criar posteriormente neste tutorial, como, por exemplo, a transformação Pesquisa e o destino OLE DB.  
  
### <a name="to-add-and-configure-an-ole-db-connection-manager-to-the-ssis-package"></a>Para adicionar e configurar um Gerenciador de conexões OLE DB no pacote SSIS.  
  
1.  Clique com o botão direito do mouse em qualquer lugar da área **Gerenciadores de Conexões** e clique em **Nova Conexão OLE DB**.  
  
2.  Na caixa de diálogo **Configurar Gerenciador de Conexões OLE DB** , clique em **Novo**.  
  
3.  Em **Nome do servidor**, insira **localhost**.  
  
     Quando você especifica localhost como o nome do servidor, o gerenciador de conexões se conecta à instância padrão do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] no computador local. Para usar uma instância remota do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], substitua localhost pelo nome do servidor ao qual você deseja se conectar.  
  
4.  No grupo **Fazer logon no servidor** , verifique se a opção **Usar Autenticação do Windows** está selecionada.  
  
5.  No grupo **conectar-se a um banco de dados** , na caixa **selecionar ou inserir um nome de banco de dados** , digite ou selecione `AdventureWorksDW2012` .  
  
6.  Clique em **Testar Conexão** para verificar se as configurações de conexão especificadas são válidas.  
  
7.  Clique em **OK**.  
  
8.  Clique em **OK**.  
  
9. No painel **Conexões de Dados** da caixa de diálogo **Configurar Gerenciador de Conexões OLE DB** , verifique se a opção **localhost.AdventureWorksDW2012** está selecionada.  
  
10. Clique em **OK**.  
  
## <a name="next-task-in-lesson"></a>Próxima tarefa da lição  
 [Etapa 4: Adicionar uma tarefa de fluxo de dados ao pacote](lesson-1-4-adding-a-data-flow-task-to-the-package.md)  
  
## <a name="see-also"></a>Consulte Também  
 [gerenciador de conexões OLE DB](connection-manager/ole-db-connection-manager.md)  
  
  
