---
title: Análise aprofundada do tutorial – SQL Server Machine Learning de função RevoScaleR
description: Neste tutorial, saiba como chamar funções de RevoScaleR, usando a integração de R do SQL Server Machine Learning.
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/27/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.openlocfilehash: 28f3ebe1887e188513c01881f68d5d7f323e31f2
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67962240"
---
# <a name="tutorial-use-revoscaler-r-functions-with-sql-server-data"></a>Tutorial: Usar funções RevoScaleR R com dados do SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

[RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) é um pacote do Microsoft R fornecendo distribuídos e processamento paralelo para ciência de dados e cargas de trabalho de aprendizado de máquina. Para o desenvolvimento de R no SQL Server **RevoScaleR** é uma das principais pacotes internos, com funções para criar objetos de fonte de dados, definindo um contexto de computação, gerenciamento de pacotes e o mais importante: Trabalhando com dados de ponta a ponta, na importação para análise e visualização. Algoritmos de aprendizado de máquina no SQL Server têm uma dependência **RevoScaleR** fontes de dados. Dada a importância da **RevoScaleR**, sabendo quando e como chamar as funções é uma habilidade essencial. 

Neste tutorial com várias partes, você será apresentado a um intervalo de **RevoScaleR** funções para tarefas associadas com a ciência de dados. O processo, você aprenderá como criar um contexto de computação remota, mover dados entre contextos de computação local e remota e executar código R em um SQL Server remoto. Você também aprenderá como analisar e plotar os dados localmente e no servidor remoto e criar e implantar modelos.

## <a name="prerequisites"></a>Pré-requisitos

+ [Serviços de aprendizado de máquina do SQL Server 2017](../install/sql-machine-learning-services-windows-install.md) com o recurso de R, ou [SQL Server 2016 R Services (no banco de dados)](../install/sql-r-services-windows-install.md)
  
+ [Permissões de banco de dados](../security/user-permission.md) e um logon de usuário de banco de dados do SQL Server

+ [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)

+ Um IDE, como RStudio ou a ferramenta interna do RGUI incluído com o R

Para alternar entre contextos de computação local e remota, você precisa de dois sistemas. Normalmente, o local é uma estação de trabalho de desenvolvimento com potência suficiente para cargas de trabalho de ciência de dados. Remoto nesse caso é o SQL Server 2017 ou o SQL Server 2016 com o recurso R habilitado. 

Alternar contextos de computação se baseia em ter a mesma versão **RevoScaleR** em sistemas locais e remotos. Em uma estação de trabalho local, você pode obter o **RevoScaleR** pacotes e provedores relacionados ao instalar o Microsoft R Client.

Se você precisar colocar o cliente e servidor no mesmo computador, certifique-se de instalar um segundo conjunto de bibliotecas do Microsoft R para o envio de script R de um cliente "remoto". Não use as bibliotecas do R que estão instaladas nos arquivos de programa da instância do SQL Server. Especificamente, se você estiver usando um computador, você precisa de **RevoScaleR** biblioteca em ambos esses locais para oferecer suporte a operações de cliente e servidor.

+ C:\Program Files\Microsoft\R Client\R_SERVER\library\RevoScaleR 
+ C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES\library\RevoScaleR

Para obter instruções sobre configuração de cliente, consulte [configurar um cliente de ciência de dados para o desenvolvimento de R](../r/set-up-a-data-science-client.md).


## <a name="r-development-tools"></a>Ferramentas de desenvolvimento R

Normalmente, os desenvolvedores do R usam IDEs para escrever e depurar o código R. Aqui estão algumas sugestões:

- **Ferramentas do R para Visual Studio** (RTVS) é um plug-in que fornece o Intellisense, depuração e suporte para o Microsoft R. Você pode usá-lo com o R Server e serviços do SQL Server Machine Learning. Para baixar, consulte [R Tools para Visual Studio](https://www.visualstudio.com/vs/rtvs/).

- O**RStudio** é um dos ambientes mais populares para desenvolvimento do R. Para obter mais informações, consulte [ https://www.rstudio.com/products/RStudio/ ](https://www.rstudio.com/products/RStudio/).

- Ferramentas básicas de R (R.exe, RTerm.exe, RScripts.exe) também são instaladas por padrão, quando você instala o R no SQL Server ou cliente do R. Se você não quiser instalar um IDE, você pode usar as ferramentas internas de R para executar o código neste tutorial.

Lembre-se de que **RevoScaleR** é necessário nos computadores locais e remotos. Você não pode concluir este tutorial usando uma instalação genérica do RStudio ou outro ambiente que está faltando as bibliotecas do Microsoft R. Para obter mais informações, consulte [Configurar um cliente de ciência de dados](../r/set-up-a-data-science-client.md).

## <a name="summary-of-tasks"></a>Resumo de tarefas

+ Inicialmente, os dados são obtidos dos arquivos CSV ou XDF. Importar os dados para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando as funções a **RevoScaleR** pacote.
+ Modelo de treinamento e pontuação é realizada usando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] contexto de computação. 
+ Use **RevoScaleR** funções para criar um novo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tabelas para salvar os resultados da pontuação.
+ Criar plotagens tanto no servidor e o contexto de computação local.
+ Treinar um modelo de dados no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] banco de dados, executar o R no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instância.
+ Extrair um subconjunto de dados e salvá-lo como um arquivo XDF para reutilização na análise na sua estação de trabalho local.
+ Obter novos dados para pontuação, abrindo uma conexão ODBC para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] banco de dados. Pontuação, isso é feito na estação de trabalho local.
+ Criar uma função personalizada do R e executá-lo no servidor de contexto de computação para realizar uma simulação.

## <a name="next-steps"></a>Próximas etapas

> [!div class="nextstepaction"]
> [Lição 1: Criar banco de dados e permissões](deepdive-work-with-sql-server-data-using-r.md)