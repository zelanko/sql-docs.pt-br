---
title: Tutorial para análise no banco de dados usando o R
description: Saiba como inserir código de linguagem de programação R em SQL Server procedimentos armazenados e funções T-SQL.
ms.prod: sql
ms.technology: machine-learning
ms.date: 06/13/2019
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.openlocfilehash: 1257cc3f3d0b3ed07bc879f5bc3337d62bc1b3a0
ms.sourcegitcommit: 9062c5e97c4e4af0bbe5be6637cc3872cd1b2320
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/24/2019
ms.locfileid: "68470580"
---
# <a name="tutorial-r-data-analytics-for-sql-developers"></a>Tutorial: Análise de dados do R para desenvolvedores do SQL
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Neste tutorial para programadores do SQL, saiba mais sobre a integração do R criando e implantando uma solução de aprendizado de máquina baseada em R usando um banco de dados [NYCTaxi_sample](demo-data-nyctaxi-in-sql.md) no SQL Server. Você usará o T-SQL, SQL Server Management Studio e uma instância do mecanismo de banco de dados com [Serviços de Machine Learning] ([serviços de Machine Learning](../install/sql-machine-learning-services-windows-install.md) e o suporte à linguagem R

Este tutorial apresenta as funções do R usadas em um fluxo de trabalho de modelagem de dados. As etapas incluem exploração de dados, criação e treinamento de um modelo de classificação binária e implantação de modelo. O modelo que você criará prevê se uma corrida provavelmente resultará em uma dica com base na hora do dia, distância viajada e local de seleção. 

Todo o código R usado neste tutorial é encapsulado em procedimentos armazenados que você cria e executa no Management Studio.

## <a name="background-for-sql-developers"></a>Plano de fundo para desenvolvedores do SQL

O processo de criação de uma solução de aprendizado de máquina é complexo que pode envolver várias ferramentas e a coordenação de especialistas do assunto em várias fases:

+ obtendo e limpando dados
+ explorando os dados e criando recursos úteis para modelagem
+ treinando e ajustando o modelo
+ implantação para produção

O desenvolvimento e o teste do código real são mais bem executados usando um ambiente de desenvolvimento de R dedicado. No entanto, depois que o script for totalmente testado, você poderá implantá [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] - [!INCLUDE[tsql](../../includes/tsql-md.md)] lo facilmente no usando procedimentos armazenados no [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]ambiente familiar do.

A finalidade deste tutorial de várias partes é uma introdução a um fluxo de trabalho típico para migrar "código R concluído" para SQL Server. 

- [Lição 1: Explorar e visualizar a forma e a distribuição de dados chamando funções do R em procedimentos armazenados](../tutorials/sqldev-explore-and-visualize-the-data.md)

- [Lição 2: Criar recursos de dados usando o R em funções T-SQL](sqldev-create-data-features-using-t-sql.md)
  
- [Lição 3: Treinar e salvar um modelo de R usando funções e procedimentos armazenados](sqldev-train-and-save-a-model-using-t-sql.md)
  
- [Lição 4: Prever resultados potenciais usando um modelo de R em um procedimento armazenado](../tutorials/sqldev-operationalize-the-model.md)

Depois que o modelo tiver sido salvo no banco de dados, chame o modelo para previsões [!INCLUDE[tsql](../../includes/tsql-md.md)] do usando procedimentos armazenados.

## <a name="prerequisites"></a>Pré-requisitos

Todas as tarefas podem ser feitas [!INCLUDE[tsql](../../includes/tsql-md.md)] usando procedimentos armazenados [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]no.

Este tutorial pressupõe familiaridade com operações básicas do banco de dados, como criar bancos de dados e tabelas, importar e escrever consultas SQL. Ele não pressupõe que você conhece o R. Como tal, todo o código R é fornecido. 

+ [SQL Server 2016 R Services](../install/sql-r-services-windows-install.md#verify-installation) ou [SQL Server 2017 serviços de Machine Learning com R habilitado](../install/sql-machine-learning-services-windows-install.md#verify-installation)

+ [Bibliotecas de R](../package-management/installed-package-information.md)

+ [Permissões](../security/user-permission.md)

+ [Banco de dados de demonstração do NYC táxi](demo-data-nyctaxi-in-sql.md)


## <a name="next-steps"></a>Próximas etapas

> [!div class="nextstepaction"]
> [Explorar e Visualizar dados usando as funções do R em procedimentos armazenados](../tutorials/sqldev-explore-and-visualize-the-data.md)
