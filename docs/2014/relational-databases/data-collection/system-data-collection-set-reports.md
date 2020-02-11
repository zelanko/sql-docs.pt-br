---
title: Relatórios do conjuntos de coleta de dados do sistema | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- data collector [SQL Server], server activity
- server activity [SQL Server]
- reports [SQL Server], data collection
- reports [SQL Server], disk usage
- collection sets [SQL Server], reports
- data collector [SQL Server], reports
- reports [SQL Server], query statistics
- query statistics reports [SQL Server]
- disk usage reports [SQL Server]
ms.assetid: 0b126b8d-4fe7-443d-8a9a-c266350181e5
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 39bd24414e2382557a22469da502bad91abe20b7
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62873404"
---
# <a name="system-data-collection-set-reports"></a>Relatórios do conjuntos de coleta de dados do sistema
  O coletor de dados fornece um relatório histórico para cada um dos conjuntos de coleta de Dados do Sistema. Cada um dos relatórios a seguir usa dados que estão armazenados no data warehouse de gerenciamento:  
  
-   [Resumo de Uso do Disco](#Disk)  
  
-   [Histórico de Estatísticas de Consulta](#Query)  
  
-   [Histórico de Atividade do Servidor](#Server)  
  
 Você pode usar estes relatórios para obter informações para monitorar capacidade de sistema e solucionar problemas de desempenho do sistema.  
  
##  <a name="Disk"></a> Relatório Resumo de Uso do Disco  
 O relatório Resumo de Uso do Disco contém dados sobre o uso do espaço em disco para todos os bancos de dados na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Os dados fornecidos nos relatórios são obtidos com o uso do conjunto de coleta Uso do Disco, que usa o tipo de coletor de Consultas T-SQL Genérico.  
  
 Você acessa o relatório de Resumo de Uso do Disco no Pesquisador de Objetos. Para exibir o relatório, expanda a pasta **Gerenciamento** , clique com o botão direito do mouse em **Coleção de Dados**, aponte para **Relatórios**, **Data Warehouse de Gerenciamento**e clique em **Resumo de Uso do Disco**. Para obter mais informações, consulte [Exibir um relatório de conjuntos de coleta &#40;SQL Server Management Studio&#41;](view-a-collection-set-report-sql-server-management-studio.md).  
  
### <a name="disk-usage-collection-set-report"></a>Relatório Conjunto de Coleta de Uso do Disco  
 O relatório de Conjunto de Coleta de Uso do Disco fornece uma visão geral do espaço em disco usado para todos os bancos de dados da instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]e das tendências de crescimento de arquivos de dados e de log de cada um desses bancos de dados.  
  
-   A tabela de resumo exibe o tamanho inicial (em megabytes) e o tamanho atual de todos os bancos de dados instalados no servidor que o coletor de dados está monitorando.  
  
-   Tendência e informações de crescimento médio são mostradas gráfica e numericamente para arquivos de dados e de log.  
  
#### <a name="disk-usage-collection-set---database-database_name-subreport"></a>Sub-relatório Conjunto de Coleta de Uso do Disco: <database_name>.  
 O sub-relatório Conjunto de Coleta de Uso do Disco: *<database_name>* será exibido quando você clicar em uma linha de tendência de um banco de dados ou arquivo de log específico na tabela de resumo do relatório Conjunto de Coleta de Uso do Disco. Este relatório fornece uma representação gráfica de tendências de crescimento em uso do espaço em disco em um período do relatório. O uso do disco é organizado e relatado por espaço usado, espaço de dados, espaço não alocado e espaço de índice para arquivos de dados e por espaço usado e não usado para arquivos de log.  
  
 A tabela abaixo do gráfico lista as horas de coleta de dados e os dados de uso correspondentes.  
  
#### <a name="disk-usage-for-database-database_name-subreport"></a>Sub-relatório Uso de Disco para o Banco de Dados: <database_name>.  
 O sub-relatório **Uso de disco para o banco de dados:** _<database_name>_ é exibido quando você clica no nome de um banco de dados na tabela de resumo do relatório Conjunto de Coleta de Uso do Disco. Esse relatório fornece uma análise numérica e gráfica do uso do espaço pelos arquivos de dados e log de transação do banco de dados. O uso de espaço para arquivos de dados é categorizado como uma porcentagem alocada a páginas de índice, espaço alocado, páginas de dados e espaço não utilizado. Essas categorias são definidas da seguinte forma:  
  
|Categoria|Definição|  
|--------------|----------------|  
|Índice|A quantidade de espaço em disco usada para manter páginas de índice.|  
|Não alocado|A quantidade de espaço em disco disponível para o banco de dados, mas que ainda não foi alocada a objeto algum.|  
|data|A quantidade de espaço em disco usada para manter páginas de dados.|  
|Não usado|A quantidade de espaço em disco alocada a um ou mais objetos, mas que ainda não foi utilizada.|  
  
 O uso de espaço para arquivos de log de transação é categorizado como uma espaço usado e não usado.  
  
 Eventos de crescimento automático e de redução automática serão reportados para os arquivos de dados e de log se ocorrerem no banco de dados. O relatório exibe a hora inicial e a duração de cada evento e a alteração resultante no tamanho do arquivo.  
  
 O espaço em disco usado por todo arquivo de dados do banco de dados é reportado. O espaço reportado como Espaço Reservado é a quantidade de espaço usado mais o espaço alocado ao arquivo e que ainda não foi utilizado. O espaço relatado por Espaço Usado é o espaço real usado atualmente pelo arquivo, excluindo o espaço alocado.  
  
##  <a name="Query"></a> Relatório histórico de estatísticas de consulta  
 O relatório Histórico de Estatísticas de Consulta contém estatísticas execução. Os dados usados nesse relatório são obtidos com o uso do conjunto de coleta Estatísticas de Consulta, que usa o Tipo de Coletor de Atividades de Consulta.  
  
 É possível acessar o relatório Histórico de Estatísticas da Consulta no Pesquisador de Objetos. Para exibir o relatório, expanda a pasta **Gerenciamento** , clique com o botão direito do mouse em **Coleção de Dados**, aponte para **Relatórios**, **Data Warehouse de Gerenciamento**e clique em **Histórico de Estatísticas de Consulta**. Para obter mais informações, consulte [Exibir um relatório de conjuntos de coleta &#40;SQL Server Management Studio&#41;](view-a-collection-set-report-sql-server-management-studio.md).  
  
### <a name="selecting-data-to-include-in-the-report"></a>Selecionando dados que serão incluídos no relatório  
 O relatório inclui estatísticas de execução de consulta de todo o período de coleta. Há duas maneiras de navegar pela linha de tempo da coleção de dados para selecionar um segmento de dados para exibição.  
  
 **Controle de linha de tempo e botões de navegação**  
  
 Use controle da linha de tempo e os botões de navegação para movimentar-se pela linha do tempo ou selecione um intervalo de datas. Os botões de seta fornecem navegação para a esquerda e para a direita, assim você pode retroceder e avançar pela linha do tempo. Por padrão, o movimento das setas na linha do tempo é feito em incrementos de quatro horas. Usando os botões do ampliador, é possível expandir ou reduzir esse incremento de tempo para um destes valores: 15 minutos, 1 hora, 4 horas, 12 horas ou 24 horas. O intervalo de tempo selecionado é indicado pela parte destacada da linha do tempo e exibido no texto abaixo dela. Esses valores, bem como os dados do relatório, serão atualizados sempre que você clicar na linha do tempo ou usar os botões de navegação.  
  
 **Botão Calendário**  
  
 Use o botão de calendário para especificar a data e a hora de início e a duração dos dados que servirão de base para o relatório.  
  
#### <a name="query-statistics-history-report"></a>Relatório histórico de estatísticas de consulta  
 O gráfico Principais Consultas por CPU Total mostra a despesa relativa de cada consulta para o intervalo de tempo selecionado com base no uso total da CPU. Para ver uma exibição diferente da despesa relativa da consulta, clique em um dos hiperlinks fornecidos abaixo do gráfico: **Duração**, **Total de E/S**, **Leituras Físicas**ou **Gravações Lógicas**.  
  
 A tabela abaixo do gráfico fornece dados de consulta adicionais. Ele lista o texto de cada consulta do gráfico juntamente com informações estatísticas detalhadas. Observe que as barras do gráfico são links ativos, assim como cada uma das consultas mostradas na tabela. Basta clicar em um link ativo para abrir o sub-relatório Detalhes da Consulta da consulta.  
  
#### <a name="query-details-subreport"></a>Sub-relatório Detalhes da Consulta  
 O sub-relatório Detalhes da Consulta fornece o texto inteiro da consulta. Há um hiperlink **Editar Texto da Consulta** adjacente à consulta. Basta clicar nele para abrir a consulta no Editor de Consulta. A tabela abaixo da consulta fornece estatísticas de execução de consulta, como duração média por execução de consulta.  
  
 São exibidos um gráfico de planos de consulta e a duração média por execução. Para ver uma exibição diferente do custo relativo do plano de consulta, clique em um dos hiperlinks exibidos abaixo do gráfico: **Duração**, **Leituras Físicas**ou **Gravações Lógicas**. A linha de gráfico está ativa e você pode clicar em qualquer ponto para abrir o sub-relatório Detalhes do Plano de Consulta.  
  
 A tabela abaixo do gráfico mostra os 10 principais planos de consulta baseados no uso de CPU por execução. Cada número na coluna **Nº de Plano** é um link ativo em que você clica para abrir o sub-relatório Detalhes do Plano de Consulta.  
  
#### <a name="query-plan-details-subreport"></a>Sub-relatório Detalhes do Plano de Consulta  
 Este relatório exibe as informações de um plano de consulta. Além de permitir editar as estatísticas de execução de consulta e exibição, o relatório fornece informações detalhadas sobre o plano de consulta. O hiperlink **Exibir plano de execução de consulta gráfica** abre uma representação gráfica do plano de execução da consulta atual.  
  
## <a name="server-activity-history-report"></a>Relatório histórico de atividade do servidor  
 O relatório Histórico de Atividade do Servidor contém dados de consumo de recursos e atividade do servidor e da instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Os dados fornecidos nesse relatório são coletados pelo conjunto de coleta Atividade do Servidor, que usa o tipo de coletor de Consultas T-SQL Genérico e o tipo de coletor Contadores de Desempenho.  
  
 É possível acessar o relatório Histórico de Atividade do Servidor no Pesquisador de Objetos. Para exibir o relatório, expanda a pasta **Gerenciamento** , clique com o botão direito do mouse em **Coleção de Dados**, aponte para **Relatórios**, **Data Warehouse de Gerenciamento**e clique em **Histórico de Atividade do Servidor**. Para obter mais informações, consulte [Exibir um relatório de conjuntos de coleta &#40;SQL Server Management Studio&#41;](view-a-collection-set-report-sql-server-management-studio.md).  
  
### <a name="selecting-data-to-include-in-the-report"></a>Selecionando dados que serão incluídos no relatório  
 O relatório inclui as atividades do servidor de todo o período de coleta. Há duas maneiras de navegar pela linha de tempo da coleção de dados para selecionar um segmento de dados para exibição.  
  
 **Controle de linha de tempo e botões de navegação**  
  
 Use controle da linha de tempo e os botões de navegação para movimentar-se pela linha do tempo ou selecione um intervalo de datas. Os botões de seta fornecem navegação para a esquerda e para a direita, assim você pode retroceder e avançar pela linha do tempo. Por padrão, o movimento das setas na linha do tempo é feito em incrementos de quatro horas. Usando os botões do ampliador, é possível expandir ou reduzir esse incremento de tempo para um destes valores: 15 minutos, 1 hora, 4 horas, 12 horas ou 24 horas. O intervalo de tempo selecionado é indicado pela parte destacada da linha do tempo e exibido no texto abaixo dela. Esses valores, bem como os dados do relatório, são atualizados sempre que você clica na linha do tempo ou usa os botões de navegação.  
  
 **Botão Calendário**  
  
 Use o botão de calendário para especificar a data e a hora de início e a duração dos dados que servirão de base para o relatório.  
  
###  <a name="Server"></a> Relatório histórico de atividade do servidor  
 O relatório Histórico de Atividade do Servidor mostra a exibição inicial do relatório de atividade do servidor para uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e o sistema operacional de host.  
  
 A tabela a seguir descreve os gráficos que plotam a atividade do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e do sistema no relatório e os sub-relatórios detalhados que podem ser acessados através desses gráficos.  
  
|Grafo|Descrição do relatório|  
|-----------|------------------------|  
|%CPU|Para acessar esses sub-relatórios, basta clicar em qualquer ponto das linhas do gráfico %CPU do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou do Sistema.<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]<br /> O relatório Histórico de Estatísticas de Consulta apresenta um gráfico das consultas mais caras na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. A tabela abaixo do gráfico lista as consultas e inclui dados estatísticos para cada uma. Você pode clicar em uma consulta para obter mais detalhes.<br /><br /> Sistema<br /> O relatório Uso de CPU do Sistema apresenta um gráfico de % de tempo de CPU por processador e os dados estatísticos de cada processo no formato de tabela.|  
|Uso de Memória|Para acessar esses sub-relatórios, basta clicar em qualquer ponto das linhas do gráfico Uso de Memória do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou do Sistema.<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]<br /> O relatório Uso de Memória do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] apresenta gráficos para o uso de memória de processamento, contadores de memória, consumo de memória interna por tipo e uma tabela do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que fornece dados sobre o uso médio de memória pelo tipo de componente.<br /><br /> Sistema<br /> O relatório Uso de Memória do Sistema apresenta gráficos do uso de memória, taxas de acertos do cache e da página que fornecem informações sobre o conjunto de trabalho e bytes privados de cada processo.|  
|Uso de E/S de disco|Para acessar esses sub-relatórios, basta clicar em qualquer ponto das linhas do gráfico Uso de E/S de Disco do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou do Sistema.<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]<br /> O relatório Uso de E/S de Disco do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] apresenta gráficos do tempo de resposta do disco e da taxa de transferência do disco. Uma tabela adicional fornece estatísticas de arquivo virtual por disco, banco de dados e arquivo.<br /><br /> Sistema<br /> O relatório Uso de Disco do Sistema fornece gráficos de tempo de resposta do disco, comprimento médio da fila do disco, taxa de transferência do disco e uma tabela que fornece informações sobre gravações e leituras de E/S de cada processo.|  
|Uso de Rede|Não há mais relatórios disponíveis.|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Esperas|O gráfico Esperas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] exibe as esperas encontradas por threads executados por categoria de espera. Para acessar um relatório detalhado, clique em qualquer segmento do gráfico. Além de fornecer estatísticas de espera do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em gráficos em um período reduzido, esse relatório fornece informações sobre as categorias de espera no formato em tabela. Para cada categoria, como CPU e suas subcategorias, a tabela mostra o número de esperas, o tempo de espera e a porcentagem do tempo de espera total.|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Atividade|Aspectos diferentes de atividade do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] podem ser acessados pelo gráfico Atividade do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Os relatórios que você pode obter clicando em um ponto na linha de gráfico Compilações do SQL/segundo são como se segue:<br /><br /> Conexões e sessões<br /><br /> Requests<br /><br /> Taxa de acertos do cache de plano<br /><br /> recursos de tempdb|  
  
## <a name="see-also"></a>Consulte Também  
 [Coleta de Dados](data-collection.md)   
 [Exibir um relatório de conjuntos de coleta &#40;SQL Server Management Studio&#41;](view-a-collection-set-report-sql-server-management-studio.md)  
  
  
