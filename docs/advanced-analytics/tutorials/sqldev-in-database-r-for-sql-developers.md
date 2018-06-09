---
title: Tutorial de análise de R inserido para desenvolvedores de aprendizado de máquina do SQL Server | Microsoft Docs
description: Tutorial mostra como inserir R no SQL Server procedimentos armazenados e funções T-SQL
ms.prod: sql
ms.technology: machine-learning
ms.date: 06/07/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 3d2b77d73bb1b8f5d4c507b884d0a09f4647012b
ms.sourcegitcommit: b52b5d972b1a180e575dccfc4abce49af1a6b230
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/08/2018
ms.locfileid: "35250019"
---
# <a name="tutorial-embedded-r-in-stored-procedures-and-t-sql-functions"></a>Tutorial: Inserida R em procedimentos armazenados e funções de T-SQL
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

O objetivo deste tutorial é fornecer os programadores SQL com experiência prática na criação de uma solução no SQL Server de aprendizado de máquina. Neste tutorial, você aprenderá como incorporar R em um aplicativo ou a solução de BI ao encapsular o código R em procedimentos armazenados.

> [!NOTE]
> 
> A mesma solução está disponível em Python. 2017 do SQL Server é necessária. Consulte [no banco de dados analytics para desenvolvedores Python](../tutorials/sqldev-in-database-python-for-sql-developers.md)

## <a name="overview"></a>Visão geral

O processo de criação de uma solução de ponta a ponta normalmente consiste na obtenção e limpeza de dados, exploração de dados e engenharia de recursos, treinamento do modelo e ajuste e, por fim, na implantação do modelo em produção. Desenvolvimento e teste do código real é mais bem executada usando um ambiente de desenvolvimento dedicado. Para R, isso pode significar que RStudio ou [!INCLUDE[rtvs-short](../../includes/rtvs-short-md.md)].

No entanto, depois que a solução for criada, você poderá implantá-la com facilidade no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando os procedimentos armazenados do [!INCLUDE[tsql](../../includes/tsql-md.md)] no ambiente conhecido do [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)].

Neste tutorial, vamos supor que você tenha recebido todo o código de R necessário para a solução e foco sobre como compilar e implantar a solução usando o SQL Server.

- [Lição 1: Baixar os dados de exemplo e scripts](../tutorials/sqldev-download-the-sample-data.md)

- [Lição 2: Configurar o ambiente de tutorial](../r/sqldev-import-data-to-sql-server-using-powershell.md)

- [Lição 3: Explorar e visualizar a forma de dados e a distribuição chamando funções de R em procedimentos armazenados](../tutorials/sqldev-explore-and-visualize-the-data.md)

- [Lição 4: Criar recursos de dados usando R nas funções T-SQL](../tutorials/sqldev-create-data-features-using-t-sql.md)
  
- [Lição 5: Treinar e salvar um modelo de R usando procedimentos armazenados e funções](../r/sqldev-train-and-save-a-model-using-t-sql.md)
  
- [Lição 6: Código de Wrap R em um procedimento armazenado para operacionalização](../tutorials/sqldev-operationalize-the-model.md). 
  Depois que o modelo for salvo no banco de dados, chame o modelo de previsão no [!INCLUDE[tsql](../../includes/tsql-md.md)] usando procedimentos armazenados.

## <a name="scenario"></a>Cenário

Este tutorial usa um dataset público bem conhecido, com base em viagens em táxis cidade de Nova York. Para tornar mais rápido executar o código de exemplo, criamos uma amostra representativa de 1% dos dados. Você usará esses dados para criar um modelo de classificação binária que prevê se uma viagem específica é provável obter uma dica ou não, com base em colunas, como a hora do dia, distância e local de coleta.

## <a name="requirements"></a>Requisitos

Este tutorial assume familiaridade com operações de banco de dados básicos, como criação de tabelas e bancos de dados, importando dados e escrever consultas SQL. Não suponha que você sabe que R. Como tal, todo o código R é fornecido. Um programador experiente do SQL pode usar um script do PowerShell fornecido, os dados de exemplo no GitHub, e [!INCLUDE[tsql](../../includes/tsql-md.md)] na [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] para concluir este exemplo. 

Antes de iniciar o tutorial:

- Verifique se você tem uma instância configurada de [SQL Server 2016 R Services](../install/sql-r-services-windows-install.md#verify-installation) ou [serviços de aprendizado de máquina do SQL Server de 2017 com R habilitado](../install/sql-machine-learning-services-windows-install.md#verify-installation). Além disso, [confirmar que você tem as bibliotecas de R](../r/determine-which-packages-are-installed-on-sql-server.md#get-the-r-library-location).
- O logon que você usa para este tutorial deve ter permissões para criar bancos de dados e outros objetos, para carregar dados, selecione os dados e executar procedimentos armazenados.

> [!NOTE]
> Recomendamos que você faça **não** usar [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] para gravar ou testar o código de R. Se o código que você inserir em um procedimento armazenado tiver problemas, as informações que são retornadas pelo procedimento armazenado serão geralmente inadequadas entender a causa do erro.
> 
> Para depuração, é recomendável que você use uma ferramenta como [!INCLUDE[rtvs-short](../../includes/rtvs-short-md.md)], ou RStudio. Os scripts do R fornecidos neste tutorial já foram desenvolvidos e depurados com ferramentas tradicionais do R.

## <a name="next-lesson"></a>Próxima lição

[Lição 1: Baixar os dados de exemplo](../tutorials/sqldev-download-the-sample-data.md)
