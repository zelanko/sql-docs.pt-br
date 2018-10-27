---
title: No banco de dados análise do Python para desenvolvedores do SQL | Microsoft Docs
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 26703f73312b5531490afc7d01319d4ac290bebe
ms.sourcegitcommit: 70e47a008b713ea30182aa22b575b5484375b041
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49806756"
---
# <a name="in-database-python-analytics-for-sql-developers"></a>Análise de Python no banco de dados para desenvolvedores do SQL
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

O objetivo deste passo a passo é fornecer aos programadores SQL experiência prática na criação de uma solução de machine learning usando o Python é executado no SQL Server. Neste passo a passo, você aprenderá como adicionar código do Python aos procedimentos armazenados e executar procedimentos armazenados para criar e a previsão a partir de modelos.

> [!NOTE]
> Prefere R? Ver [este tutorial](sqldev-in-database-r-for-sql-developers.md), que fornece uma solução semelhante, mas usa o R e pode ser executado no SQL Server 2016 ou SQL Server 2017.

## <a name="overview"></a>Visão geral

O processo de criação de uma solução de aprendizado de máquina é um complexo que pode envolver várias ferramentas e a coordenação de especialistas no assunto em várias fases:

+ obtenção e limpeza de dados
+ explorar os dados e criação de recursos úteis para a modelagem
+ treinamento e o modelo de ajuste
+ implantação na produção

**O foco deste passo a passo é criar e implantar uma solução usando o SQL Server.**

Os dados estão no conjunto de dados de táxi de NYC bem conhecido. Para tornar este passo a passo rápido e fácil, os dados são amostrados. Você criará um modelo de classificação binária que prevê se uma corrida específica é provável que receber uma gorjeta ou não, com base em colunas, como a hora do dia, distância e local de embarque.

Todas as tarefas podem ser feitas usando [!INCLUDE[tsql](../../includes/tsql-md.md)] procedimentos armazenados no ambiente familiar do [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]


- [Explorar e visualizar os dados usando o Python](sqldev-py3-explore-and-visualize-the-data.md)

    Executar a exploração de dados básicos e visualização, pelo Python chamada de [!INCLUDE[tsql](../../includes/tsql-md.md)] procedimentos armazenados.

- [Criar recursos de dados usando o Python no T-SQL](sqldev-py5-train-and-save-a-model-using-t-sql.md)

    Crie novos recursos de dados usando funções personalizadas do SQL.
  
- [Treinar e salvar um modelo de Python usando o T-SQL](sqldev-py5-train-and-save-a-model-using-t-sql.md)

    Criar e salvar o modelo de aprendizado de máquina usando o Python em procedimentos armazenados.
  
    Este passo a passo demonstra como executar uma tarefa de classificação binária. Você também pode usar os dados para criar modelos de regressão ou classificação multiclasse.

  
-  [ Operacionalizar o modelo de Python](sqldev-py6-operationalize-the-model.md)

    Depois que o modelo foi salvo no banco de dados, chame o modelo de previsão usando [!INCLUDE[tsql](../../includes/tsql-md.md)].

## <a name="requirements"></a>Requisitos

### <a name="prerequisites"></a>Prerequisites

+ Instale uma instância do SQL Server 2017 com serviços de Machine Learning e o Python habilitado. Para obter mais informações, consulte [instalar o SQL Server 2017 serviços Machine Learning (no banco de dados)](../install/sql-machine-learning-services-windows-install.md).
+ O logon usado para este passo a passo deve ter permissões para criar bancos de dados e outros objetos, carregar dados, selecionar dados e executar procedimentos armazenados.

### <a name="experience-level"></a>Nível de experiência

Você deve estar familiarizado com as operações de banco de dados fundamentais, como criação de bancos de dados e tabelas, importar dados em tabelas e criar consultas SQL.

Um programador experiente do SQL deve conseguir concluir esse passo a passo usando o [!INCLUDE[tsql](../../includes/tsql-md.md)] no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou executando os scripts do PowerShell fornecidos.

Python: Conhecimento básico é útil, mas não é necessário. Todo o código Python é fornecido.

Algum conhecimento do PowerShell é útil.

### <a name="tools"></a>Ferramentas

Para este tutorial, vamos supor que você atingiu a fase de implantação. Você recebeu os dados limpos, código T-SQL para o recurso de engenharia e o trabalho de código Python completo. Portanto, você pode concluir este tutorial usando o SQL Server Management Studio ou qualquer outra ferramenta que oferece suporte à execução de instruções SQL.

+ [Visão geral das ferramentas do SQL Server](https://docs.microsoft.com/sql/tools/overview-sql-tools) 

Se você quiser desenvolver e testar seu próprio código Python ou depura uma solução de Python, recomendamos o uso de um ambiente de desenvolvimento dedicado:

+ **Visual Studio 2017** dá suporte a ambos os R e [Python](https://blogs.msdn.microsoft.com/visualstudio/2017/05/12/a-lap-around-python-in-visual-studio-2017/). É recomendável o [carga de trabalho de ciência de dados](https://blogs.msdn.microsoft.com/visualstudio/2016/11/18/data-science-workloads-in-visual-studio-2017-rc/), que também oferece suporte a R e F #.
+ Se você tiver uma versão anterior do Visual Studio, [extensões do Python para Visual Studio](https://docs.microsoft.com/visualstudio/python/python-in-visual-studio) torna mais fácil de gerenciar vários ambientes do Python.
+ PyCharm é um IDE popular entre os desenvolvedores de Python.

    > [!NOTE]
    > Em geral, evite escrever ou teste de novo código do Python no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Se o código que você inserir em um procedimento armazenado apresentar problemas, as informações que são retornadas do procedimento armazenado serão geralmente serão inadequadas para entender a causa do erro.

Use os seguintes recursos para ajudá-lo a planejar e executar uma projeto de aprendizado de máquina com êxito:

+ [Processo de ciência de dados de equipe](https://docs.microsoft.com/azure/machine-learning/team-data-science-process/overview)

### <a name="estimated-time-required"></a>Tempo estimado necessário

|Etapa| Tempo (horas)|
|----|----|
|Baixar os dados de exemplo| 0:15|
|Importar dados para o SQL Server usando o PowerShell|0:15|
|Explorar e visualizar os dados|0:20|
|Criar recursos de dados usando o T-SQL|0:30|
|Treinar e salvar um modelo usando o T-SQL|0:15|
|Colocar o modelo em operação|0:40|

## <a name="get-started"></a>Introdução

  [Etapa 1: Baixar os dados de exemplo](demo-data-nyctaxi-in-sql.md)
