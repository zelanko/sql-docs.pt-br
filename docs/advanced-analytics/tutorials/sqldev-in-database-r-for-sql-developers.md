---
title: Tutorial para análise no banco de dados usando R e SQL Server Machine Learning | Microsoft Docs
description: Saiba como incorporar o código de idioma em procedimentos armazenados do SQL Server e funções T-SQL de programação R.
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/29/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 80c4d39e87984b022340079be4d944ed6ad963e3
ms.sourcegitcommit: af1d9fc4a50baf3df60488b4c630ce68f7e75ed1
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/06/2018
ms.locfileid: "51030643"
---
# <a name="tutorial-in-database-r-analytics-for-sql-developers"></a>Tutorial: Análise de no banco de dados R para desenvolvedores do SQL
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Neste tutorial para programadores SQL, saiba mais sobre a integração do R criando e implantando uma solução usando de aprendizado de máquina baseada em R uma [NYCTaxi_sample](demo-data-nyctaxi-in-sql.md) banco de dados no SQL Server. 

Este tutorial apresenta as funções de R usadas em um fluxo de trabalho de modelagem de dados. As etapas incluem a exploração de dados, criar e treinar um modelo de classificação binária e a implantação de modelo. Você usará os dados de exemplo do táxi de Nova York e Limosine comissão e o modelo que você irá criar prevê se uma corrida é provavelmente resultará em uma dica com base na hora do dia, distância percorreu e coleta local. Todo o código R usado neste tutorial é encapsulado em procedimentos armazenados que você criar e executar no Management Studio.


> [!NOTE]
> 
> Este tutorial está disponível em R e Python. Para a versão do Python, consulte [no banco de dados do analytics para desenvolvedores de Python](../tutorials/sqldev-in-database-python-for-sql-developers.md).

## <a name="overview"></a>Visão geral

O processo de criação de uma solução de aprendizado de máquina é um complexo que pode envolver várias ferramentas e a coordenação de especialistas no assunto em várias fases:

+ obtenção e limpeza de dados
+ explorar os dados e criação de recursos úteis para a modelagem
+ treinamento e o modelo de ajuste
+ implantação na produção

Desenvolvimento e teste do código real é mais bem executados usando um ambiente de desenvolvimento dedicado. No entanto, depois que o script é totalmente testado, você pode facilmente implantá-lo para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando [!INCLUDE[tsql](../../includes/tsql-md.md)] procedimentos armazenados no ambiente familiar do [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)].

Se você for um programador SQL é novo no R ou é um novidade no SQL, este tutorial com várias partes de desenvolvedor R introduz um fluxo de trabalho típico para realizar a análise no banco de dados com R e SQL Server. 

- [Lição 1: Explorar e visualizar a forma de dados e a distribuição chamando funções de R em procedimentos armazenados](../tutorials/sqldev-explore-and-visualize-the-data.md)

- [Lição 2: Criar recursos de dados usando o R em funções T-SQL](sqldev-create-data-features-using-t-sql.md)
  
- [Lição 3: Treinar e salvar um modelo R usando procedimentos armazenados e funções](sqldev-train-and-save-a-model-using-t-sql.md)
  
- [Lição 4: Prever resultados possíveis, usando um modelo do R em um procedimento armazenado](../tutorials/sqldev-operationalize-the-model.md)

Depois que o modelo foi salvo no banco de dados, chame o modelo de previsões de [!INCLUDE[tsql](../../includes/tsql-md.md)] usando procedimentos armazenados.

## <a name="prerequisites"></a>Prerequisites

Todas as tarefas podem ser feitas usando [!INCLUDE[tsql](../../includes/tsql-md.md)] procedimentos armazenados no [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)].

Este tutorial presume familiaridade com operações de banco de dados básico, como criação de tabelas e bancos de dados, importação de dados e escrever consultas SQL. Ele pressupõe que conheça o R. Assim, todo o código R é fornecido. 

+ [SQL Server 2016 R Services](../install/sql-r-services-windows-install.md#verify-installation) ou [serviços SQL Server 2017 Machine Learning com R habilitado](../install/sql-machine-learning-services-windows-install.md#verify-installation)

+ [Bibliotecas do R](../r/determine-which-packages-are-installed-on-sql-server.md#get-the-r-library-location)

+ [Permissões](../security/user-permission.md)

+ [Banco de dados de demonstração de táxi de NYC](demo-data-nyctaxi-in-sql.md)


## <a name="next-steps"></a>Próximas etapas

> [!div class="nextstepaction"]
> [Configurar o banco de dados de táxi de NYC](demo-data-nyctaxi-in-sql.md)