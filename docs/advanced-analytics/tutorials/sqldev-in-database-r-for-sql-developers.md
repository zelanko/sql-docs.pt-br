---
title: Tutorial para análise no banco de dados usando R e SQL Server Machine Learning | Microsoft Docs
description: Tutorial que mostra como incorporar o R no SQL Server procedimentos armazenados e funções T-SQL
ms.prod: sql
ms.technology: machine-learning
ms.date: 07/15/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 8c7296c46bb6312d66c07c0bb63c9e97c37ec1db
ms.sourcegitcommit: c8f7e9f05043ac10af8a742153e81ab81aa6a3c3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/17/2018
ms.locfileid: "39082428"
---
# <a name="tutorial-learn-in-database-analytics-using-r-in-sql-server"></a>Tutorial: Aprenda a análise de no banco de dados usando o R no SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Neste tutorial para programadores SQL, você obtém experiência prática com a linguagem R para criar e implantar uma solução de machine learning, encapsulando o código R em procedimentos armazenados.

Este tutorial usa um conhecido conjunto de dados público, com base em corridas de táxis de Nova York. Para fazer o código de exemplo executado mais rápido, criamos uma amostragem representativa de 1% dos dados. Você usará esses dados para criar um modelo de classificação binária que prevê se uma corrida específica é provável que receber uma gorjeta ou não, com base em colunas, como a hora do dia, distância e local de embarque.

> [!NOTE]
> 
> Da mesma solução está disponível em Python. SQL Server 2017 é necessária. Consulte [no banco de dados do analytics para desenvolvedores do Python](../tutorials/sqldev-in-database-python-for-sql-developers.md)

## <a name="overview"></a>Visão geral

O processo de criação de uma solução de ponta a ponta normalmente consiste na obtenção e limpeza de dados, exploração de dados e engenharia de recursos, treinamento do modelo e ajuste e, por fim, a implantação do modelo na produção. Desenvolvimento e teste do código real é mais bem executados usando um ambiente de desenvolvimento dedicado. Para R, que pode significar RStudio ou [!INCLUDE[rtvs-short](../../includes/rtvs-short-md.md)].

No entanto, depois que a solução for criada, você poderá implantá-la com facilidade no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando os procedimentos armazenados do [!INCLUDE[tsql](../../includes/tsql-md.md)] no ambiente conhecido do [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)].

- [Lição 1: Baixar os dados de exemplo e scripts](../tutorials/sqldev-download-the-sample-data.md)

- [Lição 2: Configurar o ambiente de tutorial](../r/sqldev-import-data-to-sql-server-using-powershell.md)

- [Lição 3: Explorar e visualizar a forma de dados e a distribuição chamando funções de R em procedimentos armazenados](../tutorials/sqldev-explore-and-visualize-the-data.md)

- [Lição 4: Criar recursos de dados usando o R em funções T-SQL](../tutorials/sqldev-create-data-features-using-t-sql.md)
  
- [Lição 5: Treinar e salvar um modelo R usando procedimentos armazenados e funções](../r/sqldev-train-and-save-a-model-using-t-sql.md)
  
- [Lição 6: Código de encapsulamento de R em um procedimento armazenado para operacionalização](../tutorials/sqldev-operationalize-the-model.md). 
  Depois que o modelo for salvo no banco de dados, chame o modelo de previsão no [!INCLUDE[tsql](../../includes/tsql-md.md)] usando procedimentos armazenados.

## <a name="prerequisites"></a>Prerequisites

Este tutorial presume familiaridade com operações de banco de dados básico, como criação de tabelas e bancos de dados, importação de dados e escrever consultas SQL. Ele pressupõe que conheça o R. Assim, todo o código R é fornecido. Um programador experiente do SQL pode usar um script PowerShell fornecido, os dados de exemplo no GitHub, e [!INCLUDE[tsql](../../includes/tsql-md.md)] em [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] para concluir este exemplo. 

Antes de iniciar o tutorial:

- Verifique se você tiver uma instância configurada do [SQL Server 2016 R Services](../install/sql-r-services-windows-install.md#verify-installation) ou [serviços de aprendizado de máquina do SQL Server 2017 com R habilitado](../install/sql-machine-learning-services-windows-install.md#verify-installation). Além disso, [confirmar que você tem as bibliotecas do R](../r/determine-which-packages-are-installed-on-sql-server.md#get-the-r-library-location).
- O logon que você pode usar para este tutorial deve ter permissões para criar bancos de dados e outros objetos, carregar dados, selecionam dados e executar procedimentos armazenados.

> [!NOTE]
> É recomendável que você faça **não** usar [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] para gravar ou testar o código R. Se o código que você inserir em um procedimento armazenado apresentar problemas, as informações que são retornadas do procedimento armazenado serão geralmente serão inadequadas para entender a causa do erro.
> 
> Para depuração, recomendamos que você use uma ferramenta como [!INCLUDE[rtvs-short](../../includes/rtvs-short-md.md)], ou RStudio. Os scripts do R fornecidos neste tutorial já foram desenvolvidos e depurados com ferramentas tradicionais do R.

## <a name="next-steps"></a>Próximas etapas

> [!div class="nextstepaction"]
> [Lição 1: Baixar os dados de exemplo](../tutorials/sqldev-download-the-sample-data.md)