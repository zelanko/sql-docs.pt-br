---
title: Tutorial de aprofundamento da função RevoScaleR-SQL Server Machine Learning
description: Neste tutorial, saiba como chamar funções RevoScaleR usando a integração do SQL Server Machine Learning R.
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/27/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.openlocfilehash: c326d51e9b3ac4edac61f97bf5f7fa3143d8d350
ms.sourcegitcommit: 9062c5e97c4e4af0bbe5be6637cc3872cd1b2320
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/24/2019
ms.locfileid: "68470626"
---
# <a name="tutorial-use-revoscaler-r-functions-with-sql-server-data"></a>Tutorial: Usar funções do R RevoScaleR com dados de SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

O [RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) é um pacote do Microsoft R que fornece processamento paralelo e distribuído para cargas de trabalho de ciência de dados e de aprendizado de máquina. Para o desenvolvimento de R no SQL Server, o **RevoScaleR** é um dos pacotes internos principais, com funções para criar objetos de fonte de dados, definir um contexto de computação, gerenciar pacotes e o mais importante: trabalhando com dados de ponta a ponta, de importar para visualização e análise. Os algoritmos de Machine Learning no SQL Server têm uma dependência em fontes de dados **RevoScaleR** . Considerando a importância do **RevoScaleR**, saber quando e como chamar suas funções é uma habilidade essencial. 

Neste tutorial de várias partes, você é apresentado a uma variedade de funções **RevoScaleR** para tarefas associadas à ciência de dados. No processo, você aprenderá a criar um contexto de computação remota, mover dados entre contextos de computação locais e remotos e executar o código R em um SQL Server remoto. Você também aprende como analisar e plotar dados tanto localmente quanto no servidor remoto, e como criar e implantar modelos.

## <a name="prerequisites"></a>Pré-requisitos

+ [SQL Server 2017 serviços de Machine Learning](../install/sql-machine-learning-services-windows-install.md) com o recurso r ou [SQL Server 2016 R Services (no banco de dados)](../install/sql-r-services-windows-install.md)
  
+ [Permissões de banco de dados](../security/user-permission.md) e um logon de usuário de banco de dados SQL Server

+ [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)

+ Um IDE como RStudio ou a ferramenta RGUI interna incluída com R

Para alternar entre os contextos de computação local e remota, você precisa de dois sistemas. O local é normalmente uma estação de trabalho de desenvolvimento com suficientes Power para cargas de trabalho de ciência de dados. O remoto nesse caso é SQL Server 2017 ou SQL Server 2016 com o recurso R habilitado. 

A alternância de contextos de computação é predicada sobre ter a mesma versão **RevoScaleR** em sistemas locais e remotos. Em uma estação de trabalho local, você pode obter os pacotes **RevoScaleR** e provedores relacionados instalando Microsoft R Client.

Se você precisar colocar o cliente e o servidor no mesmo computador, certifique-se de instalar um segundo conjunto de bibliotecas do Microsoft R para enviar o script R de um cliente "remoto". Não use as bibliotecas de R que estão instaladas nos arquivos de programas da instância SQL Server. Especificamente, se você estiver usando um computador, precisará da biblioteca **RevoScaleR** em ambos os locais para dar suporte a operações de cliente e servidor.

+ C:\Arquivos de Files\Microsoft\R Client\R_SERVER\library\RevoScaleR 
+ C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES\library\RevoScaleR

Para obter instruções sobre a configuração do cliente, consulte [configurar um cliente de ciência de dados para o desenvolvimento de R](../r/set-up-a-data-science-client.md).


## <a name="r-development-tools"></a>Ferramentas de desenvolvimento R

Os desenvolvedores de r normalmente usam IDEs para escrever e depurar o código R. Aqui estão algumas sugestões:

- **Ferramentas do R para Visual Studio** (RTVS) é um plug-in gratuito que fornece IntelliSense, depuração e suporte para o Microsoft R. Você pode usá-lo com o R Server e o SQL Server Serviços de Machine Learning. Para baixar, consulte [R Tools para Visual Studio](https://www.visualstudio.com/vs/rtvs/).

- O**RStudio** é um dos ambientes mais populares para desenvolvimento do R. Para obter mais informações, [https://www.rstudio.com/products/RStudio/](https://www.rstudio.com/products/RStudio/)consulte.

- As ferramentas básicas do R (R. exe, RTerm. exe, RScripts. exe) também são instaladas por padrão quando você instala o R em SQL Server ou R Client. Se você não quiser instalar um IDE, poderá usar ferramentas de R internas para executar o código neste tutorial.

Lembre-se de que **RevoScaleR** é necessário em computadores locais e remotos. Você não pode concluir este tutorial usando uma instalação genérica do RStudio ou outro ambiente que não tem as bibliotecas do Microsoft R. Para obter mais informações, consulte [Configurar um cliente de ciência de dados](../r/set-up-a-data-science-client.md).

## <a name="summary-of-tasks"></a>Resumo das tarefas

+ Inicialmente, os dados são obtidos dos arquivos CSV ou XDF. Você importa os dados para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o usando as funções no pacote **RevoScaleR** .
+ O treinamento e a Pontuação do modelo são [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] executados usando o contexto de computação. 
+ Use as funções **RevoScaleR** para criar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] novas tabelas para salvar os resultados da pontuação.
+ Crie plotagens no servidor e no contexto de computação local.
+ Treine um modelo em dados no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] banco de dado, executando R [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] na instância.
+ Extraia um subconjunto de dados e salve-o como um arquivo XDF para reutilização na análise na estação de trabalho local.
+ Obtenha novos dados para pontuação, abrindo uma conexão ODBC com o banco [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de dados. A pontuação é feita na estação de trabalho local.
+ Crie uma função personalizada do R e execute-a no contexto de computação do servidor para executar uma simulação.

## <a name="next-steps"></a>Próximas etapas

> [!div class="nextstepaction"]
> [Lição 1: Criar banco de dados e permissões](deepdive-work-with-sql-server-data-using-r.md)