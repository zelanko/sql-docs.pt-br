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
manager: craigg
ms.openlocfilehash: dd63f490ed1c635abfb6bef6972363cfba3c96bc
ms.sourcegitcommit: 8d6fb6bbe3491925909b83103c409effa006df88
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/22/2019
ms.locfileid: "59981230"
---
# <a name="sanddance-for-azure-data-studio-preview"></a>SandDance para o Studio de dados do Azure (visualização)
O estúdio de dados do Azure agora oferece uma maneira de criar visualizações rápidas para os arquivos. csv e tsv que você está trabalhando. Isso inclui arquivos locais ou arquivos no HDFS em seu Cluster de dados grande do SQL Server de 2019. Essa extensão é útil quando você está tentando ter uma rápida de examinar os dados e entender o que está acontecendo. Usamos uma tecnologia chamada SandDance da Microsoft Research, que pode gerar visualizações no local dos dados.

![animação sanddance](https://user-images.githubusercontent.com/11507384/54236654-52d42800-44d1-11e9-859e-6c5d297a46d2.gif)

Usando exibições fáceis de entender, SandDance facilita você insights sobre seus dados, que, na Ajuda do turno você contar histórias de suporte de dados, criar casos com base na evidência, teste de hipóteses, aprofunde-se em explicações superfície, dar suporte a decisões de compras, ou relacionar dados em um contexto mais amplo, o mundo real.

SandDance usa as visualizações de unidade, que se aplicam a um mapeamento individual entre linhas em seu banco de dados e as marcas na tela.
Transição animada suave entre as exibições ajuda a manter o contexto enquanto você interage com seus dados.

## <a name="usage"></a>Uso

Clique duas vezes em um arquivo. csv ou tsv local e escolha *modo de exibição no SandDance*.

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