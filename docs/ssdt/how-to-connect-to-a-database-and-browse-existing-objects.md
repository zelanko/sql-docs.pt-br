---
title: 'Como fazer: conectar-se a um banco de dados e procurar objetos existentes | Microsoft Docs'
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.topic: conceptual
f1_keywords:
- sql.data.tools.connectionpicker.f1
ms.assetid: 9b331800-3806-4459-ac58-88cdc98124d3
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 21096819ebd7a54ab8f4505ad980c0e6a5266d6f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65098111"
---
# <a name="how-to-connect-to-a-database-and-browse-existing-objects"></a>Como fazer: conectar-se a um Banco de Dados e Procure Objetos Existentes
Uma tarefa muito comum para administradores de banco de dados e desenvolvedores é conectar a um banco de dados online, criar ou procurar seu esquema e consultar seus objetos. O Pesquisador de Objetos do SQL Server no Visual Studio agora contém um nó **SQL Server** dedicado, sob o qual todas as instâncias conectadas do SQL Server e seus respectivos bancos de dados são agrupados em uma hierarquia semelhante ao SSMS. As instâncias conectadas do SQL Server podem ser uma instância local, como um SQL Server 2008 em execução, ou uma instância do SQL Azure externa.  
  
O procedimento a seguir supõe que você já tem o banco de dados de exemplo AdventureWorks instalado. Use [CodePlex](https://msftdbprodsamples.codeplex.com/) para localizar e instalar bancos de dados de exemplo para diferentes versões do SQL Server. Se preferir, você também pode seguir as etapas e usar um banco de dados existente no seu servidor.  
  
### <a name="to-connect-to-a-database-instance"></a>Para conectar-se a uma instância de banco de dados  
  
1.  No Visual Studio, certifique-se de que o **Pesquisador de Objetos do SQL Server** esteja aberto. Se não estiver, clique no menu **Exibir** e selecione **Pesquisador de Objetos do SQL Server**.  
  
2.  Clique com o botão direito do mouse no tabela nó**SQL Server** no **Pesquisador de Objetos do SQL Server** e selecione **Adicionar SQL Server**.  
  
3.  Na caixa de diálogo **Conectar ao Servidor** , insira o **Nome do servidor** da instância do servidor à qual deseja se conectar, suas credenciais e clique em **Conectar**.  
  
4.  No **Pesquisador de Objetos do SQL Server**, expanda o nó **Bancos de Dados** em sua instância do servidor. Você verá todos os bancos de dados que residem nessa instância do servidor adicionados sob o nó **Bancos de Dados** .  
  
5.  Expanda o nó **AdventureWorks** (ou outro banco de dados). Você observará que todas as entidades de banco de dados são organizadas em uma hierarquia semelhante ao SQL Server Management Studio.  
  
