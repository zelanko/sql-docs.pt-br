---
title: Detalhes de instâncias (utilitário do SQL Server) gerenciadas | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
ms.assetid: 6e51b7bb-a733-4852-8c33-7f4dbdf931c2
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 5677e7f5dc7a5191b2d39e6100cafee1f38e86ab
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48185446"
---
# <a name="managed-instance-details-sql-server-utility"></a>Detalhes de instâncias gerenciadas (Utilitário do SQL Server)
  As informações da exibição Instâncias Gerenciadas do Gerenciador do Utilitário fornecem dados de utilização para instâncias individuais do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], histórico de utilização da CPU, detalhes de utilização do armazenamento em nível de arquivo e a capacidade de exibir e atualizar limites de políticas. Os limites de políticas podem ser controlados no nível de instância do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] , para um computador, para arquivos de banco de dados e arquivos de log e no nível de volumes de armazenamento. Você também pode exibir detalhes de propriedades de instâncias gerenciadas individuais do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
## <a name="uielement-list"></a>Lista de elementos de interface do usuário  
 Exibição de lista  
 A exibição de lista no painel superior exibe dados sobre instâncias individuais do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] listadas em linhas por ComputerName\InstanceName.  
  
 Os ícones do estado de integridade fornecem o status resumido de cada instância do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] por categoria de utilização:  
  
-   Marca de verificação verde – ![](../../2014/database-engine/media/well-utilized.gif "Well_utilized") – Número de instâncias gerenciadas do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] que não estão violando políticas de utilização de recursos. Os recursos estão bem-utilizados.  
  
-   Seta para baixo verde – ![](../../2014/database-engine/media/utility-down-arrow.gif "Utility_down_arrow") – Os recursos estão subutilizados.  
  
-   Seta para cima vermelha – ![](../../2014/database-engine/media/utility-up-arrow.gif "Utility_up_arrow") – Os recursos estão superutilizados.  
  
 A sequência de colunas da exibição de lista pode ser alterada arrastando-se as colunas para a esquerda ou para a direita. Para adicionar ou excluir colunas da exibição de lista, clique com o botão direito do mouse nos títulos das colunas e selecione ou desmarque colunas. O menu de atalho também fornece opções de classificação. A classificação também pode ser ativada clicando-se na parte superior do nome de uma coluna.  
  
 Para acessar as opções de filtro da exibição de lista do Utilitário, clique com o botão direito do mouse no nó **Instâncias Gerenciadas** no painel de navegação do Gerenciador do Utilitário e selecione **Filtrar**. Depois que as configurações de filtro forem implementadas, o nó **Instâncias Gerenciadas** no Gerenciador do Utilitário será rotulado **Instâncias Gerenciadas (filtradas)**. Para obter mais informações, consulte [Configurações de filtro &#40;Pesquisador de Objetos e Gerenciador do Utilitário&#41;](../ssms/object/filter-settings-object-explorer-and-utility-explorer.md).  
  
 Por padrão, as colunas a seguir exibem informações do estado de integridade de cada instância gerenciada do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
-   CPU da Instância – Exibe o estado de integridade da utilização do processador alocado a essa instância do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. O estado de integridade deste parâmetro é determinado de acordo com a política de utilização da CPU definida para a instância do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] e o parâmetro de configuração da política de avaliação de recurso volátil. Para obter mais informações, veja [Reduzir o ruído em políticas de utilização da CPU &#40;Utilitário do SQL Server&#41;](../relational-databases/manage/reduce-noise-in-cpu-utilization-policies-sql-server-utility.md).  
  
     Para exibir o histórico da utilização do processador para essa instância do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]ou para exibir ou alterar os limites da política, clique na guia **Utilização da CPU** .  
  
-   CPU do Computador - Exibe o estado de integridade da utilização do processador do computador. O estado de integridade deste parâmetro é determinado de acordo com a política de utilização da CPU definida para o computador e o parâmetro de configuração da política de avaliação de recurso volátil. Para obter mais informações, veja [Reduzir o ruído em políticas de utilização da CPU &#40;Utilitário do SQL Server&#41;](../relational-databases/manage/reduce-noise-in-cpu-utilization-policies-sql-server-utility.md).  
  
     Para exibir o histórico da utilização do processador para essa instância do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]ou para exibir ou alterar os limites da política, clique na guia **Utilização da CPU** .  
  
-   Espaço de Arquivo – Exibe um resumo dos estados da integridade da utilização do espaço de arquivo de todos os bancos de dados que pertencem à instância selecionada do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Se o estado de integridade de qualquer arquivo do banco de dados for superutilizado, a integridade do espaço de arquivo será informada na exibição de lista como superutilizada. Se o estado de integridade de qualquer do banco de dados for subutilizado e nenhum banco de dados for superutilizado, a integridade do espaço de arquivo será relatada na exibição de lista como subutilizada. Caso contrário, o estado da integridade do espaço de arquivo será relatado na exibição de lista como bem-utilizado. Para exibir ou alterar os limites da política, clique na guia **Utilização de Armazenamento** .  
  
-   Espaço de Volume - Exibe um resumo dos estados da integridade da utilização do espaço de volume de todos os volumes que contêm bancos de dados pertencentes à instância selecionada do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Se o estado de integridade de qualquer volume for superutilizado, a integridade do espaço no volume será relatada na exibição de lista como superutilizada. Se o estado de integridade de qualquer volume for subutilizado e nenhum volume for superutilizado, a integridade do espaço de volume será relatada na exibição de lista como subutilizada. Caso contrário, o estado da integridade do espaço de volume será relatado na exibição de lista como bem-utilizado. Para exibir ou alterar os limites da política, clique na guia **Utilização de Armazenamento** .  
  
-   Tipo de Política - Indica se as políticas padrão "Globais" ou as políticas personalizadas de "Substituição" estão em vigor para a instância gerenciada do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
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
  
-   Agrupamento:  
  
-   Diferenciar Maiúsculas de Minúsculas: (Verdadeiro ou Falso)  
  
-   Idioma:  
  
-   Hora do Último Relatório: esta coluna mostra a data e hora local do UCP usando o tipo de dados datetime. Para obter mais informações, veja o tópico [datetime (Transact-SQL)](http://go.microsoft.com/fwlink/?LinkId=164071) nos Manuais Online do SQL Server. Ao usar o modelo de objeto do Utilitário, observe que o SSMS usa o tipo de dados datetimeoffset. Para obter mais informações, veja o tópico [datetimeoffset (Transact-SQL)](http://go.microsoft.com/fwlink/?LinkId=141713) nos Manuais Online do SQL Server.  
  
 Guia Utilização da CPU  
 A guia Utilização da CPU mostra gráficos lado a lado de dados históricos da utilização da CPU do computador e da instância do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .  
  
 O gráfico exibe o histórico de utilização do processador para o intervalo especificado nos botões de opção à direita da área de exibição. Para alterar o intervalo de exibição e atualizar o conjunto de dados, selecione um botão de opção na lista.  
  
 As opções de intervalo são as seguintes:  
  
-   1 Dia, exibido em intervalos de 15 minutos.  
  
-   1 Semana, exibido em intervalos de 1 dia.  
  
-   1 Mês, exibido em intervalos de 1 semana.  
  
-   1 Ano, exibido em intervalos de 1 mês.  
  
 Guia Utilização de Armazenamento  
 A guia Utilização de Armazenamento tem uma exibição de árvore que exibe detalhes da utilização do armazenamento. Observe que os dados de tempo mostram a data e hora locais do UCP usando o tipo de dados datetime. Para obter mais informações, veja o tópico [datetime (Transact-SQL)](http://go.microsoft.com/fwlink/?LinkId=164071) nos Manuais Online do SQL Server. Ao usar o modelo de objeto do Utilitário, observe que o SSMS usa o tipo de dados datetimeoffset. Para obter mais informações, veja o tópico [datetimeoffset (Transact-SQL)](http://go.microsoft.com/fwlink/?LinkId=141713) nos Manuais Online do SQL Server.  
  
 A exibição pode ser agrupada por banco de dados ou por volume. Para usar a exibição de árvore do banco de dados, selecione o botão de opção **Banco de dados** na seleção **Agrupar arquivos por:** . Para exibir o status da utilização do armazenamento de arquivos individuais do banco de dados, clique no sinal de adição ao lado do nome de um banco de dados na exibição de árvore. Os arquivos de banco de dados listados incluem todos os bancos de dados do sistema e de usuários que pertencem à instância gerenciada do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] selecionados na exibição de lista.  
  
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
  
 Para obter mais informações sobre como alterar a tolerância para violações da política, consulte [Reduzir o ruído em políticas de utilização da CPU &#40;Utilitário do SQL Server&#41;](../relational-databases/manage/reduce-noise-in-cpu-utilization-policies-sql-server-utility.md).  
  
 Guia Detalhes da Propriedade  
 Os detalhes da propriedade listados para instâncias do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] incluem as seguintes categorias:  
  
-   Nome do Processador:  
  
-   Velocidade do Processador (MHz):  
  
-   Contagem de Processadores:  
  
-   Memória Física (MB):  
  
-   Versão do Sistema Operacional:  
  
-   Versão do SQL Server:  
  
-   Edição do SQL Server:  
  
-   Clusterizado: (Verdadeiro ou Falso)  
  
-   Diretório de Backup:  
  
-   Agrupamento:  
  
-   Diferenciar Maiúsculas de Minúsculas: (Verdadeiro ou Falso)  
  
-   Idioma:  
  
## <a name="see-also"></a>Consulte também  
 [Detalhes do aplicativo da camada de dados implantado &#40;Utilitário do SQL Server&#41;](../../2014/database-engine/deployed-data-tier-application-details-sql-server-utility.md)   
 [Painel do utilitário &#40;utilitário do SQL Server&#41;](../../2014/database-engine/utility-dashboard-sql-server-utility.md)   
 [Monitorar instâncias do SQL Server no Utilitário do SQL Server](../relational-databases/manage/monitor-instances-of-sql-server-in-the-sql-server-utility.md)   
 [Recursos e tarefas do Utilitário do SQL Server](../relational-databases/manage/sql-server-utility-features-and-tasks.md)   
 [Solucionar problemas do Utilitário do SQL Server](../../2014/database-engine/troubleshoot-the-sql-server-utility.md)  
  
  
