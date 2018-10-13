---
title: Guia de início rápido para uma execução de código "Hello World" básico R no T-SQL (aprendizado de máquina do SQL Server) | Microsoft Docs
description: Guia de início rápido para o script de R no SQL Server. Conheça os fundamentos de chamar o script de R usando o procedimento armazenado do sistema sp_execute_external_script um exercício de Olá, mundo.
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/08/2018
ms.topic: quickstart
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 1a51fcb9e67bef48346ff74ebfb1e911a6ee3365
ms.sourcegitcommit: ce4b39bf88c9a423ff240a7e3ac840a532c6fcae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/09/2018
ms.locfileid: "48878079"
---
# <a name="quickstart-hello-world-r-script-in-sql-server"></a>Guia de início rápido: Script de R "Hello world" no SQL Server 
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

SQL Server inclui o suporte à linguagem de R para análises de ciência de dados em dados do SQL Server residentes. Seu script R pode consistir em funções de R de código-fonte aberto, bibliotecas de R de terceiros ou bibliotecas internas do Microsoft R, como [RevoScaleR](../r/revoscaler-overview.md) para análise preditiva em grande escala. 

Execução do script é por meio de procedimentos armazenados, usando qualquer uma das seguintes abordagens:

+ Interna [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql) procedimento armazenado, passando o script R no como um parâmetro de entrada.
+ Encapsular o script de R em um [procedimento armazenado de personalizado](sqldev-in-database-r-for-sql-developers.md) criado por você.

Neste início rápido, você aprenderá conceitos-chave, executando um "Hello World" R script inT-SQL, uma introdução para o **sp_execute_external_script** procedimento armazenado do sistema. 

## <a name="prerequisites"></a>Prerequisites

Este exercício exige o acesso a uma instância do SQL Server com um dos seguintes já instalados:

+ [Serviços de aprendizado de máquina do SQL Server 2017](../install/sql-machine-learning-services-windows-install.md), com a linguagem R instalada
+ [SQL Server 2016 R Services](../install/sql-r-services-windows-install.md)

  Instância do SQL Server pode estar em uma máquina virtual do Azure ou no local. Apenas lembre-se de que o recurso de script externo é desabilitado por padrão, portanto, talvez você precise [habilitar scripts externos](../install/sql-machine-learning-services-windows-install.md#bkmk_enableFeature) e verifique **Launchpad do SQL Server service** está em execução antes de começar.

+ Uma ferramenta para executar consultas SQL. Você pode usar qualquer aplicativo que possa se conectar a um banco de dados do SQL Server e executar o código T-SQL. Os profissionais do SQL podem usar o SQL Server Management Studio (SSMS) ou o Visual Studio.

Para este início rápido, para mostrar como é fácil executar R dentro do SQL Server, usamos o novo **extensão mssql para Visual Studio Code**. VS Code é um ambiente de desenvolvimento gratuito que pode ser executados no Windows, Linux ou macOS. O **mssql** extensão é uma extensão leve para execução de consultas T-SQL. Para obter o Visual Studio Code, consulte [Baixar e instalar o Visual Studio Code](https://code.visualstudio.com/Download). Para adicionar o **mssql** extensão, consulte este artigo: [usar a extensão mssql para Visual Studio Code](https://docs.microsoft.com/sql/linux/sql-server-linux-develop-use-vscode).

## <a name="connect-to-a-database-and-run-a-hello-world-test-script"></a>Conectar-se ao banco de dados e executar um script de teste do Olá, Mundo

1. No Visual Studio Code, crie um novo arquivo de texto e nomeie-o BasicRSQL.sql.

2. Enquanto este arquivo estiver aberto, pressione CTRL + SHIFT + P (COMMAND + P em um macOS), digite **sql** para listar os comandos SQL e, em seguida, selecione **CONECTAR**. Visual Studio Code solicitará que você crie um perfil para usar ao se conectar a um banco de dados específico. Isso é opcional, mas torna mais fácil alternar entre bancos de dados e logons.
    + Escolha um servidor ou instância em que R no SQL Server foi instalado.
    + Use uma conta que tenha permissões para criar um novo banco de dados, execute as instruções SELECT e exiba as definições de tabela.

2. Se a conexão for bem-sucedida, você deverá ser capaz de ver o servidor e o nome do banco de dados na barra de status, juntamente com suas credenciais atuais. Se a conexão falhar, verifique se o nome do servidor e o nome do computador estão corretos.

3. Cole essa instrução e execute-a.

    ```sql
    EXEC sp_execute_external_script
      @language =N'R',
      @script=N'OutputDataSet<-InputDataSet',
      @input_data_1 =N'SELECT 1 AS hello'
      WITH RESULT SETS (([Hello World] int));
    GO
    ```

Entradas para esse procedimento armazenado incluem:

+ *@language* parâmetro define a extensão da linguagem para chamar, nesse caso, R.
+ *@script* o parâmetro define os comandos transmitidos para o tempo de execução de R. Todo o script R deve ser colocado neste argumento, como texto Unicode. Você também pode adicionar texto a uma variável do tipo **nvarchar** e chamar a variável.
+ *@input_data_1* dados são retornados pela consulta, passada para o tempo de execução de R, que retorna os dados para o SQL Server como um quadro de dados.
+ COM conjuntos de resultados cláusula define o esquema da tabela de dados retornados para o SQL Server, adicionando "Hello World" como o nome da coluna **int** para o tipo de dados.

**Resultados**

![rsql_basictut_hello1](media/rsql-basictut-hello1.PNG)

Se você receber erros dessa consulta, a regra os problemas de instalação. Configuração de pós-instalação é necessária para habilitar o uso de bibliotecas de código externo. Ver [instalar serviços de aprendizado de máquina do SQL Server 2017](../install/sql-machine-learning-services-windows-install.md) ou [instalar o SQL Server 2016 R Services](../install/sql-r-services-windows-install.md). Da mesma forma, certifique-se de que o serviço Launchpad está em execução. 

Dependendo do seu ambiente, você pode precisar habilitar as contas de trabalho R para se conectar ao SQL Server, instalar bibliotecas de rede adicional, habilitar a execução remota de código ou reiniciar a instância depois que tudo estiver configurado. Para obter mais informações, consulte [perguntas frequentes sobre atualização e instalação de serviços de R](../r/upgrade-and-installation-faq-sql-server-r-services.md)

> [!TIP]
> No Visual Studio Code, você pode realçar o código que deseja executar e pressionar CTRL + SHIFT + E. Se isso for muito difícil lembrar, você poderá alterá-lo! Consulte [Personalizar as associações de teclas de atalho](https://github.com/Microsoft/vscode-mssql/wiki/customize-shortcuts).
> 
> ![rsql-basictut_hello1code](media/rsql-basictut-hello1code.PNG)
> 

## <a name="next-steps"></a>Próximas etapas

Agora que você confirmou a que sua instância estiver pronta para trabalhar com R, dar uma olhada mais próxima na estruturação de entradas e saídas.

> [!div class="nextstepaction"]
> [Guia de início rápido: Lidar com entradas e saídas](rtsql-working-with-inputs-and-outputs.md)
