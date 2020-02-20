---
title: 'Tutorial de R + T-SQL: Desenvolver um modelo'
description: Saiba como inserir código de programação R em procedimentos armazenados do SQL Server e funções do T-SQL.
ms.prod: sql
ms.technology: machine-learning
ms.date: 06/13/2019
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 9669b2c38d2e8b571ef7e519100b13cf5a63a10d
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/31/2020
ms.locfileid: "74479408"
---
# <a name="tutorial-r-data-analytics-for-sql-developers"></a>Tutorial: Análise de dados do R para desenvolvedores de SQL
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Neste tutorial para programadores de SQL, saiba mais sobre a integração do R ao criar e implantar uma solução de aprendizado de máquina baseada em R usando um banco de dados [NYCTaxi_sample](demo-data-nyctaxi-in-sql.md) no SQL Server. Você usará o T-SQL, o SQL Server Management Studio e uma instância do mecanismo de banco de dados com os [Serviços de Machine Learning](../install/sql-machine-learning-services-windows-install.md) e o suporte à linguagem R

Este tutorial apresenta as funções do R usadas em um fluxo de trabalho de modelagem de dados. As etapas incluem exploração de dados, criação e treinamento de um modelo de classificação binária e implantação de modelo. O modelo que você criará prevê se uma corrida provavelmente resultará em uma gorjeta com base na hora do dia, na distância percorrida e na localização de embarque. 

Todo o código R usado neste tutorial é encapsulado em procedimentos armazenados que você cria e executa no Management Studio.

## <a name="background-for-sql-developers"></a>Contexto para desenvolvedores de SQL

O processo de criação de uma solução de aprendizado de máquina é complexo, podendo envolver várias ferramentas e a coordenação de especialistas do assunto em várias fases:

+ obtenção e limpeza de dados
+ exploração de dados e criação de recursos úteis para modelagem
+ treinamento e ajuste do modelo
+ implantação para produção

O desenvolvimento e teste do código do R real serão mais bem executados usando um ambiente de desenvolvimento R dedicado. No entanto, depois que o script estiver totalmente testado, você poderá implantá-lo com facilidade no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando os procedimentos armazenados do [!INCLUDE[tsql](../../includes/tsql-md.md)] no ambiente conhecido do [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)].

A finalidade deste tutorial de várias partes é uma introdução a um fluxo de trabalho típico para migrar "código R pronto" para o SQL Server. 

- [Lição 1: Explorar e visualizar a forma e a distribuição de dados chamando funções do R em procedimentos armazenados](../tutorials/sqldev-explore-and-visualize-the-data.md)

- [Lição 2: Criar recursos de dados usando o R em funções do T-SQL](sqldev-create-data-features-using-t-sql.md)
  
- [Lição 3: Treinar e salvar um modelo do R usando funções e procedimentos armazenados](sqldev-train-and-save-a-model-using-t-sql.md)
  
- [Lição 4: Prever os resultados potenciais usando um modelo do R em um procedimento armazenado](../tutorials/sqldev-operationalize-the-model.md)

Depois que o modelo for salvo no banco de dados, use procedimentos armazenados a fim de chamar o modelo para fazer previsões por meio do [!INCLUDE[tsql](../../includes/tsql-md.md)].

## <a name="prerequisites"></a>Prerequisites

Todas as tarefas podem ser feitas usando procedimentos armazenados do [!INCLUDE[tsql](../../includes/tsql-md.md)] no [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)].

Este tutorial pressupõe que você tem familiaridade com as operações de banco de dados, tais como criar bancos de dados e tabelas, importar dados e escrever consultas SQL. Ele não pressupõe que você conhece o R. Assim, todo o código R é fornecido. 

+ [SQL Server 2016 R Services](../install/sql-r-services-windows-install.md#verify-installation) ou [Serviços de Machine Learning do SQL Server com o R habilitado](../install/sql-machine-learning-services-windows-install.md#verify-installation)

+ [Bibliotecas do R](../package-management/r-package-information.md)

+ [Permissões](../security/user-permission.md)

+ [Banco de dados de demonstração de Táxi de Nova York](demo-data-nyctaxi-in-sql.md)


## <a name="next-steps"></a>Próximas etapas

> [!div class="nextstepaction"]
> [Explorar e visualizar dados usando as funções do R em procedimentos armazenados](../tutorials/sqldev-explore-and-visualize-the-data.md)
