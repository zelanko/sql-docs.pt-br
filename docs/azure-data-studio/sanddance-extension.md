---
title: SandDance para Azure Data Studio
titleSuffix: Azure Data Studio
description: Como usar SandDance no Azure Data Studio
ms.custom: seodec18
ms.date: 07/03/2019
ms.prod: sql
ms.technology: azure-data-studio
ms.reviewer: alayu; sstein
ms.topic: conceptual
author: yualan
ms.author: alayu
ms.openlocfilehash: a96bde6a66642bf02cc076c3d4d4f3ac44e02a3f
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/25/2019
ms.locfileid: "67959337"
---
# <a name="sanddance-for-azure-data-studio-preview"></a>SandDance para Azure Data Studio (versão prévia)
Agora, o Azure Data Studio oferece uma maneira de criar visualizações rápidas para os arquivos .csv e .tsv em que você está trabalhando. Isso inclui arquivos locais ou arquivos no HDFS em seu cluster de Big Data do SQL Server 2019. Essa extensão é útil quando você está tentando ter uma visão rápida dos dados e entender o que está acontecendo. Usamos uma tecnologia chamada SandDance da Microsoft Research, que pode gerar visualizações dos dados no local.

![sanddance-animation](https://user-images.githubusercontent.com/11507384/54236654-52d42800-44d1-11e9-859e-6c5d297a46d2.gif)

Usando exibições fáceis de entender, o SandDance ajuda você a chegar a insights sobre seus dados que, por sua vez, o ajudam a contar histórias com suporte de dados, criar casos com base em evidências, testar hipóteses, aprofundar-se em explicações superficiais, dar suporte a decisões de compra ou relacionar dados a um contexto mais amplo do mundo real.

O SandDance usa visualizações de unidade, que aplicam um mapeamento de um para um entre linhas no banco de dados e marcas na tela.
Transições animadas suaves entre os modos de exibição ajudam a manter o contexto à medida que você interage com seus dados.

## <a name="usage"></a>Uso

Começando no menu Arquivo, use Abrir Pasta ou [Ctrl + K Ctrl + O] para abrir o diretório que contém o arquivo .CSV.  Em seguida, no painel do Explorer, clique com o botão direito do mouse no arquivo .csv ou .tsv e escolha *Exibir no SandDance*.

Clique com o botão direito do mouse em um arquivo .csv ou .tsv no HDFS se você estiver conectado a um cluster de Big Data do SQL Server 2019 e escolha *Exibir no SandDance*.

## <a name="known-issues"></a>Problemas conhecidos

No momento, os dados devem ter a primeira coluna como um identificador exclusivo.

Atualmente, não limitamos a contagem de linhas que é visualizada. No entanto, o consumo de memória aumenta proporcionalmente ao número de linhas, portanto, recomendamos que o conjunto de dados ou a exibição seja limitada a cerca de 100 mil linhas.

Confira [problemas conhecidos](https://microsoft.github.io/SandDance/#known-issues)

## <a name="release-notes"></a>Notas de Versão

### <a name="100"></a>1.0.0

Versão inicial do azdata-sanddance

## <a name="next-steps"></a>Next Steps
Para saber mais, [visite o repositório do GitHub](https://github.com/Microsoft/SandDance).
