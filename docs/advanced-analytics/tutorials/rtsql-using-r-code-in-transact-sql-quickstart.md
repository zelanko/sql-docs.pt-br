---
title: "Usando o código R no Transact-SQL (R no início rápido do SQL) | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 08/20/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2016
dev_langs:
- R
ms.assetid: 4e6fe30d-a105-4d5b-bc05-5e5204753847
caps.latest.revision: 36
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: c023af0a3a9b9c53cb2b6adf7298c18657a60803
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="using-r-code-in-transact-sql-r-in-sql-quickstart"></a>Usando o código R no Transact-SQL (R no início rápido do SQL)

Este tutorial orienta a mecânica básica de chamar um script R de um procedimento armazenado T-SQL.

**Você aprenderá**

+ Como inserir o R em uma função T-SQL
+ Algumas dicas para trabalhar com R e SQL objetos de dados e tipos de dados
+ Como criar um modelo simples e salvá-lo para o SQL Server
+ Como criar previsões e um gráfico de R usando o modelo

**Tempo estimado**

30 minutos, não incluindo a instalação

## <a name="prerequisites"></a>Pré-requisitos

Você deve ter acesso a uma instância do SQL Server com um dos seguintes já instalados:

+ SQL Server 2017 Machine Learning Services, com a linguagem R instalada
+ SQL Server 2016 R Services

A instância do SQL Server pode estar em uma máquina virtual do Azure ou no local. Apenas lembre-se de que o recurso de script externo é desabilitado por padrão, portanto, talvez seja necessário executar algumas etapas adicionais para que isso funcione.

Para executar consultas SQL que incluem script R, você pode usar qualquer outro aplicativo que possa se conectar a um banco de dados e executar o código T-SQL. Profissionais do SQL podem usar o SQL Server Management Studio (SSMS) ou o Visual Studio.

Para este tutorial, para mostrar como é fácil executar R dentro do SQL Server, usamos o novo **extensão mssql para o código do Visual Studio**. Código do VS é um ambiente de desenvolvimento gratuito que pode ser executado em Windows, macOS ou Linux. O **mssql*** extensão é uma extensão leve para execução de consultas do SLq. Para instalá-lo, consulte este artigo: [Usar a extensão mssql para Visual Studio Code](https://docs.microsoft.com/sql/linux/sql-server-linux-develop-use-vscode).

## <a name="connect-to-a-database-and-run-a-hello-world-test-script"></a>Conectar-se ao banco de dados e executar um script de teste do Olá, Mundo

1. No Visual Studio Code, crie um novo arquivo de texto e nomeie-o BasicRSQL.sql.
2. Enquanto este arquivo estiver aberto, pressione CTRL + SHIFT + P (COMMAND + P em um macOS), digite **sql** para listar os comandos SQL e, em seguida, selecione **CONECTAR**. Código do Visual Studio solicita que você criar um perfil para usar ao se conectar a um banco de dados específico. Isso é opcional, mas torna mais fácil alternar entre bancos de dados e logons.
    + Escolha um servidor ou instância onde R no SQL Server foi instalado.
    + Use uma conta que tenha permissões para criar um novo banco de dados, execute as instruções SELECT e exiba as definições de tabela.
2. Se a conexão for bem-sucedida, você deverá ser capaz de ver o servidor e o nome do banco de dados na barra de status, juntamente com suas credenciais atuais. Se a conexão falhar, verifique se o nome do servidor e o nome do computador estão corretos.
3. Cole essa instrução e execute-a.

    ```sql
    EXEC sp_execute_external_script
      @language =N'R',
      @script=N'OutputDataSet<-InputDataSet',
      @input_data_1 =N'SELECT 1 AS hello'
      WITH RESULT SETS (([hello] int not null));
    GO
    ```

    No Visual Studio Code, você pode realçar o código que deseja executar e pressionar CTRL + SHIFT + E. Se isso for muito difícil lembrar, você poderá alterá-lo! Consulte [Personalizar as associações de teclas de atalho](https://github.com/Microsoft/vscode-mssql/wiki/customize-shortcuts).

    ![rsql-basictut_hello1code](media/rsql-basictut-hello1code.PNG)

**Resultados**

![rsql_basictut_hello1](media/rsql-basictut-hello1.PNG)

## <a name="troubleshooting"></a>Solução de problemas

+ Se você receber erros dessa consulta, a instalação pode estar incompleta. Depois de adicionar o recurso usando o Assistente de instalação do SQL Server, você deve executar algumas etapas adicionais para habilitar o uso de bibliotecas de código externo.  Consulte [Configurar o SQL Server R Services](../r/set-up-sql-server-r-services-in-database.md).

+ Certifique-se de que o serviço Launchpad está sendo executado. Dependendo do seu ambiente, você pode precisar habilitar as contas de trabalho R para se conectar ao SQL Server, instalar bibliotecas de rede adicional, habilitar a execução remota de código ou reiniciar a instância depois que tudo estiver configurado. Consulte [Perguntas frequentes sobre a instalação e a atualização dos R Services](../r/upgrade-and-installation-faq-sql-server-r-services.md)

+ Para obter o Visual Studio Code, consulte [Baixar e instalar o Visual Studio Code](https://code.visualstudio.com/Download).

## <a name="next-lesson"></a>Próxima lição

Agora que a instância está pronta para trabalhar com R, vamos começar.

Lição 1: [trabalhando com entradas e saídas](rtsql-working-with-inputs-and-outputs.md)

Lição 2: [R e SQL objetos de dados e tipos de dados](rtsql-r-and-sql-data-types-and-data-objects.md)

Lição 3: [funções usando R com dados do SQL Server](rtsql-using-r-functions-with-sql-server-data.md)

Lição 4: [criar um modelo de previsão](rtsql-create-a-predictive-model-r.md)

Lição 5: [prever e plotar do modelo](rtsql-predict-and-plot-from-model.md)

