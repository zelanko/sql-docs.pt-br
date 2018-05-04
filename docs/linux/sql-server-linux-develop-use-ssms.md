---
title: Gerenciar o SQL Server no Linux com o SSMS | Microsoft Docs
description: Este tutorial mostra como usar o SQL Server Management Studio no Windows para se conectar ao SQL Server em execução no Linux.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 10/02/2017
ms.topic: article
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: ''
ms.suite: sql
ms.custom: sql-linux
ms.technology: database-engine
ms.assetid: 30cc4564-f389-4707-9b25-8ba782cc5150
ms.openlocfilehash: 95f97fdb3b35d50e671f9569a8b58315014fc509
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="use-sql-server-management-studio-ssms-on-windows-to-manage-sql-server-on-linux"></a>Use o SQL Server Management Studio (SSMS) no Windows para gerenciar o SQL Server no Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Este artigo mostra como usar [SQL Server Management Studio (SSMS)](../ssms/download-sql-server-management-studio-ssms.md) para se conectar ao SQL Server 2017 no Linux. O SSMS é um aplicativo do Windows, então use SSMS, quando você tiver um computador Windows que pode se conectar a uma instância remota do SQL Server no Linux.

Depois de se conectar com êxito, você deve executar uma consulta simples do Transact-SQL (T-SQL) para verificar a comunicação com o banco de dados.

## <a name="install-the-newest-version-of-sql-server-management-studio"></a>Instale a versão mais recente do SQL Server Management Studio

Ao trabalhar com o SQL Server, você deve usar sempre a versão mais recente do SQL Server Management Studio (SSMS). A versão mais recente do SSMS está sempre atualizada e otimizados e funciona atualmente com o SQL Server 2017 em Linux. Para baixar e instalar a versão mais recente, consulte [baixar o SQL Server Management Studio](../ssms/download-sql-server-management-studio-ssms.md). Para se manter atualizado, a versão mais recente do SSMS avisa você quando há uma nova versão disponível para download. 

## <a name="connect-to-sql-server-on-linux"></a>Conecte-se ao SQL Server no Linux

As etapas a seguir mostram como se conectar ao SQL Server 2017 no Linux com o SSMS.

1. Inicie o SSMS digitando **Microsoft SQL Server Management Studio** nas janelas de caixa de pesquisa e, em seguida, clique no aplicativo de área de trabalho.

    ![SQL Server Management Studio](./media/sql-server-linux-develop-use-ssms/ssms.png)

2. No **conectar ao servidor** janela, insira as informações a seguir (se já estiver executando o SSMS, clique em **conectar > mecanismo de banco de dados** para abrir o **conectar ao servidor** janela):

   | Configuração | Description |
   |-----|-----|
   | **Tipo de servidor** | O padrão é o mecanismo de banco de dados; Não altere esse valor. |
   | **Nome do servidor** | Insira o nome do computador do SQL Server do Linux de destino ou endereço IP. |
   | **Autenticação** | Para o SQL Server de 2017 no Linux, use **autenticação do SQL Server**. |
   | **Logon** | Insira o nome de um usuário com acesso ao banco de dados no servidor (por exemplo, o padrão **SA** conta criada durante a instalação). |
   | **Senha** | Digite a senha para o usuário especificado (para o **SA** conta, você criou esse durante a instalação). |

    ![SQL Server Management Studio: Conectar-se ao servidor de banco de dados SQL](./media/sql-server-linux-develop-use-ssms/connect.png)

3. Clique em **Conectar**.

    > [!TIP]
    > Se houver uma falha de conexão, primeiro, tente diagnosticar o problema da mensagem de erro. Em seguida, examine as [recomendações de solução de problemas de conexão](sql-server-linux-troubleshooting-guide.md#connection).
 
5. Depois de se conectar com êxito para o SQL Server **Pesquisador de objetos** é aberto e você agora pode acessar o banco de dados para executar tarefas administrativas ou consultar dados.
 
     ![Pesquisador de objetos](./media/sql-server-linux-develop-use-ssms/object-explorer.png)
     
## <a name="run-sample-queries"></a>Executar consultas de exemplo

Depois de se conectar ao seu servidor, você pode se conectar a um banco de dados e executar uma consulta de exemplo. Se você for novo para escrever consultas, consulte [escrever instruções de Transact-SQL](../t-sql/tutorial-writing-transact-sql-statements.md).

1. Identifica um banco de dados para usar para executar uma consulta. Isso pode ser um novo banco de dados criado na [tutorial do Transact-SQL](../t-sql/tutorial-writing-transact-sql-statements.md). Ou poderia ser o **AdventureWorks** exemplo de banco de dados que você [baixado e restaurado](sql-server-linux-migrate-restore-database.md).
2. Em **Pesquisador de objetos**, navegue até o banco de dados de destino no servidor.
2. O banco de dados e, em seguida, selecione **nova consulta**:

    ![Nova consulta. Se conectar ao banco de dados do SQL server: SQL Server Management Studio](./media/sql-server-linux-develop-use-ssms/new-query.png)

3. Na janela de consulta, escreva uma consulta Transact-SQL para selecionar uma das tabelas de dados. O exemplo a seguir seleciona dados do **Production. Product** analítico o **AdventureWorks** banco de dados.

        SELECT TOP 10 Name, ProductNumber
        FROM Production.Product
        ORDER BY Name ASC

4. Clique o **Execute** botão:

    ![Sucesso. Se conectar ao banco de dados do SQL server: SQL Server Management Studio](./media/sql-server-linux-develop-use-ssms/execute-query.png)

## <a name="next-steps"></a>Próximas etapas

Além das consultas, você pode usar instruções T-SQL para criar e gerenciar bancos de dados.

Se você estiver familiarizado com o T-SQL, consulte [Tutorial: gravando instruções de Transact-SQL](../t-sql/tutorial-writing-transact-sql-statements.md) e [referência Transact-SQL (mecanismo de banco de dados)](https://msdn.microsoft.com/library/bb510741.aspx).

Para obter mais informações sobre como usar o SSMS, consulte [usar o SQL Server Management Studio](https://msdn.microsoft.com/library/ms174173.aspx).
