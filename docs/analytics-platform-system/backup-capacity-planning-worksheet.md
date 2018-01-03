---
title: Planilha de planejamento de capacidade do servidor de backup (SQL Server PDW)
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.prod: analytics-platform-system
ms.prod_service: mpp-data-warehouse
ms.service: 
ms.component: 
ms.suite: sql
ms.custom: 
ms.technology: mpp-data-warehouse
description: "Esta planilha de planejamento de capacidade ajuda você a determinar os requisitos de um servidor de backup para executar um backup de banco de dados do SQL Server PDW e operações de restauração."
ms.date: 01/05/2017
ms.topic: article
ms.assetid: 36294bf6-6dde-481f-a190-d4382b04c030
caps.latest.revision: "6"
ms.openlocfilehash: e025410f3be18b5f8276984219dd1cb6a40c2a87
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="backup-server-capacity-planning-worksheet"></a>Planilha de planejamento de capacidade do servidor de backup
Esta planilha de planejamento de capacidade ajuda você a determinar os requisitos de um servidor de backup para executar um backup de banco de dados do SQL Server PDW e operações de restauração. Use isso para criar seu plano para compras novos ou provisionamento backup servidores existentes.  
  
Esta planilha é um suplemento para as instruções em [adquirir e configurar um servidor de Backup](acquire-and-configure-backup-server.md).  
  
## <a name="capacity-planning-worksheet-for-backup-servers"></a>Planilha de planejamento de capacidade para servidores de Backup  

### <a name="notes"></a>Observações  
  
1.  Essa planilha se aplica a servidores que executarão as operações de backup e restauração para bancos de dados do PDW.  
  
2.  A única maneira de fazer backup e restaurar bancos de dados PDW é usar os comandos de banco de dados de BACKUP e restauração do banco de dados SQL. No entanto, quando os dados de backup estiverem em seu servidor de backup, ele existe como um conjunto de arquivos do Windows. Você pode arquivar os arquivos de backup do servidor para outro local de armazenamento usando métodos tradicionais de Windows baseados em arquivo backup.  
  
### <a name="clipboard-iconmediaclipboard-iconpng-clipboard-icon-capacity-planning-worksheet"></a>![Ícone da área de transferência](media/clipboard-icon.png "ícone da área de transferência") planilha de planejamento de capacidade 
  
Esta planilha de impressão e preenchê-lo com seus próprios requisitos.  
  
|Componente|Requisito|Preencha essa coluna com seus próprios requisitos|Recomendações|  
|-------------|---------------|--------------------------------------------------|-------------------|  
|Armazenamento|Você planeja armazenar no servidor de backup em qualquer determinado período de tempo máximo de bytes.|![Ícone de lápis](media/pencil-icon.png "ícone de lápis")|Para determinar os requisitos de armazenamento, calcule a quantidade de dados você planeja armazenar no servidor de backup em qualquer período de tempo determinado.<br /><br />Os dados de backup são armazenados no servidor de backup em um formato compactado. Taxas de compactação de dados dependem das características de seus dados.<br /><br />Por exemplo: como uma estimativa aproximada, recomendamos calcular uma taxa de compactação de 7:1 em relação ao tamanho dos dados descompactados. Isso pressupõe que pelo menos 80% dos dados é armazenado em índices columnstore clusterizados. Por exemplo, se você tiver 700 GB de dados não compactados em um banco de dados e são armazenadas em índices columnstore clusterizados, em seguida, você pode estimar que o backup do banco de dados serão necessários cerca de 100 GB.<br /><br />Se você planeja ter várias cópias de backups de banco de dados no servidor de backup, você precisa de conta para eles.<br /><br />Por exemplo: se você pretende fazer backup de 10 bancos de dados que contêm 5 TB de dados não compactados, os bancos de dados têm um tamanho combinado de 50 TB. Se você planeja esses todos os dias de 10 bancos de dados de backup por 5 dias em uma linha, o tamanho descompactado total é 250 TB. Acrescentando uma taxa de compactação de 7:1, você precisará 250 / 7 = 35.7 TB de armazenamento no servidor de backup. É recomendável sendo conservadora e Obtendo sobre capacidade adicional de 30% de conta para as variações e expandir.  Neste exemplo, seria melhor 46.6 TB.|  
|Rede|Tipo de conexão de rede.|![Ícone de lápis](media/pencil-icon.png "ícone de lápis")|Determine o melhor tipo de conexão de rede que pode atender aos seus requisitos de taxa de carga.<br /><br />Por exemplo: InfiniBand ou 10Gbit Ethernet fornecem o melhor carregar taxas. Ethernet de 1 Gbit limitará taxas de carga para 360 GB por hora ou menos.|  
|E/S|Bytes por hora para gravações.|![Ícone de lápis](media/pencil-icon.png "ícone de lápis")|Para gravar backups em disco, 4 TB por hora velocidades de gravação são ideais.<br /><br />Por exemplo: para unidades que podem gravar a 50 MB/s, você deve pelo menos 24 drives, além de mais para espelhamento ou paridade.<br /><br />Capacidade de e/s, levam em consideração todos a e/s ocorrendo no servidor de carregamento. Se o servidor de carregamento tem outro tráfego de e/s, além de carregamentos de dados, como a recepção de arquivos de dados de um servidor ETL, aumenta os requisitos de e/s.|  
|CPU|Número de soquetes.|![Ícone de lápis](media/pencil-icon.png "ícone de lápis")|Recebimento e armazenamento de arquivos de backup não é um aplicativo de uso intensivo de CPU.  Como um requisito mínimo, é recomendável usar um servidor de soquete 2 fabricados recentemente.|  
|RAM|GB de memória que permite que o Windows em cache os arquivos durante o carrega.|![Ícone de lápis](media/pencil-icon.png "ícone de lápis")|Recebimento e armazenamento de arquivos de backup requerem muito pouco RAM no servidor de carregamento.<br /><br />Para determinar os requisitos de RAM, consulte a sua instalação do Windows Server e os requisitos de aplicativo de parte 3. Se você não tem requisitos de outras fontes, é recomendável um mínimo de 32 GB.|  
  
Quando tiver terminado de determinar seus requisitos de capacidade, retorne para o [adquirir e configurar um servidor carregando](acquire-and-configure-loading-server.md) tópico para planejar sua compra.  
  
## <a name="see-also"></a>Consulte Também  
[Backup e carregamento de hardware](backup-and-loading-hardware.md)  
  
