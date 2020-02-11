---
title: Planejamento de capacidade do servidor de backup
description: Essa planilha de planejamento de capacidade ajuda a determinar os requisitos de um servidor de backup para executar operações de backup e restauração de banco de dados data warehouse paralelas. Use isso para criar seu plano de compra de novos ou provisionar servidores de backup existentes.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 46dbdded5adf41a847f017cf4ee203597df13962
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "74401343"
---
# <a name="backup-server-capacity-planning-worksheet---parallel-data-warehouse"></a>Planilha de planejamento de capacidade do servidor de backup – data warehouse paralelos
Essa planilha de planejamento de capacidade ajuda a determinar os requisitos de um servidor de backup para executar SQL Server PDW operações de backup e restauração de banco de dados. Use isso para criar seu plano de compra de novos ou provisionar servidores de backup existentes.  
  
Esta planilha é um suplemento para as instruções em [adquirir e configurar um servidor de backup](acquire-and-configure-backup-server.md).  
  
## <a name="capacity-planning-worksheet-for-backup-servers"></a>Planilha de planejamento de capacidade para servidores de backup  

### <a name="notes"></a>Observações  
  
1.  Esta planilha se aplica a servidores que executarão operações de backup e restauração para bancos de dados do PDW.  
  
2.  A única maneira de fazer backup e restaurar bancos de dados do PDW é usar os comandos SQL BACKUP DATABASE e RESTOre DATABASE. No entanto, depois que os dados de backup estiverem em seu servidor de backup, ele existirá como um conjunto de arquivos do Windows. Você pode arquivar os arquivos de backup do seu servidor em outro local de armazenamento usando métodos tradicionais de backup baseado em arquivo do Windows.  
  
### <a name="clipboard-iconmediaclipboard-iconpng-clipboard-icon-capacity-planning-worksheet"></a>![Ícone da área de transferência](media/clipboard-icon.png "Ícone da área de transferência") Planilha de planejamento de capacidade 
  
Imprima esta planilha e preencha-a com seus próprios requisitos.  
  
|Componente|Requisito|Preencha esta coluna com seus próprios requisitos|Recomendações|  
|-------------|---------------|--------------------------------------------------|-------------------|  
|Armazenamento|Máximo de bytes que você planeja armazenar no servidor de backup em um determinado período de tempo.|![Ícone de lápis](media/pencil-icon.png "Ícone de lápis")|Para determinar os requisitos de armazenamento, descubra a quantidade de dados que você planeja armazenar no servidor de backup em um determinado período de tempo.<br /><br />Os dados de backup são armazenados no servidor de backup em um formato compactado. As taxas de compactação de dados dependem das características dos seus dados.<br /><br />Por exemplo: como uma estimativa aproximada, é recomendável estimar uma taxa de compactação 7:1 em relação ao tamanho dos dados descompactados. Isso pressupõe que pelo menos 80% dos dados são armazenados em índices columnstore clusterizados. Por exemplo, se você tiver 700 GB de dados descompactados em um banco e ele estiver armazenado em índices columnstore clusterizados, você poderá estimar que o backup do banco de dado precisará de aproximadamente 100 GB.<br /><br />Se você planeja ter várias cópias de backups de banco de dados no servidor de backup, precisará fazer uma conta para elas.<br /><br />Por exemplo: se você planeja fazer backup de 10 bancos de dados que cada um contém 5 TB de dado descompactado, eles têm um tamanho combinado de 50 TB. Se você planeja fazer backup desses 10 bancos de dados diariamente por 5 dias em uma linha, o tamanho total descompactado é de 250 TB. Levando em uma taxa de compactação de 7:1, você precisará de 250/7 = 35,7 TB de armazenamento no servidor de backup. É recomendável ser conservador e obter cerca de 30% de capacidade adicional para considerar as variações e o crescimento.  Neste exemplo, 46,6 TB seria melhor.|  
|Rede|Tipo de conexão de rede.|![Ícone de lápis](media/pencil-icon.png "Ícone de lápis")|Determine o melhor tipo de conexão de rede que pode atender aos seus requisitos de taxa de carga.<br /><br />Por exemplo: InfiniBand ou 10 Gbit Ethernet fornecerá as taxas de carregamento ideais. o 1Gbit Ethernet limitará as taxas de carga a 360 GB por hora ou menos.|  
|E/S|Bytes por hora para gravações.|![Ícone de lápis](media/pencil-icon.png "Ícone de lápis")|Para a gravação de backups em disco, as velocidades de gravação de 4 TB por hora são ideais.<br /><br />Por exemplo: para unidades que podem gravar 50 MB/s, você deverá ter pelo menos 24 unidades, além de mais para espelhamento ou paridade.<br /><br />Para a capacidade de e/s, leve em conta toda a e/s que ocorre no servidor de carregamento. Se o servidor de carregamento tiver outro tráfego de e/s além de carregamentos de dados, como o recebimento de arquivos de dados de um servidor ETL, os requisitos de e/s aumentarão.|  
|CPU|Número de soquetes.|![Ícone de lápis](media/pencil-icon.png "Ícone de lápis")|Receber e armazenar arquivos de backup não é um aplicativo com uso intensivo de CPU.  Como requisito mínimo, é recomendável usar um servidor de 2 soquetes fabricado recentemente.|  
|RAM|GB de memória que permite ao Windows armazenar em cache arquivos durante cargas.|![Ícone de lápis](media/pencil-icon.png "Ícone de lápis")|O recebimento e o armazenamento de arquivos de backup requer muito pouca RAM no servidor de carregamento.<br /><br />Para determinar os requisitos de RAM, consulte a instalação do Windows Server e os requisitos de aplicativos de terceiros. Recomendamos um mínimo de 32 GB se você não tiver requisitos de outras fontes.|  
  
Quando terminar de determinar os requisitos de capacidade, retorne ao tópico [adquirir e configurar um servidor de carregamento](acquire-and-configure-loading-server.md) para planejar sua compra.  
  
## <a name="see-also"></a>Consulte Também  
[Hardware de backup e carregamento](backup-and-loading-hardware.md)  
  
