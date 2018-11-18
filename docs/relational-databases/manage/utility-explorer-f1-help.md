---
title: Ajuda F1 do Gerenciador do Utilitário | Microsoft Docs
ms.custom: ''
ms.date: 08/19/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: configuration
ms.topic: reference
f1_keywords:
- sql13.swb.ue.navigation.f1
- sql13.SWB.UE.dac.details.F1
- sql13.SQB.UE.dac.details.F1
- utility details
helpviewer_keywords:
- Utility
- management
- data-tier application
ms.assetid: 8697e4a4-4f59-4cda-af71-7de86005bd4a
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 84db1d36a782fc054129b1ff753b620e82684499
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/15/2018
ms.locfileid: "51675365"
---
# <a name="utility-explorer-f1-help"></a>Ajuda de F1 do Gerenciador do Utilitário
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  As seções a seguir documentam a funcionalidade do Utilitário do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e as operações associadas.  
  
  ## <a name="utility-dashboard-sql-server-utility"></a>Painel do Utilitário (Utilitário do SQL Server)
 Para consultar dados no painel do Utilitário do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], selecione o nó superior na árvore do Gerenciador do Utilitário, identificado como “Utility<UCP_Name>\\(ComputerName\UCP).” O painel inclui dados resumidos e dados detalhados de todas as instâncias gerenciadas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e todos os aplicativos da camada de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Utility. Para atualizar dados no painel, clique com o botão direito do mouse no nó superior da árvore do Gerenciador do Utilitário e selecione **Atualizar**.  
  
 Para obter mais informações sobre como criar um ponto de controle do utilitário, veja [Criar um ponto de controle do Utilitário do SQL Server &#40;Utilitário do SQL Server&#41;](../../relational-databases/manage/create-a-sql-server-utility-control-point-sql-server-utility.md). Para obter mais informações sobre como adicionar uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ao Utilitário do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , veja [Inscrever uma instância do SQL Server &#40;Utilitário do SQL Server&#41;](../../relational-databases/manage/enroll-an-instance-of-sql-server-sql-server-utility.md).  
 
  
### <a name="uielement-list"></a>Lista de elementos de interface do usuário  
 Integridade de instância gerenciada  
 O status de integridade para instâncias gerenciadas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é exibido no lado esquerdo do painel de conteúdo do Gerenciador do Utilitário.  
  
 Estes são os parâmetros de integridade de instância gerenciada:  
  
-   Utilização da CPU para a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   Utilização do arquivo de banco de dados.  
  
-   Utilização de espaço do volume de armazenamento.  
  
-   Utilização da CPU para o computador.  
  
-   O status para cada parâmetro é dividido em três categorias:  
  
-   Bem-utilizado - Número de instâncias gerenciadas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que não estão violando políticas de utilização de recursos.  
  
-   Subutilizado - Número de recursos gerenciados do que estão violando políticas de subutilização de recursos.  
  
-   Superutilizado - Número de recursos gerenciados do que estão violando políticas de superutilização de recursos.  
  
-   Nenhum Dado Disponível - Dados não estão disponíveis para instâncias gerenciadas do SQL Server porque a instância do SQL Server acabou de ser inscrita e a primeira operação de coleta de dados não foi concluída, ou porque há um problema com a instância gerenciada do SQL Server na coleta e no carregamento de dados na UCP.  
  
 O status detalhado para cada parâmetro de integridade é listado em indicadores deslizantes. A fração à direita dos indicadores deslizantes mostra a quantidade de instâncias gerenciadas em cada categoria de status.  
  
 Para criar uma exibição filtrada de uma instância gerenciada do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou um aplicativo de camada de dados, clique no link para obter uma categoria de utilização ao lado do indicador deslizante no painel do Utility. Por exemplo, se você clicar em **CPU de Instância Superutilizada** no painel **Conteúdo do Gerenciador do Utilitário** , o SSMS criará uma exibição de lista filtrada das instâncias gerenciadas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que têm a CPU superutilizada com base nas configurações de política atuais.  
  
 Observe que, quando você clicar em um link para uma categoria de utilização, o nó correspondente no painel de navegação do Gerenciador do Utilitário será acrescentado com **(filtrado)** – ou seja, **Instâncias Gerenciadas** é rotulado **Instâncias Gerenciadas (filtrado)**. Para exibir as configurações de filtro, clique com o botão direito do mouse no nó do painel de navegação, selecione **Filtrar**e clique em **Configurações de Filtro**. Para limpar as configurações de filtro, clique com o botão direito do mouse no nó do painel de navegação, selecione **Filtrar** e clique em **Remover Filtro**.  
  
 Para obter mais informações sobre como exibir o status de integridade de instâncias individuais do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], ou para exibir ou alterar definições de configuração de política, veja [Detalhes de instâncias gerenciadas &#40;Utilitário do SQL Server&#41;](https://msdn.microsoft.com/library/6e51b7bb-a733-4852-8c33-7f4dbdf931c2).  
  
 Resumo do Utility  
 Exibe o número de instâncias gerenciadas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e o número de aplicativos da camada de dados gerenciados pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Utility.  
  
 Integridade do Aplicativo da Camada de Dados  
 O status de integridade de aplicativos da camada de dados é exibido no lado direito do painel de conteúdo do Gerenciador do Utilitário.  
  
 Estes são os parâmetros de Integridade do Aplicativo da Camada de Dados:  
  
-   Utilização da CPU para a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   Utilização do arquivo de banco de dados.  
  
-   Utilização de espaço do volume de armazenamento.  
  
-   Utilização da CPU para o computador.  
  
 O status para cada parâmetro é dividido em três categorias:  
  
-   Bem-utilizado - Número de aplicativos da camada de dados que não estão violando políticas de utilização de recursos.  
  
-   Superutilizado - Número de aplicativos da camada de dados que estão violando políticas de superutilização de recursos.  
  
-   Subutilizado - Número de aplicativos da camada de dados que estão violando políticas de subutilização de recursos.  
  
-   Nenhum Dado Disponível - Dados não estão disponíveis para aplicativos de camada de dados porque a instância gerenciada do SQL Server que contém o aplicativo da camada de dados não está relatando dados.  
  
 O status detalhado para cada parâmetro de integridade é listado em indicadores deslizantes. A fração à direita dos indicadores deslizantes mostra a quantidade de aplicativos da camada de dados em cada categoria de status. Para obter mais informações sobre como exibir o status de integridade de aplicativos individuais da camada de dados, ou para exibir ou alterar definições de configuração de política, veja [Detalhes do aplicativo da camada de dados implantado &#40;Utilitário do SQL Server&#41;](https://msdn.microsoft.com/library/79c41dd9-abcb-434e-9326-00a341d5c867).  
  
 Histórico de utilização de armazenamento do Utility  
 O histórico de utilização é mostrado em um gráfico de tempo na parte inferior do painel do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Utility. Observe que os dados de tempo mostram a data e hora locais do UCP usando o tipo de dados datetime. Para obter mais informações, consulte o tópico [datetime (Transact-SQL)](https://go.microsoft.com/fwlink/?LinkId=164071) . Ao usar o modelo de objeto do Utilitário, observe que o SSMS usa o tipo de dados datetimeoffset. Para obter mais informações, consulte o tópico [datetimeoffset (Transact-SQL)](https://go.microsoft.com/fwlink/?LinkId=141713) .  
  
 Use os botões de opção à esquerda da área de exibição para alterar o período de relatório do gráfico.  
  
 Estas são as opções para o intervalo de relatórios:  
  
-   1 Dia, exibido em intervalos de 15 minutos.  
  
-   1 Semana, exibido em intervalos de 1 dia.  
  
-   1 Mês, exibido em intervalos de 1 semana.  
  
-   1 Ano, exibido em intervalos de 1 mês.  
  
 Depois que você faz uma alteração no intervalo de relatórios, os dados são atualizados automaticamente.  
  
 Utilização de armazenamento do Utilitário  
 No lado direito inferior do painel, o gráfico de pizza de utilização de armazenamento exibe a taxa de espaço utilizado para liberar espaço em volumes que residem em computadores contendo instâncias gerenciadas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Os dados desta exibição são atualizados a cada 15 minutos.  
 
 ## <a name="deployed-data-tier-application-details-sql-server-utility"></a>Detalhes do aplicativo da camada de dados implantado (Utilitário do SQL Server)
  As informações da exibição Aplicativos da Camada de Dados Implantados do Gerenciador do Utilitário fornecem dados de utilização para aplicativos da camada de dados individuais, o histórico de utilização da CPU, detalhes de utilização do armazenamento em nível de arquivo e a capacidade de exibir e atualizar limites de políticas. Os limites de políticas podem ser controlados no nível de aplicativo da camada de dados para utilização da CPU e para arquivos de log e arquivos de dados do banco de dados. Você também pode exibir detalhes de propriedades de aplicativos da camada de dados individuais.  
  
### <a name="uielement-list"></a>Lista de elementos de interface do usuário  
 Exibição de lista  
 A exibição de lista no painel superior exibe dados sobre aplicativos da camada de dados individuais. Os ícones do estado de integridade fornecem o status resumido de cada aplicativo da camada de dados por categoria de utilização:  
  
-   Marca de verificação verde – ![](../../relational-databases/manage/media/well-utilized.gif "Well_utilized") – Número de aplicativos da camada de dados que não estão violando políticas de utilização de recursos. Os recursos estão bem-utilizados.  
  
-   Seta para baixo verde – ![](../../relational-databases/manage/media/utility-down-arrow.gif "Utility_down_arrow") – Os recursos estão subutilizados.  
  
-   Seta para cima vermelha – ![](../../relational-databases/manage/media/utility-up-arrow.gif "Utility_up_arrow") – Os recursos estão superutilizados.  
  
 A sequência de colunas da exibição de lista pode ser alterada arrastando-se as colunas para a esquerda ou para a direita. Para adicionar ou excluir colunas da exibição de lista, clique com o botão direito do mouse nos títulos das colunas e selecione ou desmarque colunas. O menu de atalho também fornece opções de classificação. A classificação também pode ser ativada clicando-se na parte superior do nome de uma coluna.  
  
 Para acessar as opções de filtro da exibição de lista do Utilitário do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , clique com o botão direito do mouse no nó **Aplicativos da Camada de Dados Implantados** no painel de navegação do Gerenciador do Utilitário e selecione **Filtrar**. Depois que as configurações de filtro forem implementadas, o nó **Aplicativos da Camada de Dados Implantados** no Gerenciador do Utilitário será rotulado **Aplicativos da Camada de Dados Implantados (filtrados)**. Para obter mais informações, consulte [Configurações de filtro &#40;Pesquisador de Objetos e Gerenciador do Utilitário&#41;](https://msdn.microsoft.com/library/4aab04bc-e1ab-4d4b-ab74-b287fc805bc2).  
  
 Por padrão, as colunas a seguir exibem informações do estado de integridade de cada aplicativo da camada de dados.  
  
-   Nome - O nome do aplicativo da camada de dados.  
  
-   CPU do Aplicativo - Exibe o estado de integridade de utilização de processador para este aplicativo da camada de dados. O estado de integridade desse parâmetro é determinado de acordo com a política de utilização da CPU definida para o aplicativo da camada de dados e o parâmetro de configuração da política de avaliação de recurso volátil. Para obter mais informações, veja [Reduzir o ruído em políticas de utilização da CPU &#40;Utilitário do SQL Server&#41;](../../relational-databases/manage/reduce-noise-in-cpu-utilization-policies-sql-server-utility.md).  
  
     Para exibir o histórico de utilização do processador desse aplicativo da camada de dados ou para exibir ou alterar os limites da política, clique na guia **Utilização da CPU**.  
  
-   CPU do Computador - Exibe o estado de integridade da utilização do processador do computador. O estado de integridade deste parâmetro é determinado de acordo com a política de utilização da CPU definida para o computador e o parâmetro de configuração da política de avaliação de recurso volátil. Para obter mais informações, veja [Reduzir o ruído em políticas de utilização da CPU &#40;Utilitário do SQL Server&#41;](../../relational-databases/manage/reduce-noise-in-cpu-utilization-policies-sql-server-utility.md).  
  
     Para exibir o histórico de utilização do processador desse aplicativo da camada de dados ou para exibir ou alterar os limites da política, clique na guia **Utilização da CPU**.  
  
-   Espaço para Arquivo - Exibe um resumo de estados de integridade de utilização de espaço para arquivo para cada aplicativo da camada de dados.  
  
    -   Verificação verde - Os estados de integridade de todos os grupos de arquivos e grupos de arquivos de log não são superutilizados nem subutilizados.  
  
    -   Seta para baixo verde - O estado de integridade de pelo menos um grupo de arquivos ou grupo de arquivos de log é subutilizado, e nenhum deles é superutilizado.  
  
    -   Seta para cima vermelha - O estado de integridade de pelo menos um grupo de arquivos ou grupo de arquivos de log é superutilizado. Note que, se um banco de dados estiver no estado de "emergência", o estado de integridade exibirá o espaço de arquivo de log superutilizado.  
  
     Para exibir ou alterar os limites da política de espaço para arquivo, clique na guia **Utilização do Armazenamento** .  
  
-   Espaço no Volume - Exibe um resumo dos estados da integridade da utilização do espaço para todos os volumes que contenham bancos de dados pertencentes ao aplicativo da camada de dados selecionado. Se o estado de integridade de qualquer volume for superutilizado, a integridade do espaço no volume será relatada na exibição de lista como superutilizada. Se o estado de integridade de qualquer volume for subutilizado e nenhum volume for superutilizado, a integridade do espaço de volume será relatada na exibição de lista como subutilizada. Caso contrário, o estado da integridade do espaço de volume será relatado na exibição de lista como bem-utilizado. Para exibir ou alterar os limites da política, clique na guia **Utilização de Armazenamento** .  
  
-   Tipo de Política - Indica se as políticas padrão "Globais" ou as políticas personalizadas de "Substituição" estão em vigor para o aplicativo da camada de dados.  
  
-   Nome da Instância - Exibe o nome da instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que hospeda o aplicativo da camada de dados.  
  
 Outras colunas que podem ser exibidas com o menu de atalho na área de título de coluna da exibição de lista:  
  
-   Nome do Banco de Dados  
  
-   Data de Implantação  
  
-   Confiável: (True ou False)  
  
-   Ordenação  
  
-   Nível de Compatibilidade: (por exemplo, Version100)  
  
-   Criptografia Habilitada: (True ou False)  
  
-   Modelo de Recuperação: (Simples, Completa e Bulk-logged)  
  
-   Hora do Último Relatório: esta coluna mostra a data e hora local do UCP usando o tipo de dados datetime. Para obter mais informações, consulte o tópico [datetime (Transact-SQL)](https://go.microsoft.com/fwlink/?LinkId=164071) . Ao usar o modelo de objeto do Utilitário, observe que o SSMS usa o tipo de dados datetimeoffset. Para obter mais informações, consulte o tópico [datetimeoffset (Transact-SQL)](https://go.microsoft.com/fwlink/?LinkId=141713) .  
  
 Guia Utilização da CPU  
 A guia Utilização da CPU mostra gráficos lado a lado de dados históricos da utilização de CPU do computador e do aplicativo da camada de dados.  
  
 O gráfico exibe o histórico de utilização do processador para o intervalo especificado nos botões de opção à direita da área de exibição. Para alterar o intervalo de exibição e atualizar o conjunto de dados, selecione um botão de opção na lista.  
  
 As opções de intervalo são as seguintes:  
  
-   1 Dia, exibido em intervalos de 15 minutos.  
  
-   1 Semana, exibido em intervalos de 1 dia.  
  
-   1 Mês, exibido em intervalos de 1 semana.  
  
-   1 Ano, exibido em intervalos de 1 mês.  
  
 Guia Utilização de Armazenamento  
 A guia de Utilização do Armazenamento tem uma exibição de árvore que exibe detalhes de utilização de armazenamento para arquivos de banco de dados e arquivos de log que pertencem ao aplicativo da camada de dados selecionado na exibição de lista. Observe que os dados de tempo mostram a data e hora locais do UCP usando o tipo de dados datetime. Para obter mais informações, consulte o tópico [datetime (Transact-SQL)](https://go.microsoft.com/fwlink/?LinkId=164071) . Ao usar o modelo de objeto do Utilitário, observe que o SSMS usa o tipo de dados datetimeoffset. Para obter mais informações, consulte o tópico [datetimeoffset (Transact-SQL)](https://go.microsoft.com/fwlink/?LinkId=141713) .  
  
 A exibição pode ser agrupada por grupo de arquivos ou por volume. Para usar a exibição de árvore do grupo de arquivos, selecione o botão de opção **Grupo de arquivos** na seleção **Agrupar arquivos por:** .  
  
 Os dados exibidos no gráfico de histórico de utilização de armazenamento são alterados de acordo com o nó selecionado na exibição de árvore:  
  
-   Selecione o nó do grupo de arquivos para exibir um gráfico do espaço de arquivo usado por todos os arquivos de dados pertencentes ao grupo de arquivos selecionado.  
  
-   Selecione o nó de arquivos de log para exibir um gráfico do espaço de arquivo usado por todos os arquivos de log pertencentes ao banco de dados selecionado.  
  
-   Selecione o nó de banco de dados para exibir um gráfico que adiciona o espaço para arquivo usado por todos os arquivos de dados e de log pertencentes ao banco de dados selecionado.  
  
 Para exibir o status da utilização do armazenamento para arquivos individuais, clique no sinal de adição ao lado do nome de arquivo na exibição de árvore.  
  
 Os ícones de estado de integridade exibem o status de cada grupo de arquivos comparado a limites de política:  
  
-   Marca de verificação verde - A utilização de espaço para arquivo para pelo menos um arquivo de dados no grupo de arquivos não é superutilizada nem subutilizada.  
  
-   Seta para baixo verde - A utilização do espaço para arquivo de pelo menos um arquivo de dados no grupo de arquivos é subutilizada, e nenhum arquivo do grupo de arquivos é superutilizado.  
  
-   Seta para cima verde - A utilização de espaço de arquivo de todos os arquivos de dados do grupo de arquivos está superutilizada. Note que, se um banco de dados estiver no estado de "emergência", o estado de integridade exibirá o espaço de arquivo de log superutilizado.  
  
 Para exibir arquivos por volume, selecione o botão de opção **Volume** na seleção **Agrupar arquivos por:** . O gráfico de histórico de utilização de armazenamento exibe o espaço de arquivo usado por todos os arquivos de dados e de log no volume de armazenamento. Expanda a árvore para exibir detalhes de arquivos de dados e de log individuais do banco de dados.  
  
 Ícones de status são usados para fornecer o status de cada volume:  
  
-   Verificação verde - Os recursos estão bem-utilizados.  
  
-   Seta para baixo verde - Os recursos estão subutilizados.  
  
-   Seta para cima vermelha - Os recursos estão superutilizados.  
  
 O medidor ao lado de cada nome de arquivo na guia de Utilização de Armazenamento representa a quantidade de espaço usada pelo arquivo relativa à capacidade efetiva do arquivo. O valor percentual exibido ao lado do medidor é a taxa da quantidade de espaço usada pelo arquivo relativa à capacidade efetiva do arquivo. As dicas de ferramenta fornecem os dados usados para calcular os percentuais de cada volume e de cada arquivo comparados com a capacidade efetiva.  
  
 Se o arquivo não estiver configurado para crescimento automático, a capacidade efetiva será a quantidade de espaço alocada ao arquivo. Se o arquivo estiver configurado para crescimento automático, a capacidade efetiva será a soma da quantidade de espaço alocada atualmente ao arquivo e a quantidade de espaço livre disponível no volume.  
  
 Políticas de armazenamento podem ser configuradas para arquivos de dados e de log. Para exibir ou alterar os limites da política de utilização de armazenamento de arquivos, clique no link **Política de Arquivo** na parte inferior do painel Utilização de Armazenamento. Para exibir ou alterar os limites da política de utilização de armazenamento de um volume de armazenamento, clique no link **Política de Volume** na parte inferior do painel Utilização de Armazenamento.  
  
 Para substituir os limites da política padrão, clique no botão de opção **Substituir a política padrão**, especifique valores para os limites superior e inferior e clique em **OK**.  
  
 Para obter mais informações sobre como alterar a tolerância para violações da política, consulte [Reduzir o ruído em políticas de utilização da CPU &#40;Utilitário do SQL Server&#41;](../../relational-databases/manage/reduce-noise-in-cpu-utilization-policies-sql-server-utility.md).  
  
 Guia Detalhes da Propriedade  
 Os detalhes da propriedade listados para aplicativos da camada de dados incluem as seguintes categorias:  
  
-   Nome do Banco de Dados  
  
-   Data de Implantação  
  
-   Confiável: (True ou False)  
  
-   Ordenação  
  
-   Nível de Compatibilidade: (por exemplo, Version100)  
  
-   Criptografia Habilitada: (True ou False)  
  
-   Modelo de Recuperação: (Simples, Completa e Bulk-logged)  
  
-   Hora do Último Relatório: esta coluna mostra a data e hora local do UCP usando o tipo de dados datetime. Para obter mais informações, consulte o tópico [datetime (Transact-SQL)](https://go.microsoft.com/fwlink/?LinkId=164071) . Ao usar o modelo de objeto do Utilitário, observe que o SSMS usa o tipo de dados datetimeoffset. Para obter mais informações, consulte o tópico [datetimeoffset (Transact-SQL)](https://go.microsoft.com/fwlink/?LinkId=141713) .

## <a name="managed-instance-details-sql-server-utility"></a>Detalhes de instâncias gerenciadas (Utilitário do SQL Server)
 As informações da exibição Instâncias Gerenciadas do Gerenciador do Utilitário fornecem dados de utilização para instâncias individuais do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], histórico de utilização da CPU, detalhes de utilização do armazenamento em nível de arquivo e a capacidade de exibir e atualizar limites de políticas. Os limites de políticas podem ser controlados no nível de instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , para um computador, para arquivos de banco de dados e arquivos de log e no nível de volumes de armazenamento. Você também pode exibir detalhes de propriedades de instâncias gerenciadas individuais do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
### <a name="uielement-list"></a>Lista de elementos de interface do usuário  
 Exibição de lista  
 A exibição de lista no painel superior exibe dados sobre instâncias individuais do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] listadas em linhas por ComputerName\InstanceName.  
  
 Os ícones do estado de integridade fornecem o status resumido de cada instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] por categoria de utilização:  
  
-   Marca de verificação verde – ![](../../relational-databases/manage/media/well-utilized.gif "Well_utilized") – Número de instâncias gerenciadas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que não estão violando políticas de utilização de recursos. Os recursos estão bem-utilizados.  
  
-   Seta para baixo verde – ![](../../relational-databases/manage/media/utility-down-arrow.gif "Utility_down_arrow") – Os recursos estão subutilizados.  
  
-   Seta para cima vermelha – ![](../../relational-databases/manage/media/utility-up-arrow.gif "Utility_up_arrow") – Os recursos estão superutilizados.  
  
 A sequência de colunas da exibição de lista pode ser alterada arrastando-se as colunas para a esquerda ou para a direita. Para adicionar ou excluir colunas da exibição de lista, clique com o botão direito do mouse nos títulos das colunas e selecione ou desmarque colunas. O menu de atalho também fornece opções de classificação. A classificação também pode ser ativada clicando-se na parte superior do nome de uma coluna.  
  
 Para acessar as opções de filtro da exibição de lista do Utilitário, clique com o botão direito do mouse no nó **Instâncias Gerenciadas** no painel de navegação do Gerenciador do Utilitário e selecione **Filtrar**. Depois que as configurações de filtro forem implementadas, o nó **Instâncias Gerenciadas** no Gerenciador do Utilitário será rotulado **Instâncias Gerenciadas (filtradas)**. Para obter mais informações, consulte [Configurações de filtro &#40;Pesquisador de Objetos e Gerenciador do Utilitário&#41;](https://msdn.microsoft.com/library/4aab04bc-e1ab-4d4b-ab74-b287fc805bc2).  
  
 Por padrão, as colunas a seguir exibem informações do estado de integridade de cada instância gerenciada do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   CPU da Instância – Exibe o estado de integridade da utilização do processador alocado a essa instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. O estado de integridade deste parâmetro é determinado de acordo com a política de utilização da CPU definida para a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e o parâmetro de configuração da política de avaliação de recurso volátil. Para obter mais informações, veja [Reduzir o ruído em políticas de utilização da CPU &#40;Utilitário do SQL Server&#41;](../../relational-databases/manage/reduce-noise-in-cpu-utilization-policies-sql-server-utility.md).  
  
     Para exibir o histórico da utilização do processador para essa instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]ou para exibir ou alterar os limites da política, clique na guia **Utilização da CPU** .  
  
-   CPU do Computador - Exibe o estado de integridade da utilização do processador do computador. O estado de integridade deste parâmetro é determinado de acordo com a política de utilização da CPU definida para o computador e o parâmetro de configuração da política de avaliação de recurso volátil. Para obter mais informações, veja [Reduzir o ruído em políticas de utilização da CPU &#40;Utilitário do SQL Server&#41;](../../relational-databases/manage/reduce-noise-in-cpu-utilization-policies-sql-server-utility.md).  
  
     Para exibir o histórico da utilização do processador para essa instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]ou para exibir ou alterar os limites da política, clique na guia **Utilização da CPU** .  
  
-   Espaço de Arquivo – Exibe um resumo dos estados da integridade da utilização do espaço de arquivo de todos os bancos de dados que pertencem à instância selecionada do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Se o estado de integridade de qualquer arquivo do banco de dados for superutilizado, a integridade do espaço de arquivo será informada na exibição de lista como superutilizada. Se o estado de integridade de qualquer do banco de dados for subutilizado e nenhum banco de dados for superutilizado, a integridade do espaço de arquivo será relatada na exibição de lista como subutilizada. Caso contrário, o estado da integridade do espaço de arquivo será relatado na exibição de lista como bem-utilizado. Para exibir ou alterar os limites da política, clique na guia **Utilização de Armazenamento** .  
  
-   Espaço de Volume - Exibe um resumo dos estados da integridade da utilização do espaço de volume de todos os volumes que contêm bancos de dados pertencentes à instância selecionada do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Se o estado de integridade de qualquer volume for superutilizado, a integridade do espaço no volume será relatada na exibição de lista como superutilizada. Se o estado de integridade de qualquer volume for subutilizado e nenhum volume for superutilizado, a integridade do espaço de volume será relatada na exibição de lista como subutilizada. Caso contrário, o estado da integridade do espaço de volume será relatado na exibição de lista como bem-utilizado. Para exibir ou alterar os limites da política, clique na guia **Utilização de Armazenamento** .  
  
-   Tipo de Política - Indica se as políticas padrão "Globais" ou as políticas personalizadas de "Substituição" estão em vigor para a instância gerenciada do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Outras colunas que podem ser exibidas com o menu de atalho na área de título de coluna da exibição de lista:  
  
-   Nome do Processador:  
  
-   Velocidade do Processador (MHz):  
  
-   Contagem de Processadores:  
  
-   Memória Física (MB):  
  
-   Versão do Sistema Operacional:  
  
-   Versão do SQL Server:  
  
-   Edição do SQL Server:  
  
-   Clusterizado: (Verdadeiro ou Falso)  
  
-   Diretório de Backup:  
  
-   Ordenação:  
  
-   Diferenciar Maiúsculas de Minúsculas: (Verdadeiro ou Falso)  
  
-   Idioma:  
  
-   Hora do Último Relatório: esta coluna mostra a data e hora local do UCP usando o tipo de dados datetime. Para obter mais informações, consulte o tópico [datetime (Transact-SQL)](https://go.microsoft.com/fwlink/?LinkId=164071) . Ao usar o modelo de objeto do Utilitário, observe que o SSMS usa o tipo de dados datetimeoffset. Para obter mais informações, consulte o tópico [datetimeoffset (Transact-SQL)](https://go.microsoft.com/fwlink/?LinkId=141713) .  
  
 Guia Utilização da CPU  
 A guia Utilização da CPU mostra gráficos lado a lado de dados históricos da utilização da CPU do computador e da instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 O gráfico exibe o histórico de utilização do processador para o intervalo especificado nos botões de opção à direita da área de exibição. Para alterar o intervalo de exibição e atualizar o conjunto de dados, selecione um botão de opção na lista.  
  
 As opções de intervalo são as seguintes:  
  
-   1 Dia, exibido em intervalos de 15 minutos.  
  
-   1 Semana, exibido em intervalos de 1 dia.  
  
-   1 Mês, exibido em intervalos de 1 semana.  
  
-   1 Ano, exibido em intervalos de 1 mês.  
  
 Guia Utilização de Armazenamento  
 A guia Utilização de Armazenamento tem uma exibição de árvore que exibe detalhes da utilização do armazenamento. Observe que os dados de tempo mostram a data e hora locais do UCP usando o tipo de dados datetime. Para obter mais informações, consulte o tópico [datetime (Transact-SQL)](https://go.microsoft.com/fwlink/?LinkId=164071) . Ao usar o modelo de objeto do Utilitário, observe que o SSMS usa o tipo de dados datetimeoffset. Para obter mais informações, consulte o tópico [datetimeoffset (Transact-SQL)](https://go.microsoft.com/fwlink/?LinkId=141713) .  
  
 A exibição pode ser agrupada por banco de dados ou por volume. Para usar a exibição de árvore do banco de dados, selecione o botão de opção **Banco de dados** na seleção **Agrupar arquivos por:** . Para exibir o status da utilização do armazenamento de arquivos individuais do banco de dados, clique no sinal de adição ao lado do nome de um banco de dados na exibição de árvore. Os arquivos de banco de dados listados incluem todos os bancos de dados do sistema e de usuários que pertencem à instância gerenciada do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] selecionados na exibição de lista.  
  
 A estrutura de árvore corresponde à hierarquia de armazenamento. O nó raiz da árvore de exibição é o banco de dados. O próximo nível da exibição de árvore contém um nó de grupo de arquivos ou nós pertencentes ao banco de dados e um nó de arquivos de log pertencentes ao banco de dados. O próximo nível contém os arquivos de dados pertencentes ao grupo de arquivos.  
  
 Os dados exibidos no gráfico de histórico de utilização de armazenamento são alterados de acordo com o nó selecionado na exibição de árvore:  
  
-   Selecione o nó do grupo de arquivos para exibir um gráfico do espaço de arquivo usado por todos os arquivos de dados pertencentes ao grupo de arquivos selecionado.  
  
-   Selecione o nó de arquivos de log para exibir um gráfico do espaço de arquivo usado por todos os arquivos de log pertencentes ao banco de dados selecionado.  
  
-   Selecione o nó de banco de dados para exibir um gráfico que adiciona o espaço para arquivo usado por todos os arquivos de dados e de log pertencentes ao banco de dados selecionado.  
  
 Os ícones de estado de integridade fornecem um status de um relance dos arquivos de banco de dados, dos grupos de arquivos e dos arquivos de log:  
  
 Para bancos de dados:  
  
-   Verificação Verde - os estados de integridade de todos os grupos de arquivos e arquivos de log não são superutilizados ou subutilizados.  
  
-   Seta para baixo verde - O estado de integridade de pelo menos um grupo de arquivos ou arquivo de log é subutilizado e nenhum estado de integridade é superutilizado.  
  
-   Seta para cima vermelha - O estado de integridade de pelo menos um grupo de arquivos ou arquivo de log é superutilizado.  
  
 Para grupos de arquivos e arquivos de log:  
  
-   Verificação Verde - A utilização de espaço de arquivo de todos os arquivos do grupo de arquivos não é superutilizada ou subutilizada.  
  
-   Seta para baixo Verde - A utilização do espaço de arquivo de pelo menos um arquivo do grupo de arquivos é subutilizada e nenhum arquivo do grupo de arquivos está superutilizado.  
  
-   Seta para cima verde - A utilização de espaço de arquivo de todos os arquivos de dados do grupo de arquivos está superutilizada.  
  
 Para exibir arquivos por volume, selecione o botão de opção **Volume** na seleção **Agrupar arquivos por:** . O gráfico de histórico de utilização de armazenamento exibe o espaço de arquivo usado por todos os arquivos de dados e de log no volume de armazenamento. Expanda a árvore para exibir detalhes de arquivos de dados e de log individuais do banco de dados.  
  
 Ícones de status são usados para fornecer o status de cada volume:  
  
-   Verificação verde - Os recursos estão bem-utilizados.  
  
-   Seta para baixo verde - Os recursos estão subutilizados.  
  
-   Seta para cima vermelha - Os recursos estão superutilizados.  
  
 O medidor ao lado de cada nome de arquivo na guia de Utilização de Armazenamento representa a quantidade de espaço usada pelo arquivo relativa à capacidade efetiva do arquivo. O valor percentual exibido ao lado do medidor é a taxa da quantidade de espaço usada pelo arquivo relativa à capacidade efetiva do arquivo. As dicas de ferramenta fornecem os dados usados para calcular os percentuais de cada volume e de cada arquivo comparados com a capacidade efetiva.  
  
 Se o arquivo não estiver configurado para crescimento automático, a capacidade efetiva será a quantidade de espaço alocada ao arquivo. Se o arquivo estiver configurado para crescimento automático, a capacidade efetiva será a soma da quantidade de espaço alocada atualmente ao arquivo e a quantidade de espaço livre disponível no volume.  
  
 Políticas de armazenamento podem ser configuradas para arquivos de dados e de log. Para exibir ou alterar os limites da política de utilização de armazenamento de arquivos, clique no link **Política de Arquivo** na parte inferior do painel Utilização de Armazenamento. Para exibir ou alterar os limites da política de utilização de armazenamento de um volume de armazenamento, clique no link **Política de Volume** na parte inferior do painel Utilização de Armazenamento.  
  
 Para substituir os limites da política padrão, clique no botão de opção **Substituir a política padrão**, especifique valores para os limites superior e inferior e clique em **OK**.  
  
 Para obter mais informações sobre como alterar a tolerância para violações da política, consulte [Reduzir o ruído em políticas de utilização da CPU &#40;Utilitário do SQL Server&#41;](../../relational-databases/manage/reduce-noise-in-cpu-utilization-policies-sql-server-utility.md).  
  
 Guia Detalhes da Propriedade  
 Os detalhes da propriedade listados para instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] incluem as seguintes categorias:  
  
-   Nome do Processador:  
  
-   Velocidade do Processador (MHz):  
  
-   Contagem de Processadores:  
  
-   Memória Física (MB):  
  
-   Versão do Sistema Operacional:  
  
-   Versão do SQL Server:  
  
-   Edição do SQL Server:  
  
-   Clusterizado: (Verdadeiro ou Falso)  
  
-   Diretório de Backup:  
  
-   Ordenação:  
  
-   Diferenciar Maiúsculas de Minúsculas: (Verdadeiro ou Falso)  
  
-   Idioma:  

## <a name="utility-administration-sql-server-utility"></a>Administração do Utilitário (Utilitário do SQL Server)
Use as guias de Administração do Utilitário para gerenciar configurações de políticas, segurança e data warehouse para um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Utility. Para obter mais informações sobre os conceitos do Utilitário do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , veja [Recursos e tarefas do Utilitário do SQL Server](../../relational-databases/manage/sql-server-utility-features-and-tasks.md).  
  
### <a name="uielement-list"></a>Lista de elementos de interface do usuário
 **Guia Política** – Use a guia Política para exibir ou especificar políticas de monitoramento globais.  
  
 Definir políticas de monitoramento de aplicativo da camada de dados. Para expandir a lista de valores dessa opção, clique na seta ao lado do nome da política ou clique no título da política.  
 Quando um aplicativo está executando com capacidade insuficiente do processador? Para alterar essa política, use o controle à direita da descrição da política e clique em **Aplicar**. Você também pode restaurar valores padrão ou descartar alterações usando os botões na parte inferior da exibição.  
  
-   O valor padrão máximo para utilização do processador é 70%.  
  
-   O valor padrão mínimo para utilização do processador é 0%.  
  
 Quando um aplicativo está executando com espaço de arquivo insuficiente? Para alterar a política de utilização de espaço de arquivos de dados ou de log, use o controle à direita da descrição da política e clique em **Aplicar**. Você também pode restaurar valores padrão ou descartar alterações usando os botões na parte inferior da exibição.  
  
-   O valor padrão máximo para utilização do espaço de arquivo é 70%.  
  
-   O valor padrão mínimo para utilização do espaço de arquivo é 0%.  
  
 Definir políticas globais de monitoramento de aplicativo de instância gerenciada do SQL Server. Para expandir a lista de valores dessa opção, clique na seta ao lado do nome da política ou clique no título da política.  
 Quando uma instância gerenciada do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está executando com capacidade insuficiente de processador? Para alterar essa política, use o controle à direita da descrição da política e clique em **Aplicar**. Você também pode restaurar valores padrão ou descartar alterações usando os botões na parte inferior da exibição.  
  
-   O valor padrão máximo para utilização do processador de instância é 70%.  
  
-   O valor padrão mínimo para utilização do processador de instância é 0%.  
  
 Quando uma instância gerenciada do computador do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está executando com capacidade insuficiente de processador? Para alterar essa política, use o controle à direita da descrição da política e clique em **Aplicar**. Você também pode restaurar valores padrão ou descartar alterações usando os botões na parte inferior da exibição.  
  
-   O valor padrão máximo para utilização do processador do computador é 70%.  
  
-   O valor padrão mínimo para utilização do processador do computador é 0%.  
  
 Quando uma instância gerenciada do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está executando com espaço de arquivo insuficiente? Para alterar a política de utilização de espaço de arquivos de dados ou de log, use o controle à direita da descrição da política e clique em **Aplicar**. Você também pode restaurar valores padrão ou descartar alterações usando os botões na parte inferior da exibição.  
  
-   O valor padrão máximo para utilização do espaço de arquivo é 70%.  
  
-   O valor padrão mínimo para utilização do espaço de arquivo é 0%.  
  
 Quando uma instância gerenciada do computador do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está executando com volume de armazenamento insuficiente? Para alterar essa política, use o controle à direita da descrição da política e clique em **Aplicar**. Você também pode restaurar valores padrão ou descartar alterações usando os botões na parte inferior da exibição.  
  
-   O valor padrão máximo para utilização do espaço do volume do computador é 70%.  
  
-   O valor padrão mínimo para utilização do espaço do volume do computador é 0%.  
  
 Reduzindo o ruído de violação de políticas em recursos altamente voláteis. Para expandir os controles desse recurso, clique na seta para baixo à direita da exibição.  
 Para obter mais informações, veja [Reduzir o ruído em políticas de utilização da CPU &#40;Utilitário do SQL Server&#41;](../../relational-databases/manage/reduce-noise-in-cpu-utilization-policies-sql-server-utility.md)  
  
 
**Guia Segurança** – Exibe nomes de logon com permissões de administração ou leitura no UCP.  
  
 Selecione os logons do UCP que serão adicionados à função Leitor do Utilitário.  
 O privilégio de Leitor do Utilitário permite que a conta de usuário:  
  
-   Conecte-se ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Utility.  
  
-   Veja todos os pontos de vista no Gerenciador do Utilitário no SSMS.  
  
-   Consulte configurações no nó Administração do Utilitário no Gerenciador do Utilitário no SSMS.  
  
 Os administradores do utilitário podem inscrever instâncias do SQL Server no Utilitário do SQL Server e removê-las, bem como modificar políticas em instâncias gerenciadas e modificar configurações de administração no UCP.  
  
 Para ser um administrador do Utilitário, você deve ter privilégios de sysadmin na instância do SQL Server. Para adicionar ou alterar contas de usuário para o UCP do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], use Pesquisador de Objetos no SSMS para adicionar o usuário aos logons do servidor da instância do UCP do SQL Server. Para obter mais informações, veja [sp_addlogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlogin-transact-sql.md).  
  
 
**Guia Data Warehouse** – Exibe os detalhes da configuração do data warehouse de gerenciamento do utilitário.  
  
 Retenção de Dados  
 Especifique o período de retenção de dados de informações de utilização coletadas para instâncias gerenciadas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. O período padrão é de 1 ano. O valor mínimo é 1 mês. O valor com suporte mais longo é 2 anos.  
  
 Informações de Configuração do Data Warehouse do Utilitário  
 Os parâmetros de configuração a seguir não podem ser configurados nesta versão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  
  
-   Nome do UMDW: Sysutility_mdw_\<GUID>_DATA.  
  
-   Frequência de carregamento do conjunto de coleta: a cada 15 minutos.  
  
 O diretório do UMDW é configurável: \<System drive>:\Program Files\Microsoft SQL Server\MSSQL10_50.<UCP_Name>\MSSQL\Data\\, where \<System drive> normalmente é a unidade C:\. O arquivo de log, UMDW_\<GUID>_LOG, está localizado no mesmo diretório.  
  
> **OBSERVAÇÃO:** o local do arquivo UMDW (sysutility_mdw) pode ser alterado com desanexar/anexar ou ALTER DATABASE. É recomendável usar ALTER DATABASE. Para obter mais informações, veja [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md).  
  
 Voltar aos padrões prontos para uso  
 Para redefinir as configurações nessa guia para os valores padrão, clique no botão **Restaurar Padrões** e em **Aplicar**.  
 
  
## <a name="reference"></a>Referência  
 [Criar um ponto de controle do Utilitário do SQL Server &#40;Utilitário do SQL Server&#41;](../../relational-databases/manage/create-a-sql-server-utility-control-point-sql-server-utility.md)  
  
 [Conectar a um Utilitário do SQL Server](../../relational-databases/manage/connect-to-a-sql-server-utility.md)  
  
 [Inscrever uma instância do SQL Server &#40;Utilitário do SQL Server&#41;](../../relational-databases/manage/enroll-an-instance-of-sql-server-sql-server-utility.md)  
  
 [Configurar políticas de integridade &#40;Utilitário do SQL Server&#41;](../../relational-databases/manage/configure-health-policies-sql-server-utility.md)  
  
 [Monitorar instâncias do SQL Server no Utilitário do SQL Server](../../relational-databases/manage/monitor-instances-of-sql-server-in-the-sql-server-utility.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Recursos e tarefas do Utilitário do SQL Server](../../relational-databases/manage/sql-server-utility-features-and-tasks.md)   
 [Solucionar problemas do Utilitário do SQL Server](https://msdn.microsoft.com/library/f5f47c2a-38ea-40f8-9767-9bc138d14453)  
  
  
