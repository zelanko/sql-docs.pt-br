---
title: Detalhes do aplicativo da camada de dados implantados (Utilitário do SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
f1_keywords:
- SQL12.SWB.UE.dac.details.F1
helpviewer_keywords:
- utility, management
- Utility
- SQL Server Utility [SQL Server]
- data-tier application [SQL Server], utility details
- Multi-server management [SQL Server]
ms.assetid: 79c41dd9-abcb-434e-9326-00a341d5c867
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 0ca9186b93e96c60e1c5128e385b5b77d5f2b94e
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62754077"
---
# <a name="deployed-data-tier-application-details-sql-server-utility"></a>Detalhes do aplicativo da camada de dados implantado (Utilitário do SQL Server)
  As informações da exibição Aplicativos da Camada de Dados Implantados do Gerenciador do Utilitário fornecem dados de utilização para aplicativos da camada de dados individuais, o histórico de utilização da CPU, detalhes de utilização do armazenamento em nível de arquivo e a capacidade de exibir e atualizar limites de políticas. Os limites de políticas podem ser controlados no nível de aplicativo da camada de dados para utilização da CPU e para arquivos de log e arquivos de dados do banco de dados. Você também pode exibir detalhes de propriedades de aplicativos da camada de dados individuais.  
  
## <a name="uielement-list"></a>Lista de elementos de interface do usuário  
 Exibição Lista  
 A exibição de lista no painel superior exibe dados sobre aplicativos da camada de dados individuais. Os ícones do estado de integridade fornecem o status resumido de cada aplicativo da camada de dados por categoria de utilização:  
  
-   Marca de verificação verde – ![](../../2014/database-engine/media/well-utilized.gif "Well_utilized") – Número de aplicativos da camada de dados que não estão violando políticas de utilização de recursos. Os recursos estão bem-utilizados.  
  
-   Seta para baixo verde - ![](../../2014/database-engine/media/utility-down-arrow.gif "Utility_down_arrow") - Os recursos estão subutilizados.  
  
-   Seta para cima vermelha - ![](../../2014/database-engine/media/utility-up-arrow.gif "Utility_up_arrow") - Os recursos estão superutilizados.  
  
 A sequência de colunas da exibição de lista pode ser alterada arrastando-se as colunas para a esquerda ou para a direita. Para adicionar ou excluir colunas da exibição de lista, clique com o botão direito do mouse nos títulos das colunas e selecione ou desmarque colunas. O menu de atalho também fornece opções de classificação. A classificação também pode ser ativada clicando-se na parte superior do nome de uma coluna.  
  
 Para acessar as opções de filtro da exibição de lista do Utilitário do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] , clique com o botão direito do mouse no nó **Aplicativos da Camada de Dados Implantados** no painel de navegação do Gerenciador do Utilitário e selecione **Filtrar**. Depois que as configurações de filtro forem implementadas, o nó **Aplicativos da Camada de Dados Implantados** no Gerenciador do Utilitário será rotulado **Aplicativos da Camada de Dados Implantados (filtrados)**. Para obter mais informações, consulte [Configurações de filtro &#40;Pesquisador de Objetos e Gerenciador do Utilitário&#41;](../ssms/object/filter-settings-object-explorer-and-utility-explorer.md).  
  
 Por padrão, as colunas a seguir exibem informações do estado de integridade de cada aplicativo da camada de dados.  
  
-   Nome - O nome do aplicativo da camada de dados.  
  
-   CPU do Aplicativo - Exibe o estado de integridade de utilização de processador para este aplicativo da camada de dados. O estado de integridade desse parâmetro é determinado de acordo com a política de utilização da CPU definida para o aplicativo da camada de dados e o parâmetro de configuração da política de avaliação de recurso volátil. Para obter mais informações, consulte [reduzir o ruído nas políticas de utilização da CPU &#40;Utilitário do SQL Server&#41;](../relational-databases/manage/reduce-noise-in-cpu-utilization-policies-sql-server-utility.md).  
  
     Para exibir o histórico de utilização do processador desse aplicativo da camada de dados ou para exibir ou alterar os limites da política, clique na guia **Utilização da CPU**.  
  
-   CPU do Computador - Exibe o estado de integridade da utilização do processador do computador. O estado de integridade deste parâmetro é determinado de acordo com a política de utilização da CPU definida para o computador e o parâmetro de configuração da política de avaliação de recurso volátil. Para obter mais informações, consulte [reduzir o ruído nas políticas de utilização da CPU &#40;Utilitário do SQL Server&#41;](../relational-databases/manage/reduce-noise-in-cpu-utilization-policies-sql-server-utility.md).  
  
     Para exibir o histórico de utilização do processador desse aplicativo da camada de dados ou para exibir ou alterar os limites da política, clique na guia **Utilização da CPU**.  
  
-   Espaço para Arquivo - Exibe um resumo de estados de integridade de utilização de espaço para arquivo para cada aplicativo da camada de dados.  
  
    -   Verificação verde - Os estados de integridade de todos os grupos de arquivos e grupos de arquivos de log não são superutilizados nem subutilizados.  
  
    -   Seta para baixo verde - O estado de integridade de pelo menos um grupo de arquivos ou grupo de arquivos de log é subutilizado, e nenhum deles é superutilizado.  
  
    -   Seta para cima vermelha - O estado de integridade de pelo menos um grupo de arquivos ou grupo de arquivos de log é superutilizado. Note que, se um banco de dados estiver no estado de "emergência", o estado de integridade exibirá o espaço de arquivo de log superutilizado.  
  
     Para exibir ou alterar os limites da política de espaço para arquivo, clique na guia **Utilização do Armazenamento** .  
  
-   Espaço no Volume - Exibe um resumo dos estados da integridade da utilização do espaço para todos os volumes que contenham bancos de dados pertencentes ao aplicativo da camada de dados selecionado. Se o estado de integridade de qualquer volume for superutilizado, a integridade do espaço no volume será relatada na exibição de lista como superutilizada. Se o estado de integridade de qualquer volume for subutilizado e nenhum volume for superutilizado, a integridade do espaço de volume será relatada na exibição de lista como subutilizada. Caso contrário, o estado da integridade do espaço de volume será relatado na exibição de lista como bem-utilizado. Para exibir ou alterar os limites da política, clique na guia **Utilização de Armazenamento** .  
  
-   Tipo de Política - Indica se as políticas padrão "Globais" ou as políticas personalizadas de "Substituição" estão em vigor para o aplicativo da camada de dados.  
  
-   Nome da Instância - Exibe o nome da instância do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] que hospeda o aplicativo da camada de dados.  
  
 Outras colunas que podem ser exibidas com o menu de atalho na área de título de coluna da exibição de lista:  
  
-   Nome do Banco de Dados  
  
-   Data de Implantação  
  
-   Confiável: (True ou False)  
  
-   Ordenação  
  
-   Nível de Compatibilidade: (por exemplo, Version100)  
  
-   Criptografia Habilitada: (True ou False)  
  
-   Modelo de Recuperação: (Simples, Completa e Bulk-logged)  
  
-   Hora do Último Relatório: esta coluna mostra a data e hora local do UCP usando o tipo de dados datetime. Para obter mais informações, veja o tópico [datetime (Transact-SQL)](https://go.microsoft.com/fwlink/?LinkId=164071) nos Manuais Online do SQL Server. Ao usar o modelo de objeto do Utilitário, observe que o SSMS usa o tipo de dados datetimeoffset. Para obter mais informações, veja o tópico [datetimeoffset (Transact-SQL)](https://go.microsoft.com/fwlink/?LinkId=141713) nos Manuais Online do SQL Server.  
  
 Guia Utilização da CPU  
 A guia Utilização da CPU mostra gráficos lado a lado de dados históricos da utilização de CPU do computador e do aplicativo da camada de dados.  
  
 O gráfico exibe o histórico de utilização do processador para o intervalo especificado nos botões de opção à direita da área de exibição. Para alterar o intervalo de exibição e atualizar o conjunto de dados, selecione um botão de opção na lista.  
  
 As opções de intervalo são as seguintes:  
  
-   1 Dia, exibido em intervalos de 15 minutos.  
  
-   1 Semana, exibido em intervalos de 1 dia.  
  
-   1 Mês, exibido em intervalos de 1 semana.  
  
-   1 Ano, exibido em intervalos de 1 mês.  
  
 Guia Utilização de Armazenamento  
 A guia de Utilização do Armazenamento tem uma exibição de árvore que exibe detalhes de utilização de armazenamento para arquivos de banco de dados e arquivos de log que pertencem ao aplicativo da camada de dados selecionado na exibição de lista. Observe que os dados de tempo mostram a data e hora locais do UCP usando o tipo de dados datetime. Para obter mais informações, veja o tópico [datetime (Transact-SQL)](https://go.microsoft.com/fwlink/?LinkId=164071) nos Manuais Online do SQL Server. Ao usar o modelo de objeto do Utilitário, observe que o SSMS usa o tipo de dados datetimeoffset. Para obter mais informações, veja o tópico [datetimeoffset (Transact-SQL)](https://go.microsoft.com/fwlink/?LinkId=141713) nos Manuais Online do SQL Server.  
  
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
  
 Para obter mais informações sobre como alterar a tolerância para violações da política, consulte [Reduzir o ruído em políticas de utilização da CPU &#40;Utilitário do SQL Server&#41;](../relational-databases/manage/reduce-noise-in-cpu-utilization-policies-sql-server-utility.md).  
  
 Guia Detalhes da Propriedade  
 Os detalhes da propriedade listados para aplicativos da camada de dados incluem as seguintes categorias:  
  
-   Nome do Banco de Dados  
  
-   Data de Implantação  
  
-   Confiável: (True ou False)  
  
-   Ordenação  
  
-   Nível de Compatibilidade: (por exemplo, Version100)  
  
-   Criptografia Habilitada: (True ou False)  
  
-   Modelo de Recuperação: (Simples, Completa e Bulk-logged)  
  
-   Hora do Último Relatório: esta coluna mostra a data e hora local do UCP usando o tipo de dados datetime. Para obter mais informações, veja o tópico [datetime (Transact-SQL)](https://go.microsoft.com/fwlink/?LinkId=164071) nos Manuais Online do SQL Server. Ao usar o modelo de objeto do Utilitário, observe que o SSMS usa o tipo de dados datetimeoffset. Para obter mais informações, veja o tópico [datetimeoffset (Transact-SQL)](https://go.microsoft.com/fwlink/?LinkId=141713) nos Manuais Online do SQL Server.  
  
## <a name="see-also"></a>Consulte Também  
 [Detalhes do Instância Gerenciada &#40;Utilitário do SQL Server&#41;](../../2014/database-engine/managed-instance-details-sql-server-utility.md)   
 [Painel do utilitário &#40;Utilitário do SQL Server&#41;](../../2014/database-engine/utility-dashboard-sql-server-utility.md)   
 [Monitorar instâncias de SQL Server no Utilitário do SQL Server](../relational-databases/manage/monitor-instances-of-sql-server-in-the-sql-server-utility.md)   
 [Recursos e tarefas do Utilitário do SQL Server](../relational-databases/manage/sql-server-utility-features-and-tasks.md)  
  
  
