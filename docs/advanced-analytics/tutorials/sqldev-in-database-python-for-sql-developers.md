---
title: Tutorial para análise do Python no banco de dados para desenvolvedores do SQL
description: Saiba como inserir código Python em SQL Server procedimentos armazenados e funções T-SQL.
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/29/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 9d3905ef9434bf4d3f887130c6f67ad68c6a6e36
ms.sourcegitcommit: 321497065ecd7ecde9bff378464db8da426e9e14
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/01/2019
ms.locfileid: "68714761"
---
# <a name="tutorial-python-data-analytics-for-sql-developers"></a>Tutorial: Análise de dados do Python para desenvolvedores do SQL
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Neste tutorial para programadores do SQL, saiba mais sobre a integração do Python criando e implantando uma solução de aprendizado de máquina baseada em Python usando um banco de dados [NYCTaxi_sample](demo-data-nyctaxi-in-sql.md) em SQL Server. Você usará o T-SQL, o SQL Server Management Studio e uma instância do mecanismo de banco de dados com suporte ao idioma [serviços de Machine Learning](../install/sql-machine-learning-services-windows-install.md) e Python.

Este tutorial apresenta as funções do Python usadas em um fluxo de trabalho de modelagem de dados. As etapas incluem exploração de dados, criação e treinamento de um modelo de classificação binária e implantação de modelo. Você usará dados de exemplo do táxi da cidade de Nova York e da Comissão limosine, e o modelo que você criará prevê se uma corrida provavelmente resultará em uma dica com base na hora do dia, na distância viajado e na escolha do local. 

Todo o código Python usado neste tutorial é encapsulado em procedimentos armazenados que você cria e executa no Management Studio.

> [!NOTE]
> Este tutorial está disponível em R e Python. Para a versão do R, consulte [análise no banco de dados para desenvolvedores de R](sqldev-in-database-r-for-sql-developers.md).

## <a name="overview"></a>Visão geral

O processo de criação de uma solução de aprendizado de máquina é complexo que pode envolver várias ferramentas e a coordenação de especialistas do assunto em várias fases:

+ obtendo e limpando dados
+ explorando os dados e criando recursos úteis para modelagem
+ treinando e ajustando o modelo
+ implantação para produção

O desenvolvimento e o teste do código real são mais bem executados usando um ambiente de desenvolvimento dedicado. No entanto, depois que o script for totalmente testado, você poderá implantá [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] - [!INCLUDE[tsql](../../includes/tsql-md.md)] lo facilmente no usando procedimentos armazenados no [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]ambiente familiar do. O encapsulamento de código externo em procedimentos armazenados é o principal mecanismo de operacionalização do código no SQL Server.

Seja você um programador de SQL novo no Python ou um desenvolvedor Python novo no SQL, este tutorial de várias partes apresenta um fluxo de trabalho típico para realizar análises no banco de dados com Python e SQL Server. 

+ [Lição 1: Explorar e visualizar os dados usando o Python](sqldev-py3-explore-and-visualize-the-data.md)

+ [Lição 2: Criar recursos de dados usando funções SQL personalizadas](sqldev-py4-create-data-features-using-t-sql.md)

+ [Lição 3: Treinar e salvar um modelo Python usando o T-SQL](sqldev-py5-train-and-save-a-model-using-t-sql.md)

+ [Lição 4: Prever resultados potenciais usando um modelo Python em um procedimento armazenado](sqldev-py6-operationalize-the-model.md)

Depois que o modelo tiver sido salvo no banco de dados, você poderá chamar o modelo para previsões [!INCLUDE[tsql](../../includes/tsql-md.md)] do usando procedimentos armazenados.

## <a name="prerequisites"></a>Pré-requisitos

+ [SQL Server Serviços de Machine Learning com Python](../install/sql-machine-learning-services-windows-install.md#verify-installation)

+ [Permissões](../security/user-permission.md)

+ [Banco de dados de demonstração do NYC táxi](demo-data-nyctaxi-in-sql.md)

Todas as tarefas podem ser feitas [!INCLUDE[tsql](../../includes/tsql-md.md)] usando procedimentos armazenados [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]no.

Este tutorial pressupõe familiaridade com operações básicas do banco de dados, como criar bancos de dados e tabelas, importar e escrever consultas SQL. Ele não pressupõe que você conheça o Python. Como tal, todo o código Python é fornecido. 

## <a name="next-steps"></a>Próximas etapas

> [!div class="nextstepaction"]
> [Explorar e visualizar os dados usando o Python](sqldev-py3-explore-and-visualize-the-data.md)
