---
title: "No banco de dados análise do Python para desenvolvedores em SQL | Microsoft Docs"
ms.custom: 
ms.date: 10/13/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: 
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: tutorial
applies_to: SQL Server 2017
dev_langs:
- Python
- TSQL
ms.assetid: 
caps.latest.revision: "2"
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.openlocfilehash: 6d7e49a6074e342f51595e9b1cdb10227761f670
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/25/2018
---
# <a name="in-database-python-analytics-for-sql-developers"></a>Análise de Python no banco de dados para desenvolvedores em SQL

O objetivo deste passo a passo é fornecer os programadores SQL com experiência prática na criação de uma solução usando Python é executado no SQL Server de aprendizado de máquina. Este passo a passo, você aprenderá como adicionar código Python para procedimentos armazenados e executar procedimentos armazenados para criar e previsão dos modelos.

> [!NOTE]
> Preferir R? Consulte [este tutorial](sqldev-in-database-r-for-sql-developers.md), que fornece uma solução semelhante, mas usa o R e pode ser executado no SQL Server 2016 ou 2017 do SQL Server.

## <a name="overview"></a>Visão geral

O processo de criação de uma solução de aprendizado de máquina é complexo que pode envolver várias ferramentas e a coordenação de especialistas no assunto em várias fases:

+ como obter e limpeza de dados
+ explorar os dados e criação de recursos úteis para a modelagem
+ treinamento e o modelo de ajuste
+ implantação em produção

**É o foco deste passo a passo sobre como compilar e implantar uma solução usando o SQL Server.**

Os dados são do conjunto de dados NYC táxi bem conhecido. Para tornar este passo a passo rápido e fácil, os dados são amostrados. Você criará um modelo de classificação binária que prevê se uma viagem específica é provável obter uma dica ou não, com base em colunas, como a hora do dia, distância e local de coleta.

Todas as tarefas podem ser realizadas usando [!INCLUDE[tsql](../../includes/tsql-md.md)] procedimentos armazenados no ambiente familiar do[!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]

- [Etapa 1: Baixar os dados de exemplo](sqldev-py1-download-the-sample-data.md)

    Baixe o conjunto de dados de exemplo e todos os arquivos de script para um computador local.

- [Etapa 2: Importar dados para o SQL Server usando o PowerShell](sqldev-py2-import-data-to-sql-server-using-powershell.md)

    Execute um script do PowerShell que cria um banco de dados e uma tabela na instância especificada e carrega os dados de exemplo para a tabela.

- [Etapa 3: Explorar e visualizar os dados usando Python](sqldev-py3-explore-and-visualize-the-data.md)

    Executar a exploração de dados básicos e visualização, pela chamada Python de [!INCLUDE[tsql](../../includes/tsql-md.md)] procedimentos armazenados.

- [Etapa 4: Criar recursos de dados usando Python no T-SQL](sqldev-py5-train-and-save-a-model-using-t-sql.md)

    Crie novos recursos de dados usando funções personalizadas do SQL.
  
- [Etapa 5: Treinar e salvar um modelo de Python usando o T-SQL](sqldev-py5-train-and-save-a-model-using-t-sql.md)

    Criar e salvar o modelo de aprendizado de máquina, usando Python em procedimentos armazenados.
  
    Este passo a passo demonstra como executar uma tarefa de classificação binária. Você também pode usar os dados para criar modelos de regressão ou de classificação multiclasse.

  
-  [Etapa 6: Colocar o modelo de Python](sqldev-py6-operationalize-the-model.md)

    Depois que o modelo foi salvo no banco de dados, chame o modelo de previsão usando [!INCLUDE[tsql](../../includes/tsql-md.md)].

## <a name="requirements"></a>Requisitos

### <a name="prerequisites"></a>Prerequisites

+ Instale uma instância do SQL Server 2017 com serviços de aprendizado de máquina e Python habilitado. Para obter mais informações, consulte [configurar serviços de aprendizado de máquina do SQL Server com Python](../python/setup-python-machine-learning-services.md).
+ O logon usado para este passo a passo deve ter permissões para criar bancos de dados e outros objetos, carregar dados, selecionar dados e executar procedimentos armazenados.

### <a name="experience-level"></a>Nível de experiência

Você deve estar familiarizado com operações fundamentais de banco de dados, como criação de tabelas e bancos de dados, importar dados em tabelas e criar consultas SQL.

Um programador experiente do SQL deve conseguir concluir esse passo a passo usando o [!INCLUDE[tsql](../../includes/tsql-md.md)] no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou executando os scripts do PowerShell fornecidos.

Python: Conhecimento básico é útil, mas não é necessária. Todo o código Python é fornecido.

Algum conhecimento do PowerShell é útil.

### <a name="tools"></a>Ferramentas

Para este tutorial, estamos supondo que você atingiu a fase de implantação. Você recebeu limpar dados, conclua código T-SQL para o recurso de engenharia e trabalhando código Python. Portanto, você pode concluir este tutorial usando o SQL Server Management Studio ou qualquer outra ferramenta que oferece suporte à execução de instruções SQL.

+ [Visão geral das ferramentas do SQL Server](https://docs.microsoft.com/sql/tools/overview-sql-tools) 

Se você deseja desenvolver e testar seu próprio código Python ou depura uma solução de Python, é recomendável usar um ambiente de desenvolvimento dedicado:

+ **Visual Studio de 2017** dá suporte a ambos os R e [Python](https://blogs.msdn.microsoft.com/visualstudio/2017/05/12/a-lap-around-python-in-visual-studio-2017/). É recomendável a [cargas de trabalho de ciência de dados](https://blogs.msdn.microsoft.com/visualstudio/2016/11/18/data-science-workloads-in-visual-studio-2017-rc/), que também oferece suporte a R e F #.
+ Se você tiver uma versão anterior do Visual Studio, [extensões do Python para Visual Studio](https://docs.microsoft.com/visualstudio/python/python-in-visual-studio) torna mais fácil gerenciar vários ambientes de Python.
+ PyCharm é um IDE popular entre os desenvolvedores de Python.

    > [!NOTE]
    > Em geral, evite escrever ou testando o novo código Python em [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Se o código que você inserir em um procedimento armazenado tiver problemas, as informações que são retornadas pelo procedimento armazenado serão geralmente inadequadas entender a causa do erro.

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
|Colocar o modelo|0:40|

## <a name="get-started"></a>Introdução

  [Etapa 1: Baixar os dados de exemplo](sqldev-py1-download-the-sample-data.md)
