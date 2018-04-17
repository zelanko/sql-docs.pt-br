---
title: Pré-requisitos para o passo a passo do ciência de dados do SQL Server e R | Microsoft Docs
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: c97f45375464561e8080e5de24201c80fa213c7e
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="prerequisites-for-the-data-science-walkthrough-for-sql-server-and-r"></a>Pré-requisitos para o passo a passo do ciência de dados do SQL Server e R
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

É recomendável que você faça esta explicação passo a passo em um laptop ou outro computador que tenha as bibliotecas do Microsoft R instaladas. Você deve ser capaz de se conectar, na mesma rede, como um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] computador com serviços de aprendizado de máquina e a linguagem R habilitado.

Você pode executar o passo a passo em um computador que tem ambos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e um ambiente de desenvolvimento de R, mas nós não recomendamos essa configuração para um ambiente de produção.

## <a name="install-machine-learning-for-sql-server"></a>Instalar o aprendizado de máquina do SQL Server

Você deve ter acesso a uma instância do SQL Server com suporte para R instalado. Este passo a passo tenha sido originalmente desenvolvida para o servidor SQL 2016 e testada em 2017, portanto você deve ser capaz de usar qualquer uma das seguintes versões do SQL Server. (Há algumas pequenas diferenças nas funções de RevoScaleR entre as versões.)

+ Serviços (no banco de dados) de aprendizado de máquina do SQL Server de 2017
+ SQL Server 2016 R Services

Para obter mais informações, consulte [instalar serviços aprendizado de máquina do SQL Server de 2017](../install/sql-machine-learning-services-windows-install.md) ou [instalar o SQL Server 2016 R Services](../install/sql-r-services-windows-install.md).

> [!IMPORTANT]
> Versões do SQL Server anterior de 2016 não dá suporte a integração com R. No entanto, você pode usar mais antigos bancos de dados SQL como uma fonte de dados ODBC.

## <a name="install-an-r-development-environment"></a>Instalar um ambiente de desenvolvimento R

Para este passo a passo, é recomendável que você use um ambiente de desenvolvimento de R. Aqui estão algumas sugestões:

- **Ferramentas de R para Visual Studio** (RTVS) é um plug-in que fornece o Intellisense, depuração e suporte para o Microsoft R. você pode usá-lo com R Server e serviços de aprendizado de máquina do SQL Server. Para baixar, consulte [R Tools para Visual Studio](https://www.visualstudio.com/vs/rtvs/).

- **O cliente do Microsoft R** é uma ferramenta de desenvolvimento leve que dá suporte ao desenvolvimento em R usando o pacote RevoScaleR. Para fazer isso, veja [Começar a usar o cliente do Microsoft R](https://docs.microsoft.com/machine-learning-server/r-client/what-is-microsoft-r-client).

- O**RStudio** é um dos ambientes mais populares para desenvolvimento do R. Para obter mais informações, consulte [ https://www.rstudio.com/products/RStudio/ ](https://www.rstudio.com/products/RStudio/).

    Você não pode concluir este tutorial usando uma instalação genérica de RStudio ou outro ambiente. Você também deve instalar os pacotes de R e bibliotecas de conectividade para o Microsoft R Open. Para obter mais informações, consulte [Configurar um cliente de ciência de dados](../r/set-up-a-data-science-client.md).

- Ferramentas básicas de R (R.exe, RTerm.exe, RScripts.exe) também são instaladas por padrão quando você instala o R no SQL Server ou cliente de R. Se você não quiser instalar um IDE, você pode usar essas ferramentas.

## <a name="get-permissions-on-the-sql-server-instance-and-database"></a>Obter as permissões na instância do SQL Server e banco de dados

Para se conectar a uma instância de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para executar scripts e carregar dados, você deve ter um logon válido no servidor de banco de dados.  Você pode usar um logon SQL ou a autenticação integrada do Windows. Peça ao administrador de banco de dados para configurar as seguintes permissões para a conta no banco de dados em que você usar r:

- Criar banco de dados, tabelas, funções e procedimentos armazenados
- Gravar dados em tabelas
- Capacidade de executar script R (`GRANT EXECUTE ANY EXTERNAL SCRIPT to <user>`)

Para este passo a passo, usamos o logon do SQL **RTestUser**. Geralmente, é recomendável que você usar a autenticação integrada do Windows, mas usar o logon do SQL é mais simples para alguns fins de demonstração.

## <a name="change-list"></a>Lista de alterações

+ Este exemplo foi originalmente desenvolvido usando o SQL Server 2016 R Services. No entanto, alterações significativas foram introduzidas nos componentes do Microsoft R para 2016 SP1. Especificamente, o _varsToDrop_ e _varsToKeep_ parâmetros foram não tem mais suporte para fontes de dados do SQL Server. Therefre, se você baixou uma versão do tutorial antes do SP1, ele deixará de funcionar com compilações de pós-SP1.

+ A versão atual do exemplo foi testada usando uma compilação de versão de pré-lançamento do SQL Server de 2017 Machine Learning Services (RC1 e RC2). Em geral, quase todas as etapas devem ser executados sem modificação entre 2016 SP1 e 2017.

## <a name="next-lesson"></a>Próxima lição

[Preparar os dados usando o PowerShell](/walkthrough-prepare-the-data.md)
