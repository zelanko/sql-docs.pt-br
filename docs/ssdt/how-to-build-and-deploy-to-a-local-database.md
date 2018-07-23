---
title: Como compilar e implantar em um banco de dados local | Microsoft Docs
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: ebca8ff8-9a09-4207-8979-9d577af7c1d5
caps.latest.revision: 25
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: ced224db1a1826effe84dd713abe64c3cddf1b94
ms.sourcegitcommit: c8f7e9f05043ac10af8a742153e81ab81aa6a3c3
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/17/2018
ms.locfileid: "39085928"
---
# <a name="how-to-build-and-deploy-to-a-local-database"></a>Como: Compilar e implantar em um banco de dados local
O Microsoft SQL Server 2012 fornece uma instância de servidor local sob demanda, chamada Tempo de Execução de Banco de Dados Local do SQL Server Express, que é ativada quando um projeto de Banco de Dados do SQL Server é depurado. Esta instância de servidor local pode ser usada como uma área restrita para compilar, testar e depurar seu projeto. Isso é independente de qualquer uma de suas instâncias do SQL Server instaladas e não é acessível fora do SQL Server Data Tools (SSDT). Esse tipo de organização é ideal para os desenvolvedores que não têm acesso ou têm acesso limitado a bancos de dados de produção, mas gostariam de testar seus projetos localmente antes que uma equipe autorizada implante-os na produção. Além disso, quando você está desenvolvendo uma solução de banco de dados para o SQL Azure, pode utilizar a conveniência fornecida por este servidor local para desenvolver e testar localmente seu projeto de banco de dados, antes de implantá-lo na nuvem.  
  
> [!WARNING]  
> Um banco de dados sob o nó do banco de dados local no Pesquisador de Objetos do SQL Server é um reflexo do projeto de banco de dados correspondente e não está relacionado ao banco de dados de mesmo nome em uma instância de servidor conectada.  
  
> [!WARNING]  
> Os procedimentos a seguir utilizam entidades criadas em procedimentos anteriores nas seções [Desenvolvimento de banco de dados conectado](../ssdt/connected-database-development.md) e [Desenvolvimento de banco de dados offline orientado a projetos](../ssdt/project-oriented-offline-database-development.md).  
  
### <a name="to-use-the-local-database"></a>Para usar o banco de dados local  
  
1.  Observe que no **Pesquisador de Objetos do SQL Server**, no nó **SQL Server**, um novo nó chamado **Local** é exibido. Esta é a instância de banco de dados local.  
  
2.  Expanda os nós **Local** e **Bancos de Dados**. Observe a aparência de um banco de dados com o mesmo nome como o projeto TradeDev. Expanda os nós sob este banco de dados. A janela **Operações de Ferramentas de Dados** mostra o status das operações de expansão/importação em andamento em qualquer banco de dados no nó **Local**. Observe que eles não contêm nenhuma das tabelas e entidades que nós criamos em procedimentos anteriores.  
  
3.  Pressione F5 para depurar o projeto de banco de dados TradeDev.  
  
    Por padrão, o SSDT usará a instância de servidor de banco de dados local para depurar projetos de banco de dados. Neste caso, o SSDT tentará primeiro compilar o projeto e, se não houver nenhum erro, o projeto (e suas entidades) será implantado no banco de dados local. Se você depurar o mesmo projeto posteriormente, o SSDT detectará as alterações desde a sua última sessão de depuração e implantará somente elas no banco de dados local.  
  
4.  Expanda os nós em **TradeDev** no servidor de banco de dados **Local** novamente. Dessa vez, observe que as tabelas, as exibições e as funções foram implantados no servidor de banco de dados local.  
  
5.  Clique com o botão direito no nó **TradeDev** e selecione **Nova Consulta**.  
  
6.  No painel de script, cole este código e clique no botão **Executar Consulta** para executar a consulta.  
  
    ```  
    select * from dbo.GetProductsBySupplier(1)  
    ```  
  
7.  O painel **Mensagem** mostra (0 linha afetada), e o painel de **Resultados** não retorna nenhuma linha. Isto é porque nós estamos consultando o banco de dados local em vez do banco de dados conectado que de fato contém dados reais.  
  
    Você pode confirmar isto clicando com o botão direito na tabela **Produtos** neste banco de dados local **TradeDev** e selecionar **Exibir Dados**. Observe que a tabela está vazia.  
  
### <a name="to-replicate-real-data-to-the-local-database"></a>Para replicar os dados reais no banco de dados local  
  
1.  No **Pesquisador de Objetos do SQL Server**, expanda a instância do SQL Server conectada e localize o banco de dados do **TradeDev**.  
  
    Clique com o botão direito do mouse na tabela **Fornecedores** e selecione **Exibir Dados**.  
  
2.  Clique no botão **Script** (o segundo botão a partir da direita) no alto do Editor de Dados. Copiar as instruções `INSERT` do script.  
  
3.  Expanda a instância de servidor **Local** e clique com o botão direito no nó **TradeDev**, selecione **Nova Consulta**.  
  
4.  Cole as instruções `INSERT` nesta janela de consulta e execute a consulta.  
  
5.  Repita as etapas anteriores para replicar dados das tabelas **Products** e **Fruits** no banco de dados **TradeDev** conectado para o banco de dados **TradeDev** local.  
  
6.  Clique com o botão direito na instância de servidor **Local** e selecione **Atualizar**. Examine as tabelas usando **Exibir Dados** para verificar se o banco de dados local foi populado.  
  
7.  Clique com o botão direito no nó **TradeDev** da instância de servidor Local e selecione **Nova Consulta**.  
  
8.  No painel de script, cole este código e clique no botão **Executar Consulta** para executar a consulta.  
  
    ```  
    select * from dbo.GetProductsBySupplier(1)  
    ```  
  
9. No painel **Resultados**, abaixo do painel Editor Transact\-SQL, você verá que serão retornadas as linhas Maçãs e Batatas fritas da tabela `Products`.  
  
