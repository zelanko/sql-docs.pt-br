---
title: Carregando a capacidade do servidor planejamento - Analytics Platform System | Microsoft Docs
description: Esta planilha de planejamento de capacidade ajuda você a determinar os requisitos para um servidor de carregamento para carregar dados para o Analytics Platform System Parallel Data Warehouse."
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 2f0efd7e0688496d5af7887431ca00ae683c874f
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63213382"
---
# <a name="loading-server-capacity-planning-worksheet-for-analytics-platform-system"></a>Ao carregar a planilha de planejamento de capacidade do servidor para o Analytics Platform System
Esta planilha de planejamento de capacidade ajuda você a determinar os requisitos para um servidor de carregamento para carregar dados no SQL Server PDW. Use isso para criar seu plano para compra ou provisionar servidores de carregamento existente.  
  
## <a name="worksheet-notes"></a>Notas de planilha
  
1.  Esta planilha aplica-se aos servidores que serão carregamento de dados com o **dwloader** a ferramenta de carregamento de linha de comando.  
  
2.  Para carregar dados com o Integration Services ou uma ferramenta de carregamento de terceiros, os requisitos podem variar dependendo das diferenças no processo de carregamento.  
  
3.  A maioria dos requisitos se aplicam ao carregar qualquer um dos arquivos de dados compactado ou descompactado; quaisquer diferenças em requisitos são indicadas em negrito.  
  
## <a name="clipboardmediaclipboard-iconpng-clipboard-capacity-planning-worksheet"></a>![Área de transferência](media/clipboard-icon.png "área de transferência") planilha de planejamento de capacidade  
  
Imprima esta planilha e preenchê-lo com seus próprios requisitos.  
  
|Componente|Requisito|Preencha essa coluna com seus próprios requisitos|Recomendações|  
|-------------|---------------|--------------------------------------------------|-------------------|  
|Armazenamento|Você planeja armazenar no servidor de carregamento em qualquer determinado período de tempo máximo de bytes.|![Ícone de lápis](media/pencil-icon.png "ícone de lápis")|Para determinar os requisitos de armazenamento, descobrir quantos dados você pretende armazenar no servidor de carregamento em qualquer período de tempo determinado.  Os requisitos de capacidade são para carregar os arquivos. o sistema operacional e os arquivos de carga devem ser em matrizes de disco diferente.<br /><br />Por exemplo:  Se você planeja carregar 100 GB de dados do disco 3 vezes a cada dia, mas não exclui os dados de arquivos até o final de semana, em seguida, você precisa um TB 2.1 mínimo para armazenar os arquivos de dados. É recomendável ser conservador e Obtendo sobre armazenamento de 30% a mais para levar em conta as variações e crescimento.  Neste exemplo, seria melhor 2.73 TB de espaço de armazenamento.|  
|Taxa de carga|Máximo de bytes por hora de dados para carregar no PDW.|![Ícone de lápis](media/pencil-icon.png "ícone de lápis")|Essa é uma estimativa. Ao calcular esse requisito, pressupõem que os arquivos já estão no servidor de carregamento e que outras condições de carregamento são tão bons quanto possíveis.<br /><br />Por exemplo:  Não há necessidade de considerar de compactação de dados, pois dwloader sempre envia descompactados dados para o PDW. Não é necessário considerar em conversões de tipo de dados e o tamanho da tabela de destino.|  
|Rede|Tipo de conexão de rede.|![Ícone de lápis](media/pencil-icon.png "ícone de lápis")|Determine o melhor tipo de conexão de rede para seus requisitos de taxa de carga.<br /><br />Por exemplo:  InfiniBand ou 10 Gbit Ethernet fornecerá as taxas de carregamento ideal. Ethernet de 1 Gbit limitará as taxas de carga para 360 GB por hora ou menos.|  
|E/S|Bytes por hora para leituras e gravações.|![Ícone de lápis](media/pencil-icon.png "ícone de lápis")|Para carregar dados, dwloader deve ler todos os dados do disco antes de enviá-lo ao PDW.<br /><br />Cada servidor de carregamento não é possível carregar os dados mais rápido do que o dispositivo pode receber dados de todas as fontes de carregamento. Para economizar dinheiro, planeje a capacidade de carregamento de forma que não exceda a capacidade de carga do dispositivo de leitura e/s.<br /><br />Por exemplo: <br />PDW recebe e carrega dados em um dispositivo de rack de 1 a uma taxa máxima de 1,8 TB por hora. Para um dispositivo com 2 ou mais racks, a taxa de carga máxima é 3.6 TB por hora.<br /><br />Se você planeja carregar de vários servidores de carregamento ao mesmo tempo, os requisitos de e/s para cada servidor de carregamento será menor do que quando um servidor está fazendo todo o carregamento.<br /><br />Por exemplo:  Um servidor de carregamento pode carregar um máximo de 1,8 TB por hora para um dispositivo de rack 1. Dois servidores de carregamento pode cada simultaneamente carregar 900 GB por hora em um dispositivo de rack 1. Níveis mais altos de simultaneidade podem reduzir a eficiência e a taxa de transferência máxima.<br /><br />Capacidade de e/s, levar em conta todas as e/s ocorrendo no servidor de carregamento. Se o servidor de carregamento tiver outro tráfego de e/s, além de carregamentos de dados, como a recepção de arquivos de dados de um servidor ETL, aumentará os requisitos de e/s.<br /><br />Para dados compactados, os requisitos de e/s dependem da taxa de compactação de dados. dwloader lê os dados compactados e, em seguida, descompacta-lo antes de enviá-lo ao PDW. Quanto maior a taxa de compactação, os menos dados carregando o servidor precisará ler do disco.<br /><br />Por exemplo:  Se a taxa de carga necessário é 1,8 TB por hora, e os dados são armazenados no servidor de carregamento com a compactação de 2:1, em seguida, o servidor de carregamento precisa apenas ler 900 GB por hora do disco, em vez de 1,8 TB. Uma taxa de compactação de 3:1 significa que o servidor de carregamento precisa ler 600 GB por hora do disco.|  
|CPU|Número de soquetes.|![Ícone de lápis](media/pencil-icon.png "ícone de lápis")|Para carregar os dados não compactados, dwloader não é um aplicativo de uso intensivo de CPU.  Como um requisito mínimo, é recomendável usar um servidor de soquete 2 fabricados recentemente.<br /><br />Para carregar dados compactados, você precisa de capacidade suficiente da CPU para descompactar os dados antes de enviá-lo ao PDW. dwloader pode executar 10 threads ativos ao mesmo tempo. Se você planeja carregar os arquivos compactados 10 simultaneamente, é recomendável que o servidor tem pelo menos uma CPU de 10 núcleos ou duas CPUs de 6 núcleos.|  
|RAM|GB de memória que permite que o Windows em cache os arquivos durante o carrega.|![Ícone de lápis](media/pencil-icon.png "ícone de lápis")|dwloader usa muito pouca RAM no servidor de carregamento. Para desempenho, o Windows usa memória em cache os arquivos de carregamento depois de lê-los a partir do disco.<br /><br />Para determinar os requisitos de RAM, consulte a sua instalação do Windows Server e os requisitos de aplicativo de terceiros 3ª. Se você não tiver requisitos de outras fontes, é recomendável um mínimo de 32 GB.<br /><br />Para dados compactados, RAM mais rápido é útil porque ele agilizará a descompactação.|  
  
## <a name="see-also"></a>Consulte também  
[Adquirir e configurar um servidor de carregamento](acquire-and-configure-loading-server.md)  
[Carregador de linha de comando do dwloader](dwloader.md)  
  
