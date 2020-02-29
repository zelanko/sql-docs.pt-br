---
title: Carregando planejamento de capacidade do servidor
description: Esta planilha de planejamento de capacidade ajuda a determinar os requisitos de um servidor de carregamento para carregar dados no data warehouse paralelo do sistema de plataforma de análise ".
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 1d2c3f1c0366d2c7d3d9efe700d9cfccc688dbc9
ms.sourcegitcommit: 2d4067fc7f2157d10a526dcaa5d67948581ee49e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/28/2020
ms.locfileid: "78171595"
---
# <a name="loading-server-capacity-planning-worksheet-for-analytics-platform-system"></a>Carregando planilha de planejamento de capacidade do servidor para o Analytics Platform System
Essa planilha de planejamento de capacidade ajuda a determinar os requisitos de um servidor de carregamento para carregar dados em SQL Server PDW. Use isso para criar seu plano para comprar ou provisionar servidores de carregamento existentes.

## <a name="worksheet-notes"></a>Notas da planilha

1.  Essa planilha se aplica a servidores que carregarão dados com a ferramenta de carregamento de linha de comando **dwloader** .

2.  Para carregar dados com Integration Services ou uma ferramenta de carregamento de terceiros, os requisitos podem variar dependendo das diferenças no processo de carregamento.

3.  A maioria dos requisitos se aplica ao carregamento de arquivos de dados compactados ou descompactados; quaisquer diferenças nos requisitos são indicadas em negrito.

## <a name="clipboard-capacity-planning-worksheet"></a>![Área de transferência](media/clipboard-icon.png "Área de transferência") Planilha de planejamento de capacidade

Imprima esta planilha e preencha-a com seus próprios requisitos.

|Componente|Requisito|Preencha esta coluna com seus próprios requisitos|Recomendações|
|-------------|---------------|--------------------------------------------------|-------------------|
|Armazenamento|Máximo de bytes que você planeja armazenar no servidor de carregamento em um determinado período de tempo.|![Ícone de lápis](media/pencil-icon.png "Ícone de lápis")|Para determinar os requisitos de armazenamento, descubra a quantidade de dados que você planeja armazenar no servidor de carregamento em um determinado período de tempo.  Os requisitos de capacidade são somente para arquivos de carregamento; o sistema operacional e os arquivos de carregamento devem estar em matrizes de disco diferentes.<br /><br />Por exemplo: se você planeja carregar 100 GB de dados do disco 3 vezes por dia, mas não excluir os arquivos de dados até o final da semana, você precisará de, no mínimo, 2,1 TB para armazenar os arquivos de dados. É recomendável ser conservador e obter cerca de 30% mais armazenamento para considerar as variações e o crescimento.  Neste exemplo, 2,73 TB de espaço de armazenamento seria melhor.|
|Taxa de carga|Máximo de bytes por hora de dados a serem carregados no PDW.|![Ícone de lápis](media/pencil-icon.png "Ícone de lápis")|Essa é uma estimativa. Ao computar esse requisito, suponha que os arquivos já estejam no servidor de carregamento e que outras condições de carregamento sejam as mais boas possíveis.<br /><br />Por exemplo: não há necessidade de fatorar compactação de dados, já que o dwloader sempre envia dados descompactados para o PDW. Não há necessidade de fatorar as conversões de tipo de dados e o tamanho da tabela de destino.|
|Rede|Tipo de conexão de rede.|![Ícone de lápis](media/pencil-icon.png "Ícone de lápis")|Determine o melhor tipo de conexão de rede para seus requisitos de taxa de carga.<br /><br />Por exemplo: a InfiniBand ou 10 Gbit Ethernet fornecerá as taxas de carregamento ideais. a Ethernet de 1 Gbit limitará as taxas de carga a 360 GB por hora ou menos.|
|E/S|Bytes por hora para leituras e gravações.|![Ícone de lápis](media/pencil-icon.png "Ícone de lápis")|Para carregar dados, o dwloader deve ler todos os dados do disco antes de enviá-los para o PDW.<br /><br />Cada servidor de carregamento não pode carregar dados mais rápido do que o dispositivo pode receber dados de todas as fontes de carregamento. Para economizar dinheiro, planeje a capacidade de leitura de e/s para carregamento, de forma que ela não exceda a capacidade de carregamento do dispositivo.<br /><br />Por exemplo:<br />O PDW recebe e carrega dados em um dispositivo de 1 rack com uma taxa máxima de 1,8 TB por hora. Para um dispositivo com dois ou mais racks, a taxa de carga máxima é de 3,6 TB por hora.<br /><br />Se você planeja carregar a partir de vários servidores de carregamento ao mesmo tempo, os requisitos de e/s para cada servidor de carregamento serão menores do que quando um servidor estiver fazendo todo o carregamento.<br /><br />Por exemplo: um servidor de carregamento pode carregar no máximo 1,8 TB por hora para um dispositivo de 1 rack. Dois servidores de carregamento podem carregar simultaneamente 900 GB por hora em um dispositivo de 1 rack. Níveis mais altos de simultaneidade podem reduzir a eficiência e a taxa de transferência máxima.<br /><br />Para a capacidade de e/s, leve em conta toda a e/s que ocorre no servidor de carregamento. Se o servidor de carregamento tiver outro tráfego de e/s além de carregamentos de dados, como o recebimento de arquivos de dados de um servidor ETL, os requisitos de e/s aumentarão.<br /><br />Para dados compactados, os requisitos de e/s dependem da taxa de compactação de dados. dwloader lê os dados compactados e os descompacta antes de enviá-los para o PDW. Quanto maior a taxa de compactação, menor será o número de dados que o servidor de carregamento precisará ler do disco.<br /><br />Por exemplo: se a taxa de carga necessária for de 1,8 TB por hora e os dados forem armazenados no servidor de carregamento com a compactação 2:1, o servidor de carregamento precisará apenas ler 900 GB por hora do disco em vez de 1,8 TB. Uma taxa de compactação de 3:1 significa que o servidor de carregamento precisa ler 600 GB por hora do disco.|
|CPU|Número de soquetes.|![Ícone de lápis](media/pencil-icon.png "Ícone de lápis")|Para carregar dados descompactados, o dwloader não é um aplicativo com uso intensivo de CPU.  Como requisito mínimo, é recomendável usar um servidor de 2 soquetes fabricado recentemente.<br /><br />Para carregar dados compactados, você precisa de capacidade suficiente de CPU para descompactar os dados antes de enviá-los para o PDW. o dwloader pode executar 10 threads ativos de uma vez. Se você planeja carregar 10 arquivos compactados simultaneamente, recomendamos que o servidor tenha pelo menos uma CPU de 10 núcleos ou duas CPUs com 6 núcleos.|
|RAM|GB de memória que permite ao Windows armazenar em cache arquivos durante cargas.|![Ícone de lápis](media/pencil-icon.png "Ícone de lápis")|o dwloader usa muito pouca RAM no servidor de carregamento. Para o desempenho, o Windows usa a memória para armazenar em cache os arquivos de carregamento depois de lê-los do disco.<br /><br />Para determinar os requisitos de RAM, consulte a instalação do Windows Server e os requisitos de aplicativos de terceiros. Recomendamos um mínimo de 32 GB se você não tiver requisitos de outras fontes.<br /><br />Para dados compactados, a RAM mais rápida é útil porque irá acelerar a descompactação.|

## <a name="see-also"></a>Consulte Também
[Adquirir e configurar um](acquire-and-configure-loading-server.md)
[carregador de linha de comando dwloader](dwloader.md) do servidor de carregamento

