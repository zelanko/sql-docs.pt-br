---
title: 'Como fazer: clonar um banco de dados existente | Microsoft Docs'
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: aad3594a-11cf-4e68-a622-071a93d43875
author: markingmyname
ms.author: maghan
ms.openlocfilehash: d32b782c8508952a85f0a9a22b55d32dab096d6b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68017622"
---
# <a name="how-to-clone-an-existing-database"></a>Como fazer: Clonar um banco de dados existente
Esta tarefa utiliza algumas das etapas que você aprendeu em procedimentos anteriores para criar um novo banco de dados para o qual importar os dados existentes. Além disso, ele usa as etapas abordadas [Como usar comparação de esquema para comparar definições de banco de dados diferentes](../ssdt/how-to-use-schema-compare-to-compare-different-database-definitions.md) para sincronizar o esquema de um banco de dados de origem e de projeto.  
  
Usando estas etapas, você pode criar um banco de dados de desenvolvimento ou teste facilmente a partir de um banco de dados de produção com esquema e dados idênticos. Você pode continuar desenvolvendo o banco de dados de teste em um modo conectado, ou criar um projeto de banco de dados para desenvolvimento e teste offline, tudo sem interromper a operação do banco de dados de produção.  
  
> [!WARNING]  
> Os procedimentos a seguir usam entidades criadas em procedimentos anteriores na seção [Desenvolvimento de banco de dados conectado](../ssdt/connected-database-development.md).  
  
### <a name="to-create-a-development-database"></a>Para criar um banco de dados de desenvolvimento  
  
1.  No **Pesquisador de Objetos do SQL Server**, no nó **SQL Server**, expanda sua instância de servidor conectada.  
  
2.  Clique com o botão direito do mouse no nó **Bancos de Dados** e selecione **Adicionar Novo Banco de Dados**.  
  
3.  Renomeie o novo banco de dados como **TradeDev**.  
  
4.  Clique com o botão direito no banco de dados **Trade** no **Pesquisador de Objetos do SQL Server** e selecione **Comparação de Esquemas**. Siga as etapas no tópico [Como usar comparação de esquema para comparar definições de banco de dados diferentes](../ssdt/how-to-use-schema-compare-to-compare-different-database-definitions.md), escolhendo o banco de dados **Trade** original como a origem e o novo banco de dados **TradeDev** como o destino. Isto atualizará o **TradeDev** com o esquema do **Trade**.  
  
### <a name="to-replicate-data"></a>Para replicar dados  
  
1.  A etapa anterior duplicou somente o esquema do banco de dados de produção para o banco de dados de desenvolvimento. Neste procedimento, você duplicará dados de produção para o banco de dados de desenvolvimento.  
  
    Clique com o botão direito na tabela **Suppliers** no banco de dados **Trade** e selecione **Exibir Dados**. O Editor de Dados abre.  
  
2.  Clique no botão **Script** ao lado de **Máx. de Linhas** na barra de ferramentas.  
  
3.  Quando a janela de script abrir, verifique se Conectado é mostrado na barra de status abaixo do painel de script Transact\-SQL. Se Desconectado for mostrado, clique no botão **Conectar** (o mais à esquerda na barra de ferramentas) e insira suas informações de servidor e credenciais.  
  
4.  No menu suspenso **Banco de dados** ao lado dos botões **Conectar**/**Desconectar**, selecione **TradeDev**. Isso é semelhante à instrução Transact\-SQL`USE` e garantirá que o script no editor de código seja executado no banco de dados **TradeDev**.  
  
5.  Clique no botão **Executar Consulta** para executar as instruções `INSERT`. Isto inserirá todas as linhas da tabela `Suppliers` do banco de dados `Trade` na tabela `Suppliers` no banco de dados `TradeDev`.  
  
6.  Repita as etapas anteriores para todas as tabelas no banco de dados `Trade`, de modo que elas sejam replicadas no banco de dados `TradeDev`.  
  
7.  Use o Editor de Dados para verificar se todas as tabelas no novo banco de dados `TradeDev` foram populadas.  
  
## <a name="see-also"></a>Consulte Também  
[Como: Usar comparação de esquema para comparar definições de banco de dados diferentes](../ssdt/how-to-use-schema-compare-to-compare-different-database-definitions.md)  
  
