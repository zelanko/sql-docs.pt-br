---
title: Conectando-se com o Editor de Consultas | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
ms.assetid: 48725f54-a7b6-4b79-948e-965c1fe4eef1
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: bcb2454d9f6b4a6df465c33ca218c4a960f8099b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "68187816"
---
# <a name="connecting-with-query-editor"></a>Conectando com o Editor de Consultas
  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] permite que você escreva ou edite código enquanto estiver desconectado do servidor. Isso pode ser útil quando o servidor não estiver disponível ou quando você quiser conservar recursos escassos de rede ou servidor. Você também pode alterar a conexão do Editor de Consultas com uma instância nova do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sem abrir uma nova janela do editor ou redigitar o código.  
  
## <a name="coding-offline"></a>Codificando offline  
  
#### <a name="to-write-code-offline-and-then-connect-to-different-servers"></a>Para escrever código offline e depois se conectar a servidores diferentes  
  
1.  Na barra de ferramentas do [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] , clique em **Consulta do Mecanismo de Banco de Dados** para abrir o Editor de Consultas.  
  
2.  Na caixa de diálogo **Conectar ao Mecanismo de Banco de Dados** , clique em **Cancelar**. O Editor de Consultas é aberto e a barra de título do editor indica que você não está conectado a uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
3.  No painel de código, digite as instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] a seguir:  
  
    ```  
    SELECT * FROM Production.Product;  
    GO  
    ```  
  
     Neste ponto, você pode se conectar a uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] clicando em **Conectar**, **Executar**, **Analisar**ou **Exibir Plano de Execução Estimado**, disponíveis no menu **Consultar** , na barra de ferramentas do Editor de Consultas, ou no menu de atalho quando você clica com o botão direito do mouse na janela do Editor de Consultas. Para esta prática, nós usaremos a barra de ferramentas.  
  
4.  Na barra de ferramentas, clique no botão **Executar** para abrir a caixa de diálogo **Conectar ao Mecanismo de Banco de Dados** .  
  
5.  Na caixa de texto **Nome do servidor** , digite o nome do servidor e clique em **Opções**.  
  
6.  Na guia **Propriedades da Conexão** , na lista **Conectar ao banco de dados** , procure o servidor para selecionar [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] e clique em **Conectar**.  
  
7.  Para abrir outra janela do Editor de Consultas com a mesma conexão, na barra de ferramentas, clique em **Nova Consulta**.  
  
8.  Para alterar as conexões, clique com o botão direito do mouse na janela do Editor de Consultas, aponte para **Conexão**e clique em **Alterar Conexão**.  
  
9. Na caixa de diálogo **Conectar ao SQL Server** , selecione outra instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , se disponível, e clique em **Conectar**.  
  
 Esse recurso novo do Editor de Consultas permite a execução do mesmo código facilmente em vários servidores. Isso pode ser útil para ações de manutenção que envolvem servidores semelhantes.  
  
## <a name="next-task-in-lesson"></a>Próxima tarefa da lição  
 [Adicionando recuo](lesson-2-2-adding-indentation.md)  
  
  
