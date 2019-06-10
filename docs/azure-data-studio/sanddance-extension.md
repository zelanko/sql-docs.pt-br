---
title: SandDance para o Studio de dados do Azure
titleSuffix: Azure Data Studio
description: Como usar o SandDance no estúdio de dados do Azure
ms.custom: seodec18
ms.date: 04/18/2019
ms.prod: sql
ms.technology: azure-data-studio
ms.reviewer: alayu; sstein
ms.topic: conceptual
author: yualan
ms.author: alayu
manager: jroth
ms.openlocfilehash: 683aea4066c0b27db295cc07db31ecd07fb33245
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66798079"
---
# <a name="sanddance-for-azure-data-studio-preview"></a>SandDance para o Studio de dados do Azure (visualização)
O estúdio de dados do Azure agora oferece uma maneira de criar visualizações rápidas para os arquivos. csv e tsv que você está trabalhando. Isso inclui arquivos locais ou arquivos no HDFS em seu Cluster de dados grande do SQL Server de 2019. Essa extensão é útil quando você está tentando ter uma rápida de examinar os dados e entender o que está acontecendo. Usamos uma tecnologia chamada SandDance da Microsoft Research, que pode gerar visualizações no local dos dados.

![animação sanddance](https://user-images.githubusercontent.com/11507384/54236654-52d42800-44d1-11e9-859e-6c5d297a46d2.gif)

Usando exibições fáceis de entender, SandDance facilita você insights sobre seus dados, que, na Ajuda do turno você contar histórias de suporte de dados, criar casos com base na evidência, teste de hipóteses, aprofunde-se em explicações superfície, dar suporte a decisões de compras, ou relacionar dados em um contexto mais amplo, o mundo real.

SandDance usa as visualizações de unidade, que se aplicam a um mapeamento individual entre linhas em seu banco de dados e as marcas na tela.
Transição animada suave entre as exibições ajuda a manter o contexto enquanto você interage com seus dados.

## <a name="usage"></a>Uso

A partir do menu Arquivo, use Abrir pasta ou [Ctrl + K, Ctrl + O] para abrir o diretório que contém o. Arquivo CSV.  Em seguida, de dentro do painel do Explorer, clique com botão direito no arquivo. csv ou tsv e escolha *modo de exibição no SandDance*.

Clique com botão direito em um arquivo. csv ou tsv no HDFS se você está conectado ao Cluster de Big Data do SQL Server de 2019 e escolha *modo de exibição no SandDance*.

## <a name="known-issues"></a>Problemas conhecidos

No momento, seus dados devem ter a primeira coluna como um identificador exclusivo.

Atualmente, não capturamos a contagem de linhas que é visualizada. No entanto, o consumo de memória aumenta proporcionalmente ao número de linhas, portanto, é recomendável que o conjunto de dados ou o modo de exibição é limitado a cerca de 100 mil linhas.

Consulte [problemas conhecidos](https://microsoft.github.io/SandDance/#known-issues)

## <a name="release-notes"></a>Notas de Versão

### <a name="100"></a>1.0.0

Versão inicial do sanddance azdata

## <a name="next-steps"></a>Próximas etapas
Para saber mais, [visite o repositório do GitHub.](https://github.com/Microsoft/SandDance)
