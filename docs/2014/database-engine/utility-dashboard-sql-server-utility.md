---
title: Painel do utilitário (Utilitário do SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
ms.assetid: 999eb741-4a60-43f6-ab37-2df7dce845c1
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 5f0eb497499eafe16756becfb9607b925add08e9
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62773808"
---
# <a name="utility-dashboard-sql-server-utility"></a>Painel do Utilitário (Utilitário do SQL Server)
  Para consultar dados no painel do Utilitário do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], selecione o nó superior na árvore do Gerenciador do Utilitário, identificado como “Utility<UCP_Name>\\(ComputerName\UCP).” O painel inclui dados resumidos e dados detalhados de todas as instâncias gerenciadas do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] e todos os aplicativos da camada de dados do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Utility. Para atualizar dados no painel, clique com o botão direito do mouse no nó superior da árvore do Gerenciador do Utilitário e selecione **Atualizar**.  
  
 Para obter mais informações sobre como criar um ponto de controle do utilitário, veja [Criar um ponto de controle do Utilitário do SQL Server &#40;Utilitário do SQL Server&#41;](../relational-databases/manage/create-a-sql-server-utility-control-point-sql-server-utility.md). Para obter mais informações sobre como adicionar uma instância do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] ao Utilitário do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] , veja [Inscrever uma instância do SQL Server &#40;Utilitário do SQL Server&#41;](../relational-databases/manage/enroll-an-instance-of-sql-server-sql-server-utility.md).  
  
## <a name="uielement-list"></a>Lista de elementos de interface do usuário  
 Integridade de instância gerenciada  
 O status de integridade para instâncias gerenciadas do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] é exibido no lado esquerdo do painel de conteúdo do Gerenciador do Utilitário.  
  
 Estes são os parâmetros de integridade de instância gerenciada:  
  
-   Utilização da CPU para a instância do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
-   Utilização do arquivo de banco de dados.  
  
-   Utilização de espaço do volume de armazenamento.  
  
-   Utilização da CPU para o computador.  
  
-   O status para cada parâmetro é dividido em três categorias:  
  
-   Bem-utilizado - Número de instâncias gerenciadas do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] que não estão violando políticas de utilização de recursos.  
  
-   Subutilizado - Número de recursos gerenciados do que estão violando políticas de subutilização de recursos.  
  
-   Superutilizado - Número de recursos gerenciados do que estão violando políticas de superutilização de recursos.  
  
-   Nenhum Dado Disponível - Dados não estão disponíveis para instâncias gerenciadas do SQL Server porque a instância do SQL Server acabou de ser inscrita e a primeira operação de coleta de dados não foi concluída, ou porque há um problema com a instância gerenciada do SQL Server na coleta e no carregamento de dados na UCP.  
  
 O status detalhado para cada parâmetro de integridade é listado em indicadores deslizantes. A fração à direita dos indicadores deslizantes mostra a quantidade de instâncias gerenciadas em cada categoria de status.  
  
 Para criar uma exibição filtrada de uma instância gerenciada do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] ou um aplicativo de camada de dados, clique no link para obter uma categoria de utilização ao lado do indicador deslizante no painel do Utility. Por exemplo, se você clicar em **CPU de Instância Superutilizada** no painel **Conteúdo do Gerenciador do Utilitário** , o SSMS criará uma exibição de lista filtrada das instâncias gerenciadas do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] que têm a CPU superutilizada com base nas configurações de política atuais.  
  
 Observe que, quando você clicar em um link para uma categoria de utilização, o nó correspondente no painel de navegação do Gerenciador do Utilitário será acrescentado com **(filtrado)** – ou seja, **Instâncias Gerenciadas** é rotulado **Instâncias Gerenciadas (filtrado)**. Para exibir as configurações de filtro, clique com o botão direito do mouse no nó do painel de navegação, selecione **Filtrar**e clique em **Configurações de Filtro**. Para limpar as configurações de filtro, clique com o botão direito do mouse no nó do painel de navegação, selecione **Filtrar** e clique em **Remover Filtro**.  
  
 Para obter mais informações sobre como exibir o status de integridade de instâncias individuais do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], ou para exibir ou alterar definições de configuração de política, veja [Detalhes de instâncias gerenciadas &#40;Utilitário do SQL Server&#41;](../../2014/database-engine/managed-instance-details-sql-server-utility.md).  
  
 Resumo do Utility  
 Exibe o número de instâncias gerenciadas do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] e o número de aplicativos da camada de dados gerenciados pelo [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Utility.  
  
 Integridade do Aplicativo da Camada de Dados  
 O status de integridade de aplicativos da camada de dados é exibido no lado direito do painel de conteúdo do Gerenciador do Utilitário.  
  
 Estes são os parâmetros de Integridade do Aplicativo da Camada de Dados:  
  
-   Utilização da CPU para a instância do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
-   Utilização do arquivo de banco de dados.  
  
-   Utilização de espaço do volume de armazenamento.  
  
-   Utilização da CPU para o computador.  
  
 O status para cada parâmetro é dividido em três categorias:  
  
-   Bem-utilizado - Número de aplicativos da camada de dados que não estão violando políticas de utilização de recursos.  
  
-   Superutilizado - Número de aplicativos da camada de dados que estão violando políticas de superutilização de recursos.  
  
-   Subutilizado - Número de aplicativos da camada de dados que estão violando políticas de subutilização de recursos.  
  
-   Nenhum Dado Disponível - Dados não estão disponíveis para aplicativos de camada de dados porque a instância gerenciada do SQL Server que contém o aplicativo da camada de dados não está relatando dados.  
  
 O status detalhado para cada parâmetro de integridade é listado em indicadores deslizantes. A fração à direita dos indicadores deslizantes mostra a quantidade de aplicativos da camada de dados em cada categoria de status. Para obter mais informações sobre como exibir o status de integridade de aplicativos individuais da camada de dados, ou para exibir ou alterar definições de configuração de política, veja [Detalhes do aplicativo da camada de dados implantado &#40;Utilitário do SQL Server&#41;](../../2014/database-engine/deployed-data-tier-application-details-sql-server-utility.md).  
  
 Histórico de utilização de armazenamento do Utility  
 O histórico de utilização é mostrado em um gráfico de tempo na parte inferior do painel do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Utility. Observe que os dados de tempo mostram a data e hora locais do UCP usando o tipo de dados datetime. Para obter mais informações, veja o tópico [datetime (Transact-SQL)](https://go.microsoft.com/fwlink/?LinkId=164071) nos Manuais Online do SQL Server. Ao usar o modelo de objeto do Utilitário, observe que o SSMS usa o tipo de dados datetimeoffset. Para obter mais informações, veja o tópico [datetimeoffset (Transact-SQL)](https://go.microsoft.com/fwlink/?LinkId=141713) nos Manuais Online do SQL Server.  
  
 Use os botões de opção à esquerda da área de exibição para alterar o período de relatório do gráfico.  
  
 Estas são as opções para o intervalo de relatórios:  
  
-   1 Dia, exibido em intervalos de 15 minutos.  
  
-   1 Semana, exibido em intervalos de 1 dia.  
  
-   1 Mês, exibido em intervalos de 1 semana.  
  
-   1 Ano, exibido em intervalos de 1 mês.  
  
 Depois que você faz uma alteração no intervalo de relatórios, os dados são atualizados automaticamente.  
  
 Utilização de armazenamento do Utilitário  
 No lado direito inferior do painel, o gráfico de pizza de utilização de armazenamento exibe a taxa de espaço utilizado para liberar espaço em volumes que residem em computadores contendo instâncias gerenciadas do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Os dados desta exibição são atualizados a cada 15 minutos.  
  
## <a name="see-also"></a>Consulte Também  
 [Usar o Gerenciador do Utilitário para gerenciar o Utilitário do SQL Server](../relational-databases/manage/use-utility-explorer-to-manage-the-sql-server-utility.md)   
 [Inscrever uma instância do SQL Server &#40;Utilitário do SQL Server&#41;](../relational-databases/manage/enroll-an-instance-of-sql-server-sql-server-utility.md)   
 [Modificar uma definição de política de integridade de recursos &#40;Utilitário do SQL Server&#41;](../relational-databases/manage/modify-a-resource-health-policy-definition-sql-server-utility.md)  
  
  
