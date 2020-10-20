---
title: SandDance para Azure Data Studio
description: Saiba como usar uma extensão do Azure Data Studio para criar rapidamente visualizações de seus dados – visualizações que fornecem insights.
ms.prod: azure-data-studio
ms.technology: azure-data-studio
ms.topic: conceptual
author: yualan
ms.author: alayu
ms.reviewer: maghan, sstein
ms.custom: seodec18
ms.date: 07/03/2019
ms.openlocfilehash: 5b00b83fedeb4d0f4673f23a0a2640a3b3a00e3f
ms.sourcegitcommit: 9774e2cb8c07d4f6027fa3a5bb2852e4396b3f68
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/15/2020
ms.locfileid: "92100102"
---
# <a name="sanddance-for-azure-data-studio-preview"></a>SandDance para Azure Data Studio (versão prévia)

O Azure Data Studio agora oferece uma maneira de criar visualizações rápidas para seus dados. Essa extensão é útil quando você está tentando examinar os dados e entender o que está acontecendo. Usamos uma tecnologia chamada SandDance da Microsoft Research, que pode gerar visualizações dos dados no local.

![sanddance-animation](https://user-images.githubusercontent.com/11507384/54236654-52d42800-44d1-11e9-859e-6c5d297a46d2.gif)

Usando exibições fáceis de entender, o SandDance ajuda você a chegar a insights sobre seus dados que, por sua vez, o ajudam a contar histórias com suporte de dados, criar casos com base em evidências, testar hipóteses, aprofundar-se em explicações superficiais, dar suporte a decisões de compra ou relacionar dados a um contexto mais amplo do mundo real.

O SandDance usa visualizações de unidade, que aplicam um mapeamento de um para um entre linhas no banco de dados e marcas na tela.
Transições animadas suaves entre os modos de exibição ajudam a manter o contexto à medida que você interage com seus dados.

## <a name="usage"></a>Uso

### <a name="view-csv-or-tsv-files"></a>Exibir arquivos .csv ou .tsv
Isso inclui arquivos locais ou arquivos no HDFS em seu cluster de Big Data do SQL Server 2019.
 
Começando no menu Arquivo, use Abrir Pasta ou [Ctrl + K Ctrl + O] para abrir o diretório que contém o arquivo .CSV.  Em seguida, no painel do Explorer, clique com o botão direito do mouse no arquivo .csv ou .tsv e escolha *Exibir no SandDance*.

Clique com o botão direito do mouse em um arquivo .csv ou .tsv no HDFS se você estiver conectado a um cluster de Big Data do SQL Server 2019 e escolha *Exibir no SandDance*.

### <a name="view-sql-query-results"></a>Exibir os resultados da consulta SQL

Em uma janela de consulta SQL, execute uma consulta para obter uma grade de resultados. Clique no ícone Visualizador no lado direito do painel Resultados.

## <a name="known-issues"></a>Problemas conhecidos

Atualmente, não limitamos a contagem de linhas que é visualizada. No entanto, o consumo de memória aumenta proporcionalmente ao número de linhas, portanto, recomendamos que o conjunto de dados ou a exibição seja limitada a cerca de 100 mil linhas.

Confira [problemas conhecidos](https://microsoft.github.io/SandDance/#known-issues)

## <a name="release-notes"></a>Notas de versão

### <a name="100"></a>1.0.0

Versão inicial do azdata-sanddance

## <a name="next-steps"></a>Próximas etapas
Para saber mais, [visite o repositório do GitHub](https://github.com/Microsoft/SandDance).
