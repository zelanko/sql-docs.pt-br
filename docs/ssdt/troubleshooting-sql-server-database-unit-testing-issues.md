---
title: Solucionar problemas de teste de unidade do banco de dados SQL Server | Microsoft Docs
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: cf4c9cd1-7e73-4c3b-922a-68b9247e7b33
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 0a6a198d252f2363fc55e38677518ec02724e3e2
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65102016"
---
# <a name="troubleshooting-sql-server-database-unit-testing-issues"></a>Solucionando problemas de teste de unidade do banco de dados SQL Server
Você pode encontrar os problemas neste tópico quando trabalha com as unidades de teste do SQL Server em um banco de dados:  
  
-   [Teste de unidade e alterações do App.Config ignoradas quando você executa testes de unidade](#UnitTestingAndAppConfigChanges)  
  
-   [Implantação de banco de dados em destinos inesperados quando você executa testes de unidade](#DatabaseDeploymentInUnitTests)  
  
-   [Tempo limite quando você executa testes de unidade de banco de dados](#TimeoutsDuringUnitTests)  
  
## <a name="UnitTestingAndAppConfigChanges"></a>Teste de unidade e alterações do App.Config ignoradas quando você executa testes de unidade  
Se você modificar o arquivo App.Config no projeto de teste, deverá recompilar o projeto de teste antes de essas alterações entrarem em vigor. Essas alterações incluem as que você faz no App.Config usando a caixa de diálogo **Configuração de Teste do SQL Server**. Se você não recompilar o projeto de teste, as alterações não serão aplicadas quando você executar os testes de unidade.  
  
## <a name="DatabaseDeploymentInUnitTests"></a>Implantação de banco de dados em destinos inesperados quando você executa testes de unidade  
Se você implantar um banco de dados de um projeto de banco de dados quando executa testes de unidade, o banco de dados é implantado usando as informações da cadeia de conexão que são especificadas em sua configuração de teste de unidade. As informações da cadeia de conexão que são especificadas nas propriedades de depuração do projeto de banco de dados não são usadas para esta tarefa, o que permite que você execute os testes de unidade do SQL Server em diferentes instâncias do mesmo banco de dados.  
  
## <a name="TimeoutsDuringUnitTests"></a>Tempo limite quando você executa testes de unidade de banco de dados  
Se seus testes de unidade de banco de dados estão falhando devido a tempo limite, você poderá aumentar o período de tempo limite atualizando o arquivo app.config em seu projeto de teste. O tempo limite de conexão, definido na cadeia de conexão, especifica quanto tempo aguardar quando o teste de unidade se conecta ao servidor. O tempo limite de comando, que deve ser definido diretamente no arquivo app.config especifica quanto tempo aguardar quando o teste de unidade executa o script Transact\-SQL. Se você tiver problemas com testes de unidade de execução longa, tente aumentar o valor do tempo limite de comando no elemento de contexto apropriado. Por exemplo, para especificar um tempo limite de comando de 120 segundos para o elemento **PrivilegedContext**, atualize o app.config da seguinte maneira:  
  
```  
<SqlUnitTesting_VS2010>  
    <DatabaseDeployment DatabaseProjectFileName="..\..\..\..\..\..\Visual Studio 2010\Projects\Database10\Database10\AdventureWorks.sqlproj"  
        Configuration="Debug" />  
    <DataGeneration ClearDatabase="true" />  
    <ExecutionContext Provider="System.Data.SqlClient" ConnectionString="Data Source=(LocalDB)\Projects;Initial Catalog=AdventureWorks_Test;Integrated Security=True;Pooling=False"  
        CommandTimeout="30" />  
    <PrivilegedContext Provider="System.Data.SqlClient" ConnectionString="Data Source=(LocalDB)\Projects;Initial Catalog=AdventureWorks_Test;Integrated Security=True;Pooling=False"  
        CommandTimeout="120" />  
</SqlUnitTesting_VS2010>  
```  
  
## <a name="see-also"></a>Consulte Também  
[Como: Criar testes de unidade do SQL Server para funções, gatilhos e procedimentos armazenados](../ssdt/how-to-create-unit-tests-for-functions-triggers-stored-procedures.md)  
[Como: configurar a execução do teste de unidade do SQL Server](../ssdt/how-to-configure-sql-server-unit-test-execution.md)  
  
