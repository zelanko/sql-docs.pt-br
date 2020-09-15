---
title: Tutorial de aprofundamento do RevoScaleR
description: Nesta série de tutoriais, saiba como chamar funções do RevoScaleR usando a integração ao R do Machine Learning do SQL Server.
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 11/27/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: ad18fc08a06a647c626972cf3b3141d9d9861c87
ms.sourcegitcommit: 9b41725d6db9957dd7928a3620fe4db41eb51c6e
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/13/2020
ms.locfileid: "88178793"
---
# <a name="tutorial-use-revoscaler-r-functions-with-sql-server-data"></a>Tutorial: Usar funções RevoScaleR do R com os dados do SQL Server
[!INCLUDE [SQL Server 2016 and later](../../includes/applies-to-version/sqlserver2016.md)]

Neste tutorial de várias partes, você conhecerá uma variedade de funções do **RevoScaleR** para tarefas associadas à ciência de dados. Ao mesmo tempo, aprenderá a criar um contexto de computação remoto, mover dados entre contextos de computação local e remota e executar o código R em um SQL Server remoto. Também aprenderá a analisar e plotar dados localmente e no servidor remoto e a criar e implantar modelos.

O [RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) é um pacote R da Microsoft que fornece processamento paralelo e distribuído para cargas de trabalho de ciência de dados e de aprendizado de máquina. Para o desenvolvimento do R no SQL Server, **RevoScaleR** é um dos principais pacotes internos, com funções para criar objetos de fonte de dados, definir um contexto de computação, gerenciar pacotes e o mais importante: trabalhar com os dados de ponta a ponta, de importação a visualização e análise. Os algoritmos de Machine Learning no SQL Server têm uma dependência de fontes de dados **RevoScaleR**. Considerando a importância do **RevoScaleR**, saber quando e como chamar suas funções é uma habilidade essencial. 

## <a name="prerequisites"></a>Pré-requisitos

+ [Serviços de Machine Learning do SQL Server](../install/sql-machine-learning-services-windows-install.md) com o recurso R ou [SQL Server R Services (no banco de dados)](../install/sql-r-services-windows-install.md)
  
+ [Permissões de banco de dados](../security/user-permission.md) e logon do usuário do Banco de Dados do SQL Server

+ [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)

+ Um IDE (como o RStudio) ou a ferramenta RGUI interna incluída com o R

Para alternar entre os contextos de computação local e remota, você precisa de dois sistemas. O local é normalmente uma estação de trabalho de desenvolvimento com energia suficiente para cargas de trabalho de ciência de dados. A remota, nesse caso, é o SQL Server com o recurso R habilitado. 

A alternância de contextos de computação é predicada em ter o **RevoScaleR** da mesma versão em sistemas locais e remotos. Em uma estação de trabalho local, você pode obter os pacotes **RevoScaleR** e provedores relacionados instalando o Microsoft R Client.

Se você precisar colocar o cliente e o servidor no mesmo computador, instale um segundo conjunto de bibliotecas do Microsoft R para enviar o script R de um cliente "remoto". Não use as bibliotecas do R instaladas nos arquivos de programas da instância do SQL Server. Especificamente, se você estiver usando um computador, precisará da biblioteca **RevoScaleR** em ambos os locais para dar suporte a operações de cliente e servidor.

+ C:\Program Files\Microsoft\R Client\R_SERVER\library\RevoScaleR 
+ C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES\library\RevoScaleR

Para obter instruções sobre a configuração da cliente, confira [Configurar um cliente de ciência de dados para o desenvolvimento do R](../r/set-up-a-data-science-client.md).


## <a name="r-development-tools"></a>Ferramentas de desenvolvimento do R

Normalmente, os desenvolvedores do R usam os IDEs para escrever e depurar o código R. Aqui estão algumas sugestões:

- O **RTVS** (Ferramentas do R para Visual Studio) é um plug-in gratuito que fornece o IntelliSense, depuração e suporte para o Microsoft R. Você pode usá-lo com o R Server e o Serviços de Machine Learning do SQL Server. Para baixar, consulte [R Tools para Visual Studio](https://marketplace.visualstudio.com/items?itemName=MikhailArkhipov007.RTVS2019).

- O**RStudio** é um dos ambientes mais populares para desenvolvimento do R. Para obter mais informações, confira [https://www.rstudio.com/products/RStudio/](https://www.rstudio.com/products/RStudio/).

- As ferramentas básicas do R (R.exe, RTerm.exe, RScripts.exe) também são instaladas por padrão quando você instala o R no SQL Server ou no R Client. Se não desejar instalar um IDE, você poderá usar as ferramentas do R internas para executar o código neste tutorial.

Lembre-se de que **RevoScaleR** é necessário em computadores locais e remotos. Não é possível concluir este tutorial usando uma instalação genérica do RStudio ou outro ambiente que não está nas bibliotecas do Microsoft R. Para obter mais informações, consulte [Configurar um cliente de ciência de dados](../r/set-up-a-data-science-client.md).

## <a name="summary-of-tasks"></a>Resumo de tarefas

+ Inicialmente, os dados são obtidos dos arquivos CSV ou XDF. Importe os dados no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando as funções no pacote **RevoScaleR**.
+ O treinamento e a pontuação do modelo são executados usando o contexto de computação [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. 
+ Use as funções **RevoScaleR** para criar tabelas [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para salvar os resultados da pontuação.
+ Crie plotagens no servidor e no contexto de computação local.
+ Treine um modelo sobre dados no banco de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], executando o R na instância [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].
+ Extraia um subconjunto de dados e salve-os como um arquivo XDF para usar novamente em análises em sua estação de trabalho local.
+ Obtenha novos dados para pontuação, abrindo uma conexão ODBC com o banco de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. A pontuação é feita na estação de trabalho local.
+ Crie uma função do R personalizada e execute-a no contexto de computação do servidor para executar uma simulação.

## <a name="next-steps"></a>Próximas etapas

> [!div class="nextstepaction"]
> [Tutorial 1: Criar banco de dados e permissões](deepdive-work-with-sql-server-data-using-r.md)