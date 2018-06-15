---
title: Gerenciar objetos usando o Pesquisador de Objetos | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.component: ssms-objects
ms.reviewer: ''
ms.suite: sql
ms.technology: ssms
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql13.SWB.SQLSERVEROBJECTEXPLORER.DHELP
helpviewer_keywords:
- Object Explorer F1 Help
- OE F1 Help
- OE Help
ms.assetid: e60367a7-3fdd-40b8-82bb-9e819d78de5a
caps.latest.revision: 5
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 1ed3b055f684a0dfc7b3932c1a0d9aff318cf98e
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "33046583"
---
# <a name="manage-objects-by-using-object-explorer"></a>Gerenciar objetos usando o Pesquisador de Objetos
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
Você pode usar o Pesquisador de Objetos para gerenciar objetos como bancos de dados, tabelas e procedimentos armazenados.  
  
## <a name="viewing-objects-in-object-explorer"></a>Exibindo objetos no Pesquisador de Objetos  
O Pesquisador de Objetos usa uma estrutura de árvore para agrupar informações em pastas. Para expandir pastas, clique no sinal de mais (+) ou clique duas vezes na pasta. Expanda pastas para mostrar informações mais detalhadas. Clique com o botão direito do mouse em pastas ou objetos para executar tarefas comuns. Clique duas vezes nos objetos para executar a tarefa mais comum.  
  
A primeira vez que você expandir uma pasta, o Pesquisador de Objetos fará uma consulta ao servidor para obter informações e popular a árvore. Você pode executar outras funções enquanto a árvore estiver sendo populada. Enquanto o Pesquisador de Objetos estiver populando a árvore, você poderá clicar em **Parar** para interromper o processo. Outras ações, como filtragem da lista, só terão efeito na parte da pasta que foi populada, a menos que você atualize a pasta para iniciar a população novamente.  
  
Para conservar os recursos quando houver muitos objetos, as pastas da árvore do Pesquisador de Objetos não atualizarão a lista de conteúdo automaticamente. Para atualizar a lista de objetos dentro de uma pasta, clique com o botão direito do mouse na pasta e clique em **Atualizar**.  
  
O Pesquisador de Objetos pode exibir até 65.536 objetos. Depois que você exceder 65.536 objetos visíveis, não será possível efetuar a rolagem em objetos adicionais na exibição da árvore do Pesquisador de Objetos. Para exibir objetos adicionais no Pesquisador de Objetos, feche os nós que você não estiver usando ou aplique a filtragem para reduzir o número de objetos.  
  
## <a name="filtering-the-list-of-objects-in-object-explorer"></a>Filtrando a lista de objetos no Pesquisador de Objetos  
Quando uma pasta tiver um grande número de objetos, talvez seja difícil de encontrar o objeto que você está procurando. Nesses casos, use o recurso de filtro do Pesquisador de Objetos para reduzir a lista para um tamanho menor. Por exemplo, você pode querer achar um usuário de banco de dados específico ou a tabela criada mais recentemente em listas que contêm centenas de objetos. Clique na pasta que você deseja filtrar e clique no botão de filtro para abrir a caixa de diálogo **Configurações de Filtro** . Você pode filtrar a lista por nome, data de criação e, às vezes, esquema, e fornecer operadores adicionais de filtragem, como **Starts with**, **Contains**e **Between**.  
  
## <a name="multi-select"></a>Multisseleção  
Apenas um objeto pode ser selecionado de cada vez no Pesquisador de Objetos. Para selecionar vários itens, pressione **F7** para abrir a página **Detalhes do Pesquisador de Objetos**. A página **Detalhes do Pesquisador de Objetos** dá suporte à multisseleção.  
  
## <a name="register-a-server-from-object-explorer"></a>Registrar um servidor do Pesquisador de Objetos  
Quando conectado a um servidor, você pode registrar o servidor facilmente para uso futuro. No Pesquisador de Objetos, clique com o botão direito do mouse no nome do servidor e clique em **Registrar**. Na caixa de diálogo **Registrar Servidor** , especifique onde na árvore de grupo de servidores você deseja colocar o servidor. Na caixa **Nome do servidor** , você pode substituir o nome do servidor por um nome de servidor mais significativo. Por exemplo, você poderia registrar o servidor **APSQL02** com um nome mais significativo como "**Contas a pagar**".  
  
## <a name="performing-actions-on-object-explorer-nodes"></a>Executando ações em nós do Pesquisador de Objetos  
Para executar ações em objetos, clique com o botão direito do mouse no nó do Pesquisador de Objetos que representa o objeto. Cada tipo de objeto oferece suporte a um conjunto exclusivo de ações de clique com o botão direito do mouse. Alguns dos tipos de ações que você pode executar usando os menus de clique com o botão direito do mouse incluem:  
  
### <a name="open-a-connected-query-editor"></a>Abrir um Editor de Consultas conectado  
Quando o Pesquisador de Objetos estiver conectado a um servidor, você poderá abrir uma nova janela do Editor de Códigos usando as configurações de conexão do Pesquisador de Objetos. Para abrir uma janela nova do Editor de Códigos, clique com o botão direito do mouse no nome do servidor no Pesquisador de Objetos e clique em **Nova Consulta**. Para abrir uma nova janela do Editor de Códigos usando um determinado banco de dados, clique com o botão direito do mouse no nome do banco de dados e clique em **Nova Consulta**. Ao abrir uma nova consulta para um servidor do Analysis Services, você pode selecionar consultas de DMX, MDX ou XMLA.  
  
### <a name="start-powershell"></a>Iniciar o PowerShell  
Você pode iniciar uma sessão do PowerShell clicando com o botão direito do mouse na maioria das pastas e dos objetos na árvore do Pesquisador de Objetos e selecionando **Iniciar PowerShell**. Isso inicia uma sessão do PowerShell que tem o suporte para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] PowerShell habilitado e o caminho definido até o objeto quando você clicou com o botão direito do mouse no Pesquisador de Objetos. Você pode inserir comandos do PowerShell em um ambiente interativo do PowerShell. Para saber mais, confira [SQL Server PowerShell](http://msdn.microsoft.com/en-us/89b70725-bbe7-4ffe-a27d-2a40005a97e7).  
  
## <a name="see-also"></a>Consulte Também  
[Pesquisador de Objetos](../../ssms/object/object-explorer.md)  
[Abrir e configurar o Pesquisador de Objetos](../../ssms/object/open-and-configure-object-explorer.md)  
[Conectar-se a uma instância do Pesquisador de Objetos](../../ssms/object/connect-to-an-instance-from-object-explorer.md)  
[Painel Detalhes do Pesquisador de Objetos](../../ssms/object/object-explorer-details-pane.md)  
[Relatórios personalizados no Management Studio](../../ssms/object/custom-reports-in-management-studio.md)  
  
