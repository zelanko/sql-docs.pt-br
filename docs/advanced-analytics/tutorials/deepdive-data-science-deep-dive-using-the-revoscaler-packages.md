---
title: Tutorial sobre como o RevoScaleR funciona com o SQL Server Machine Learning | Microsoft Docs
description: Neste tutorial, saiba como chamar a função RevoScaleR no aprendizado de máquina do SQL Server com suporte de R habilitada.
ms.prod: sql
ms.technology: machine-learning
ms.date: 07/15/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: ee810c998f8aecf17c3496540c65471e0b29e102
ms.sourcegitcommit: a083e9d59e2014a06cda9138b7e17c17ecab90e0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/11/2018
ms.locfileid: "44343081"
---
# <a name="tutorial-use-revoscaler-r-functions-with-sql-server-data"></a>Tutorial: Funções de usam RevoScaleR R com dados do SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

RevoScaleR é um pacote do Microsoft R fornecendo processamento paralelo e distribuído para ciência de dados e cargas de trabalho de aprendizado de máquina. Para o desenvolvimento de R no SQL Server, RevoScaleR é um dos pacotes internos core, com funções para definir um contexto de computação, gerenciamento de pacotes e o mais importante: Trabalhando com dados – a ponta, da importação para análise e visualização. Algoritmos de aprendizado de máquina no SQL Server têm uma dependência em fontes de dados de RevoScaleR. Dada a importância do RevoScaleR, sabendo quando e como chamar as funções é uma habilidade essencial. 

Neste tutorial, você aprenderá a criar um contexto de computação remota, mover dados entre contextos de computação local e remoto e executar código R em um SQL Server remoto. Você também aprenderá como analisar e plotar os dados localmente e no servidor remoto e criar e implantar modelos.

+ Inicialmente, os dados são obtidos dos arquivos CSV ou XDF. Importar os dados para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando as funções no pacote RevoScaleR.
+ Modelo de treinamento e pontuação é realizada usando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] contexto de computação. 
+ Usar funções RevoScaleR para criar um novo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tabelas para salvar os resultados da pontuação.
+ Criar plotagens tanto no servidor e o contexto de computação local.
+ Treinar um modelo de dados no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] banco de dados, executar o R no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instância.
+ Extrair um subconjunto de dados e salvá-lo como um arquivo XDF para reutilização na análise na sua estação de trabalho local.
+ Obter novos dados para pontuação, abrindo uma conexão ODBC para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] banco de dados. Pontuação, isso é feito na estação de trabalho local.
+ Criar uma função personalizada do R e executá-lo no servidor de contexto de computação para realizar uma simulação.

## <a name="target-audience"></a>Público-alvo

Este tutorial destina-se para os cientistas de dados ou para pessoas que já estão um pouco familiarizadas com R e com tarefas de ciência de dados, como criação de modelo e resumos. No entanto, todo o código é fornecido, portanto, mesmo se você for novo no R, você pode executar o código e acompanhar, supondo que você tenha os ambientes de cliente e de servidor necessários.

Você também deve estar familiarizado com o [!INCLUDE[tsql](../../includes/tsql-md.md)] sintaxe e saber como acessar um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] banco de dados usando ferramentas como estes:

+ [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 
+ Ferramentas de banco de dados no Visual Studio 
+ A versão gratuita [extensão mssql para Visual Studio Code](https://docs.microsoft.com/sql/linux/sql-server-linux-develop-use-vscode).
  
> [!TIP]
> Salve seu espaço de trabalho do R entre as lições para que você possa facilmente selecionar a seção em que parou.

## <a name="prerequisites"></a>Prerequisites

- **SQL Server com suporte para R**
  
    Instale [serviços do SQL Server 2017 Machine Learning](../install/sql-machine-learning-services-windows-install.md) com o recurso do R, ou instale [SQL Server 2016 R Services (no banco de dados)](../install/sql-r-services-windows-install.md).

    Verifique se o script externo está habilitado, serviço Launchpad está em execução e se você tem permissões para acessar o serviço.
  
-  **Permissões de banco de dados**
  
    Para executar as consultas usadas para treinar o modelo, você deve ter privilégios **db_datareader** no banco de dados em que os dados são armazenados. Para executar o R, o usuário deve ter a permissão, EXECUTE ANY EXTERNAL SCRIPT.

-   **Computador de desenvolvimento de ciência de dados**
  
    Para alternar entre contextos de computação local e remota, você precisa de dois sistemas. Normalmente, o local é uma estação de trabalho de desenvolvimento com potência suficiente para cargas de trabalho de ciência de dados. Remoto nesse caso é o SQL Server 2017 ou o SQL Server 2016 com o recurso R habilitado. 
    
    Alternar contextos de computação se baseia em ter a mesma versão RevoScaleR em sistemas locais e remotos. Em uma estação de trabalho local, você pode obter os pacotes RevoScaleR e os provedores relacionados ao instalar ou usar qualquer um dos seguintes: [VM de ciência de dados no Azure](https://docs.microsoft.com/azure/machine-learning/data-science-virtual-machine/overview), [(gratuito) do Microsoft R Client](https://docs.microsoft.com/en-us/machine-learning-server/r-client/what-is-microsoft-r-client), ou [ Microsoft Machine Learning Server (autônomo)](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-install). Para a opção de servidor autônomo, instale a edição de desenvolvedor gratuitas, usando os instaladores do Linux ou Windows. Você também pode usar a instalação do SQL Server para instalar um servidor autônomo.
      
-   **Pacotes do R adicionais**
  
    Neste tutorial, você pode instalar os seguintes pacotes: **dplyr**, **ggplot2**, **ggthemes**, **reshape2**, e **e1071** . Instruções são fornecidas como parte do tutorial.
  
    Todos os pacotes devem ser instalados em dois locais: na estação de trabalho usado para o desenvolvimento de soluções de R e no computador do SQL Server em que os scripts R são executados. Se você não tem permissão para instalar pacotes no computador do servidor, peça ao administrador. 
    
    **Não instale os pacotes em uma biblioteca do usuário.** Os pacotes devem ser instalados na biblioteca de pacote do R que é usada pela instância do SQL Server.

## <a name="r-development-tools"></a>Ferramentas de desenvolvimento R

Normalmente, os desenvolvedores do R usam IDEs para escrever e depurar o código R. Aqui estão algumas sugestões:

- **Ferramentas do R para Visual Studio** (RTVS) é um plug-in que fornece o Intellisense, depuração e suporte para o Microsoft R. Você pode usá-lo com o R Server e serviços do SQL Server Machine Learning. Para baixar, consulte [R Tools para Visual Studio](https://www.visualstudio.com/vs/rtvs/).

- O**RStudio** é um dos ambientes mais populares para desenvolvimento do R. Para obter mais informações, consulte [ https://www.rstudio.com/products/RStudio/ ](https://www.rstudio.com/products/RStudio/).

- Ferramentas básicas de R (R.exe, RTerm.exe, RScripts.exe) também são instaladas por padrão, quando você instala o R no SQL Server ou cliente do R. Se você não quiser instalar um IDE, você pode usar as ferramentas internas de R para executar o código neste tutorial.

Lembre-se de que o RevoScaleR é necessário em computadores locais e remotos. Você não pode concluir este tutorial usando uma instalação genérica do RStudio ou outro ambiente que está faltando as bibliotecas do Microsoft R. Para obter mais informações, consulte [Configurar um cliente de ciência de dados](../r/set-up-a-data-science-client.md).

## <a name="next-steps"></a>Próximas etapas

> [!div class="nextstepaction"]
> [Lição 1: Criar o banco de dados e permissões](deepdive-work-with-sql-server-data-using-r.md)

