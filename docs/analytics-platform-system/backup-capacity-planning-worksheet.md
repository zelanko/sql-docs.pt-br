---
title: Planejamento de capacidade do servidor de backup - Parallel Data Warehouse | Microsoft Docs
description: Esta planilha de planejamento de capacidade ajuda você a determinar os requisitos para um servidor de backup para executar o backup de banco de dados do Parallel Data Warehouse e operações de restauração. Use isso para criar seu plano de compras novos ou provisionamento backup servidores existentes.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 500bebab375a0d0b94032a1855af3844bc2e6fa7
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63295056"
---
# <a name="backup-server-capacity-planning-worksheet---parallel-data-warehouse"></a>Planilha de planejamento de capacidade do servidor de backup - Parallel Data Warehouse
Esta planilha de planejamento de capacidade ajuda você a determinar os requisitos para um servidor de backup para executar o backup de banco de dados do SQL Server PDW e operações de restauração. Use isso para criar seu plano de compras novos ou provisionamento backup servidores existentes.  
  
Esta planilha é um suplemento para as instruções em [adquirir e configurar um servidor de Backup](acquire-and-configure-backup-server.md).  
  
## <a name="capacity-planning-worksheet-for-backup-servers"></a>Planilha de planejamento de capacidade para servidores de Backup  

### <a name="notes"></a>Observações  
  
1.  Esta planilha aplica-se aos servidores que executará operações de backup e restauração para bancos de dados do PDW.  
  
2.  É a única maneira de fazer backup e restaurar bancos de dados do PDW usar os comandos de banco de dados de BACKUP e RESTAURAR o banco de dados SQL. No entanto, quando os dados de backup estiverem em seu servidor de backup, ele existe como um conjunto de arquivos do Windows. Você pode arquivar os arquivos de backup do seu servidor para outro local de armazenamento usando os métodos tradicionais de Windows baseados em arquivo backup.  
  
### <a name="clipboard-iconmediaclipboard-iconpng-clipboard-icon-capacity-planning-worksheet"></a>![Ícone da área de transferência](media/clipboard-icon.png "ícone de área de transferência") planilha de planejamento de capacidade 
  
Imprima esta planilha e preenchê-lo com seus próprios requisitos.  
  
|Componente|Requisito|Preencha essa coluna com seus próprios requisitos|Recomendações|  
|-------------|---------------|--------------------------------------------------|-------------------|  
|Armazenamento|Você planeja armazenar no servidor de backup em qualquer determinado período de tempo máximo de bytes.|![Ícone de lápis](media/pencil-icon.png "ícone de lápis")|Para determinar os requisitos de armazenamento, descobrir quantos dados você pretende armazenar no servidor de backup em qualquer período de tempo determinado.<br /><br />Os dados de backup são armazenados no servidor de backup em um formato compactado. As taxas de compactação de dados dependem as características de seus dados.<br /><br />Por exemplo:  Uma estimativa aproximada, recomendamos como estimar uma taxa de compactação de 7:1 relativo ao tamanho dos dados descompactados. Isso pressupõe que pelo menos 80% dos dados é armazenado em índices columnstore clusterizados. Por exemplo, se você tiver 700 GB de dados descompactados em um banco de dados e é armazenado em índices columnstore clusterizados, em seguida, você pode estimar que o backup do banco de dados serão necessários cerca de 100 GB.<br /><br />Se você planeja ter várias cópias de backups de banco de dados no servidor de backup, você precisa levar em conta para eles.<br /><br />Por exemplo:  Se você planeja fazer backup de 10 bancos de dados que contêm 5 TB de dados não compactados, os bancos de dados têm um tamanho combinado de 50 TB. Se você planeja fazer backup desses todos os dias de 10 bancos de dados por cinco dias em uma linha, o tamanho descompactado total é de 250 TB. Incluindo uma taxa de compactação: 1 a 7, você precisará de 250 / 7 = 35.7 TB de armazenamento em seu servidor de backup. É recomendável ser conservador e Obtendo sobre capacidade adicional de 30% de conta para as variações e expandir.  Neste exemplo, seria melhor 46.6 TB.|  
|Rede|Tipo de conexão de rede.|![Ícone de lápis](media/pencil-icon.png "ícone de lápis")|Determine o melhor tipo de conexão de rede que pode atender às suas necessidades de taxa de carga.<br /><br />Por exemplo:  InfiniBand ou taxas de carregamento de 10 Gbit Ethernet fornecerá o ideal. Ethernet de 1 Gbit limitará as taxas de carga para 360 GB por hora ou menos.|  
|E/S|Bytes por hora para gravações.|![Ícone de lápis](media/pencil-icon.png "ícone de lápis")|Para gravar backups em disco, 4 TB por hora velocidades de gravação são ideais.<br /><br />Por exemplo:  Para unidades que podem gravar a 50 MB/s, você deve pelo menos 24 unidades, além de mais para o espelhamento ou paridade.<br /><br />Capacidade de e/s, levar em conta todas as e/s ocorrendo no servidor de carregamento. Se o servidor de carregamento tiver outro tráfego de e/s, além de carregamentos de dados, como a recepção de arquivos de dados de um servidor ETL, aumentará os requisitos de e/s.|  
|CPU|Número de soquetes.|![Ícone de lápis](media/pencil-icon.png "ícone de lápis")|Receber e armazenar arquivos de backup não é um aplicativo de uso intensivo de CPU.  Como um requisito mínimo, é recomendável usar um servidor de soquete 2 fabricados recentemente.|  
|RAM|GB de memória que permite que o Windows em cache os arquivos durante o carrega.|![Ícone de lápis](media/pencil-icon.png "ícone de lápis")|Receber e armazenar arquivos de backup requerem muito pouca RAM no servidor de carregamento.<br /><br />Para determinar os requisitos de RAM, consulte a sua instalação do Windows Server e os requisitos de aplicativo de terceiros 3ª. Se você não tiver requisitos de outras fontes, é recomendável um mínimo de 32 GB.|  
  
Quando tiver terminado de determinar os requisitos de capacidade, volte para o [adquirir e configurar um servidor carregando](acquire-and-configure-loading-server.md) tópico para planejar sua compra.  
  
## <a name="see-also"></a>Consulte também  
[Backup e carregamento de hardware](backup-and-loading-hardware.md)  
  
