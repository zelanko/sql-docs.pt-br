---
title: "Criar uma política de conciliação | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: data-quality-services
ms.service: 
ms.component: data-quality-services
ms.reviewer: 
ms.suite: sql
ms.technology:
- data-quality-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dqs.kb.kbmatchingmap.f1
- sql13.dqs.kb.kbmatchingpolicy.f1
- sql13.dqs.kb.kbmatchingresults.f1
ms.assetid: cce77a06-ca31-47b6-8146-22edf001d605
caps.latest.revision: 43
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.translationtype: HT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 1fe1c8b25d8309d3984c70c31f5949a9724599a3
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="create-a-matching-policy"></a>Criar uma política de correspondência
  Este tópico descreve como criar uma política correspondente em uma base de dados de conhecimento no [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS). Você se prepara para o processo de correspondência no DQS executando a atividade Política de Correspondência dos dados de exemplo. Nesta atividade, você cria e testa uma ou mais regras de correspondência na política e depois publica a base de dados de conhecimento para tornar as regras de correspondência publicamente disponíveis para uso. Pode haver apenas uma política de correspondência em uma base de dados de conhecimento, mas essa política pode conter várias regras de correspondência.  
  
 A criação de política de correspondência é executada em três estágios: um processo de mapeamento no qual você identifica a fonte de dados e mapeia os domínios para colunas, um processo de política de correspondência no qual você cria uma ou mais regras de correspondência e testa cada regra de correspondência separadamente e um processo de resultados de correspondência no qual você executa todas as regras de correspondência em conjunto e, caso fique satisfeito com elas, adiciona a política à base de dados de conhecimento. Cada um desses processos é executado em uma página separada do assistente da atividade Política de Correspondência, permitindo que você percorra páginas diferentes, para executar o processo novamente e fechar um processo de política de correspondência específico e depois retornar ao mesmo estágio do processo. Depois de testar todas as regras em conjunto, se desejar, você poderá retornar à página **Política de Correspondência** , ajustar uma regra individual, testá-la separadamente outra vez e retornar à página **Resultados de Correspondência** para executar todas as regras em conjunto mais uma vez. O DQS fornece estatísticas sobre a fonte de dados, as regras de correspondência e os resultados de correspondência que permitem a você tomar decisões conscientes sobre a política de correspondência, para que seja possível refiná-la.  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Prerequisites"></a> Pré-requisitos  
 O Microsoft Excel deverá ser instalado no computador [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] se os dados de origem estiverem em um arquivo do Excel. Caso contrário, você não poderá selecionar o arquivo do Excel no estágio de mapeamento. Os arquivos criados pelo Microsoft Excel podem ter a extensão .xlsx, .xls ou .csv. Se a versão de 64 bits do Excel for usada, somente arquivos do Excel 2003 (.xls) terão suporte; não haverá suporte para os arquivos do Excel 2007 ou 2010 (.xlsx). Se você estiver usando a versão de 64 bits do Excel 2007 ou 2010, salve o arquivo como .xls ou .csv ou instale uma versão de 32 bits do Excel.  
  
###  <a name="Security"></a> Segurança  
  
####  <a name="Permissions"></a> Permissões  
 Você deve ter a função dqs_kb_editor ou dqs_administrator no banco de dados DQS_MAIN para criar uma política de correspondência.  
  
##  <a name="MatchingRules"></a> Como definir parâmetros de regra de correspondência  
 A criação de uma regra de correspondência é um processo interativo no qual você insere os fatores usados para determinar se um registro é uma correspondência para outro. Você pode inserir condições para qualquer domínio em uma tabela. Quando o DQS executa a correspondência em dois registros, ele comparará os valores nos campos mapeados para os domínios incluídos na regra de correspondência. O DQS analisa os valores em cada campo na regra e, em seguida, usa os fatores inseridos na regra para cada domínio para calcular uma pontuação de correspondência final. Se a pontuação de correspondência dos dois registros comparados for maior que a pontuação de correspondência mínima, os dois campos serão considerados correspondências.  
  
 Os fatores que você insere em uma regra de correspondência incluem os seguintes:  
  
-   Peso: para cada domínio na regra, insira um peso numérico que determine como a análise de correspondência para o domínio será comparada à de cada domínio na regra. O peso indica a contribuição da pontuação do campo para a pontuação de correspondência geral entre dois registros. As pontuações calculadas atribuídas a cada campo de origem são somadas para se obter uma pontuação de correspondência composta para os dois registros. Para cada campo que não é um pré-requisito (com uma similaridade de exato ou similar), defina o peso entre 10 e 100. A soma dos pesos dos domínios que não são pré-requisitos deve ser igual a 100. Se o valor for um pré-requisito, o peso será definido como 0 e não poderá ser alterado.  
  
-   Similaridade de exato: selecione **Exato** se os valores no mesmo campo de dois registros diferentes tiverem que ser idênticos para os valores a serem considerados para uma correspondência. Se idênticos, a pontuação de correspondência para esse domínio será definida como “100” e o DQS utilizará essa pontuação e as pontuações dos outros domínios na regra para determinar a pontuação de correspondência de agregação. Se não forem idênticos, a pontuação de correspondência para esse domínio será definida como “0” e o processamento da regra prosseguirá para a próxima condição. Se você configurar uma regra de correspondência para um domínio numérico e selecionar **Similar**, poderá inserir uma tolerância como um percentual ou um número inteiro. Para um domínio do tipo data, você pode inserir uma tolerância como dia, mês ou ano (inteiro) se selecionar **Similar**; não há nenhuma tolerância percentual para um domínio de data. Se você selecionar **Exato**, não terá essa opção.  
  
-   Similaridade de similar: selecione **Similar** se dois valores no mesmo campo de dois registros diferentes puderem ser considerados uma correspondência, mesmo que os valores não sejam idênticos. Quando o DQS executa a regra, ele calculará uma pontuação de correspondência para esse domínio e utilizará essa pontuação e as pontuações dos outros domínios na regra para determinar a pontuação de correspondência de agregação. A similaridade mínima entre os valores de um campo é 60%. Se a pontuação de correspondência calculada para um campo de dois registros for inferior a 60, a pontuação de similaridade será definida automaticamente como 0. Se você estiver configurando uma regra de correspondência para um campo numérico e selecionar **Similar**, poderá inserir uma tolerância como um percentual ou um número inteiro. Se você estiver configurando uma regra de correspondência para um campo de data e selecionar **Similar**, poderá inserir uma tolerância numérica.  
  
-   Pré-requisito: selecione **Pré-requisito** para especificar que os valores no mesmo campo em dois registros diferentes devem retornar uma correspondência de 100% ou os registros não serão considerados uma correspondência e as outras cláusulas na regra serão desconsideradas. Quando a opção **Pré-requisito** está selecionada, o campo de peso do domínio é removido de forma que você não pode definir um peso para o domínio. Você deve reiniciar um ou mais pesos de domínio para que a soma dos pesos seja igual a 100. Os domínios de pré-requisitados não contribuem para a pontuação de correspondência de registro. A pontuação de correspondência de registro é determinada pela comparação dos valores nos campos para os quais a Similaridade está definida como Similar ou Exata. Quando você cria um campo e um pré-requisito, a Similaridade para esse domínio é definida automaticamente como Exata.  
  
 A pontuação de correspondência mínima é o limite no qual ou acima do qual dois registros são considerados uma correspondência (e o status dos registros é definido como “Correspondente”). Insira um valor inteiro em incrementos de “1” ou clique na seta para cima ou para baixo para aumentar ou diminuir o valor em incrementos de “10”. O valor mínimo é 80. Se a pontuação de correspondência estiver abaixo de 80, os dois registros não serão considerados uma correspondência. Você não pode alterar o intervalo da pontuação de correspondência mínima nessa página. A pontuação de correspondência mínima é 80. Você pode, no entanto, alterar a pontuação de correspondência mínima mais baixa na página Administração (se for um administrador do DQS).  
  
 A criação de uma regra de correspondência é um processo iterativo porque talvez você precise alterar os pesos relativos dos domínios na regra ou a similaridade ou a propriedade de pré-requisito para um domínio ou a pontuação de correspondência mínima ou ainda a pontuação de correspondência mínima para a regra, para alcançar os resultados necessários. Talvez você também ache que precisa criar várias regras, sendo que cada uma será executada para criar a pontuação correspondente. Pode ser difícil obter o resultado necessário com uma regra apenas. Várias regras fornecerão exibições diferentes de uma correspondência necessária. Com várias regras, você poderá incluir menos domínios em cada regra, usar pesos mais altos para cada domínio e obter resultados melhores. Se os dados estiverem menos precisos e menos completos, talvez sejam necessárias mais regras para localizar as correspondências exigidas. Se os dados estiverem mais precisos e completos, você precisará de menos regras.  
  
 A criação de perfil fornece ideias sobre a integridade e a exclusividade. Considere a integridade e a exclusividade em tandem. Use os dados de integridade e exclusividade para determinar qual peso atribuir a um campo no processo de correspondência. Se houver um nível alto de exclusividade em um campo, o uso de um campo em uma política de correspondência poderá diminuir os resultados de correspondência, de modo que talvez você queira definir o peso desse campo para um valor relativamente pequeno. Se houver um nível baixo de exclusividade para uma coluna, porém baixa integridade, talvez você não queira incluir um domínio para essa coluna. Com um nível baixo de exclusividade, porém um nível alto de integridade, talvez você queira incluir o domínio. Algumas colunas, como gênero, podem ter um nível de exclusividade baixo naturalmente. Para obter mais informações, consulte [Guias Criador de Perfil e Resultados](#Tabs).  
  
##  <a name="Starting"></a> Primeira etapa: iniciando uma política de correspondência  
 Execute a atividade de política de correspondência na área de gerenciamento da base de dados de conhecimento do aplicativo [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] .  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)] [Executar o aplicativo Data Quality Client](../data-quality-services/run-the-data-quality-client-application.md).  
  
2.  Na tela inicial do [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] , clique em **Nova base de dados de conhecimento** para criar uma política de correspondência em uma nova base de dados de conhecimento. Insira um nome para a base de dados de conhecimento, insira uma descrição e defina **Criar base de dados de conhecimento de** conforme desejar. Clique na **Política de Correspondência** da atividade. Clique em **Avançar** para continuar.  
  
3.  Clique em **Abrir base de dados de conhecimento** para criar ou modificar a política de correspondência em uma base de dados de conhecimento existente. Selecione a base de dados de conhecimento, selecione **Política de Correspondência**e clique em **Avançar**. Também é possível clicar em uma base de dados de conhecimento em **Base de Dados de Conhecimento Recente**. Se você abrir uma base de dados de conhecimento que foi fechada quando uma política de correspondência estava sendo trabalhada, prosseguirá para o estágio em que a atividade de política de correspondência foi fechada (conforme indicado pela coluna **Estado** da base de dados de conhecimento na tabela de base de dados de conhecimento ou no nome da base de dados de conhecimento em **Base de Dados de Conhecimento Recente**). Se você abrir uma base de dados de conhecimento que inclua uma política de correspondência e foi terminada, a página **Política de Correspondência** será exibida. Se você abrir uma base de dados de conhecimento que não inclua uma política de correspondência e foi terminada, a página **Mapeamento** será exibida.  
  
##  <a name="MatchingStage"></a> Estágio de mapeamento  
 No estágio de mapeamento, identifique a origem dos dados para os quais você criará a política de correspondência e mapeie colunas de origem para domínios para tornar os domínios disponíveis para a atividade de política correspondente.  
  
1.  Na página **Mapa** , para criar uma política para um banco de dados, deixe a **Fonte de Dados** como **SQL Server**, selecione o banco de dados para o qual deseja criar a política em **Banco de dados**e selecione a tabela ou exibição em **Tabela/Exibição**. O banco de dados de origem deve estar presente na mesma instância do SQL Server que o [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)]. Caso contrário, ele não será exibido na lista suspensa.  
  
2.  Para criar uma política para os dados em uma planilha do Excel, selecione **Arquivo do Excel** como **Fonte de Dados**, clique em **Procurar** e selecione o arquivo do Excel e deixe a opção **Usar primeira linha como cabeçalho** selecionada se apropriado. Em **Planilha**, selecione a planilha no arquivo do Excel que será a origem dos dados. O Microsoft Excel deverá ser instalado no computador Cliente Data Quality para selecionar um arquivo do Excel. Caso contrário, o botão Procurar não estará disponível e você será notificado sob esta caixa de texto de que o Microsoft Excel não está instalado.  
  
3.  Em **Mapeamentos**, selecione um campo para **Coluna de Origem**e clique no ícone **Criar Domínio** .  
  
4.  Em **Mapeamentos**, selecione um campo na fonte de dados para **Coluna de Origem**e selecione o domínio correspondente. Repita para todos os domínios que você usa no processo de correspondência. Crie domínios conforme necessário clicando em **Criar um Domínio** ou **Criar um Domínio Composto**.  
  
    > [!NOTE]  
    >  Você poderá mapear sua fonte de dados para um domínio DQS enquanto cria uma política de correspondência somente se o tipo de dados de origem tiver suporte no DQS e corresponder ao tipo de dados de domínio do DQS. Para obter mais informações sobre tipos de dados que oferecem suporte no DQS, consulte [O SQL Server com suporte e tipos de dados do SSIS para domínios do DQS](../data-quality-services/supported-sql-server-and-ssis-data-types-for-dqs-domains.md).  
  
5.  Clique no controle **mais (+)** para adicionar uma linha à tabela Mapeamentos ou no controle **menos (–)** para remover uma linha.  
  
6.  Clique em **Visualizar fonte de dados** para visualizar os dados na tabela do SQL Server ou visualizar os dados selecionados ou a planilha do Excel selecionada.  
  
7.  Clique em **Exibir/Selecionar Domínios Compostos** para exibir uma lista dos domínios compostos disponíveis na base de dados de conhecimento e selecione conforme apropriado para mapeamento.  
  
8.  Clique em **Avançar** para prosseguir para o estágio de política de correspondência.  
  
    > [!NOTE]  
    >  Clique em **Fechar** para salvar o estágio do projeto correspondente e retornar à página inicial do DQS. Na próxima vez que abrir este projeto, você iniciará no mesmo estágio. Clique em **Cancelar** para terminar a atividade de correspondência, perder seu trabalho e retornar à página inicial do DQS.  
  
##  <a name="MatchingPolicyStage"></a> Estágio de Política de Correspondência  
 Crie regras de correspondência e teste-as separadamente na página Política de Correspondência. Quando testar uma regra de correspondência na página **Política de Correspondência** , você visualizará uma tabela de resultados de correspondência que mostra os clusters que o DQS identificou para a regra selecionada. A tabela mostra cada registro no cluster com os valores de domínio de mapeamento e a pontuação correspondente e o registro dinâmico inicial para o cluster. Também é possível exibir os dados de criação de perfil do processo correspondente como um todo, as condições em cada regra de correspondência e as estatísticas sobre os resultados de cada regra de correspondência separada. Você pode se filtrar com base nos dados da regra mestra desejados.  
  
 Para obter mais informações sobre como as regras de correspondência funcionam, consulte [Como definir parâmetros de regra de correspondência](#MatchingRules).  
  
1.  Na página **Política de Correspondência** , clique no ícone **Criar uma regra de correspondência** .  
  
2.  Insira um nome e descrição para a regra.  
  
3.  Aumente o valor de **Pontuação mínima de correspondência** se você quiser tornar os requisitos de correspondência mais estritos. Para obter mais informações sobre a pontuação de correspondência mínima, consulte [Como definir parâmetros de regra de correspondência](#MatchingRules).  
  
4.  Clique no ícone **Adicionar um novo elemento de domínio** .  
  
5.  Selecione um domínio ou domínio composto para o qual inserir valores.  
  
    > [!NOTE]  
    >  Você só poderá selecionar um domínio composto se cada domínio único no domínio composto tiver sido mapeado para uma coluna de origem.  
  
6.  Para **Similaridade**, selecione **Similar** se dois valores no mesmo campo de dois registros diferentes puderem ser considerados uma correspondência, mesmo que os valores não sejam idênticos. Selecione **Exato** se dois valores no mesmo campo de dois registros diferentes tiverem que ser idênticos para ser considerados uma correspondência. (Para obter mais informações, consulte [Como definir parâmetros de regra de correspondência](#MatchingRules).)  
  
7.  Para **peso**, insira um valor que determina a contribuição de uma pontuação de correspondência de domínio para a pontuação de correspondência geral para dois registros.  
  
    > [!NOTE]  
    >  Quando você define um peso para um domínio composto, pode inserir um peso diferente para cada domínio único no domínio composto, caso em que o domínio composto não recebe um peso separado, ou pode inserir um peso único para o domínio composto no qual os domínios únicos no domínio composto não recebem pesos separados.  
  
8.  Selecione **Pré-requisito** para especificar que os valores do campo em dois registros diferentes devem retornar uma correspondência de 100% ou os registros não serão considerados uma correspondência e as outras cláusulas na regra serão desconsideradas. Se a **Similaridade** for **Similar**, ela será alterada para **Exata**e o peso será removido, pois a correspondência deverá ser 100%.  
  
9. Repita as etapas 4 a 8 para todos os outros domínios que farão parte da regra de correspondência. Verifique se a soma de pesos para todos os domínios na regra é igual a 100.  
  
10. Selecione **Clusters sobrepostos** na lista suspensa para exibir os registros dinâmicos e os registros a seguir para todos os clusters quando a correspondência for executada, mesmo que grupos de clusters tenham registros em comum. Selecione **Clusters não sobrepostos** para exibir clusters que tenham registros em comum como um cluster único quando a correspondência for executada.  
  
11. Clique em **Recarregar os dados da origem** para copiar dados da origem de dados na tabela de preparação e reindexá-los quando você executar a política de correspondência. Clique em **Executar nos dados anteriores** para executar uma política de correspondência sem copiar os dados na tabela de preparação e reindexar os dados. A opção**Executar nos dados anteriores** está desabilitada para a primeira execução da política de correspondência ou se você alterar o mapeamento na página **Mapa** e depois pressionar **Sim** no pop-up seguinte. Em ambos os casos, você deverá reindexar. Não será necessário reindexar se a política de correspondência não tiver sido alterada. A execução nos dados anteriores pode ajudar no desempenho.  
  
12. Clique em **Iniciar** para executar o processo de correspondência para a regra selecionada. Quando o processo for concluído, a tabela exibirá o ID do Registro, o número do Cluster e as colunas de dados (incluindo aquelas que não estão na regra de correspondência) para cada registro em um cluster. A linha dinâmica no cluster é considerada como a principal candidata a sobreviver ao processo de desduplicação. Cada linha adicional em um cluster é considerada uma duplicata; sua pontuação correspondente (em comparação com o registro dinâmico) é fornecida na tabela de resultados. O número do cluster é igual à ID do registro dinâmico no cluster.  
  
13. Você pode trabalhar com os dados na tabela **Resultados de Correspondência** da seguinte forma:  
  
    -   Em **Filtro**, selecione **Correspondente** para mostrar todas as linhas correspondentes e sua pontuação. As linhas que não são consideradas correspondências (que têm uma pontuação correspondente inferior à pontuação correspondente mínima) não são mostradas na tabela de resultados correspondente. Selecione **Sem correspondência** para mostrar todas as linhas sem correspondência, não as linhas correspondentes.  
  
    -   Na caixa suspensa **Percentual**, selecione um percentual na lista suspensa, em incrementos de “5”. Todas as linhas com uma pontuação correspondente maior ou igual ao percentual serão exibidas na tabela de resultados correspondente.  
  
    -   Se você clicar duas vezes em um registro na tabela de resultados correspondente, o DQS exibirá um pop-up **Detalhes da Pontuação de Correspondência** que exibe o registro dinâmico e o registro de origem (e os valores em todos os campos), a pontuação entre eles e uma busca detalhada da correspondência de registro. A busca detalhada exibe os valores em cada campo do registro dinâmico e no registro de origem para que você possa compará-los e mostra a pontuação de correspondência com a qual cada campo contribui para a pontuação de correspondência geral para os dois registros.  
  
14. Exiba as estatísticas nas guias **Criador de perfil** e **Resultados de Correspondência** para assegurar que você esteja obtendo os resultados necessários. Para obter mais informações, consulte [Guias Criador de Perfil e Resultados](#Tabs).  
  
15. Se for necessário alterar a regra, altere-a no Editor de Regra e clique em **Reiniciar**.  
  
    > [!NOTE]  
    >  Após a primeira análise de dados, o botão **Iniciar** se transforma em um botão **Iniciar** . Se os resultados da análise anterior ainda não tiverem sido salvos, clicar em **Reiniciar** causará a perda dos dados anteriores. Durante a execução da análise, não saia da página; do contrário, o processo de análise será encerrado.  
  
16. A guia **Resultados de Correspondência** exibe estatísticas das duas últimas execuções da regra. Se você executou a regra de correspondência mais de uma vez com configurações diferentes, compare as estatísticas da regra atual e da regra anterior. Se você descobrir que os resultados da regra anterior eram melhores, clique em **Restaurar regra anterior** para restaurar as condições da regra anterior, retornando a regra para seu estado anterior antes de editar. As condições de regra atuais serão perdidas. Isso permite a você ajustar a política com base nas duas últimas execuções de correspondência, diminuindo o tempo que passa ajustando a política de correspondência.  
  
17. Se você quiser que outra regra seja adicionada a política de correspondência, repita o procedimento a partir da etapa 1.  
  
18. Clique em **Avançar** para prosseguir para o estágio de resultados de correspondência.  
  
##  <a name="MatchingResultsStage"></a> Estágio de Resultados de Correspondência  
 Teste todas as suas regras de correspondência de uma vez na página **Resultados de Correspondência** . Antes de fazer isso, especifique se a execução do teste de regra identificará os clusters sobrepostos ou não sobrepostos. Se você estiver executando as regras várias vezes, poderá executar a regra nos dados recarregados com base nos dados de origem ou anteriores.  
  
 Quando testar as regras de correspondência na página **Resultados de Correspondência** , você visualizará uma tabela de resultados de correspondência que mostra os clusters que o DQS identificou para todas as regras. A tabela mostra cada registro no cluster com os valores de domínio de mapeamento e a pontuação correspondente e o registro dinâmico inicial para o cluster. Também é possível exibir os dados de criação de perfil das regras de correspondência como um todo, as condições em cada regra de correspondência e as estatísticas sobre os resultados todas as regras de correspondência.  
  
1.  Na página **Resultados de Correspondência** , selecione **Clusters sobrepostos** na lista suspensa para exibir os registros dinâmicos e os registros a seguir para todos os clusters quando a correspondência for executada, mesmo que grupos de clusters tenham registros em comum. Selecione **Clusters não sobrepostos** para exibir clusters que tenham registros em comum como um cluster único quando a correspondência for executada.  
  
2.  Clique em **Recarregar os dados da origem** para copiar dados da origem de dados na tabela de preparação e reindexá-los quando você executar a política de correspondência. Clique em **Executar nos dados anteriores** para executar uma política de correspondência sem copiar os dados na tabela de preparação e reindexar os dados. A opção**Executar nos dados anteriores** está desabilitada para a primeira execução da política de correspondência ou se você alterar o mapeamento na página **Mapa** e depois pressionar **Sim** no pop-up seguinte. Em ambos os casos, você deverá reindexar. Não será necessário reindexar se a política de correspondência não tiver sido alterada. A execução nos dados anteriores pode ajudar no desempenho.  
  
3.  Clique em **Iniciar** para executar o processo de correspondência para todas as regras que você definiu. A tabela **Resultados de Correspondência** exibe a ID do registro, o número do cluster e as colunas de dados (incluindo aquelas que não estão na regra de correspondência) para cada registro em um cluster. O registro principal no cluster é selecionado aleatoriamente. (Você determina o registro sobrevivente selecionando a regra de sobrevivência na página **Exportar** ao executar o projeto de correspondência.) Cada linha adicional em um cluster é considerada uma duplicata; sua pontuação correspondente (em comparação com o registro dinâmico) é fornecida na tabela de resultados.  
  
4.  Você pode trabalhar com os dados na tabela **Resultados de Correspondência** da seguinte forma:  
  
    -   Em **Filtro**, selecione **Correspondente** para mostrar todas as linhas correspondentes e sua pontuação. As linhas que não são consideradas correspondências (que têm uma pontuação correspondente inferior à pontuação correspondente mínima) não são mostradas na tabela de resultados correspondente. Selecione **Sem correspondência** para mostrar todas as linhas sem correspondência, não as linhas correspondentes.  
  
    -   Na caixa suspensa **Percentual**, selecione um percentual na lista suspensa, em incrementos de “5”. Todas as linhas com uma pontuação correspondente maior ou igual ao percentual serão exibidas na tabela de resultados correspondente.  
  
    -   Se você clicar duas vezes em um registro na tabela de resultados correspondente, o DQS exibirá um pop-up **Detalhes da Pontuação de Correspondência** que exibe o registro dinâmico e o registro de origem (e os valores em todos os campos), a pontuação entre eles e uma busca detalhada da correspondência de registro. A busca detalhada exibe os valores em cada campo do registro dinâmico e no registro de origem para que você possa compará-los e mostra a pontuação de correspondência com a qual cada campo contribui para a pontuação de correspondência geral para os dois registros.  
  
5.  Exiba as estatísticas nas guias **Criador de perfil** e **Resultados de Correspondência** para assegurar que você esteja obtendo os resultados necessários. Clique na guia **Regras de Correspondência** para visualizar quais são as configurações de domínio para cada regra. Para obter mais informações, consulte [Guias Criador de Perfil e Resultados](#Tabs).  
  
6.  Se você não estiver satisfeito com os resultados de todas as regras, clique em **Voltar** para retornar à página **Política de Correspondência** , modifique uma ou mais regras conforme o necessário, volte à página **Resultados de Correspondência** e clique em **Reiniciar**.  
  
    > [!NOTE]  
    >  Após a conclusão da análise, o botão **Iniciar** se transforma em um botão **Reiniciar** . Se os resultados da análise anterior ainda não tiverem sido salvos, clicar em **Reiniciar** causará a perda dos dados anteriores.  
  
7.  Se você estiver satisfeito com os resultados de todas as regras, clique em **Concluir** para concluir o processo de política de correspondência e clique em um dos seguintes:  
  
    -   **Sim – Publique a base de dados de conhecimento e saia**: A base de conhecimento será publicada para uso do usuário atual ou de outros usuários. A base de dados de conhecimento não será bloqueada, o estado da base de dados de conhecimento (na tabela de bases de dados de conhecimento) será definido como vazio e as atividades de Gerenciamento de Domínio e Descoberta da Base de Dados de Conhecimento estarão disponíveis. Você será retornado à tela Abrir Base de Dados de Conhecimento.  
  
    -   **Não – Salve o trabalho na base de dados de conhecimento e saia**: Seu trabalho será salvo, a base de conhecimento permanecerá bloqueada e o estado da base de conhecimento será definido como **Em serviço**. As atividades de Gerenciamento de Domínio e Descoberta da Base de Dados de Conhecimento estarão disponíveis. Você será retornado à home page.  
  
    -   **Cancelar – Mantenha-se na tela atual**: O pop-up será fechado e você será retornado para a tela Gerenciamento de Domínio.  
  
8.  Clique em **Fechar** para salvar seu trabalho e retornar para a página inicial do DQS. O estado da base de dados de conhecimento mostrará a cadeia de caracteres “Política de Correspondência – “ e o estado atual. Se você clicou em **Fechar** quando estava na tela **Resultado de Correspondência** , o estado mostrará: "Política de Correspondência - Resultados". Se você clicou em Fechar quando estava na tela **Política de Correspondência** , o estado mostrará: "Política de Correspondência - Política de Correspondência". Depois de clicar em **Fechar**, para executar a atividade **Descoberta da Base de Dados de Conhecimento** , você terá que retornar à atividade **Política de correspondência** , clicar em **Concluir**e em **Sim** para publicar a base de dados de conhecimento ou **Não** para salvar o trabalho na base de dados de conhecimento e sair.  
  
    > [!NOTE]  
    >  Se você clicar em **Fechar** quando um processo de correspondência estiver em execução, o processo de correspondência não terminará quando clicar em **Fechar**. Você pode reabrir a base de dados de conhecimento e verificar se o processo ainda está em execução ou, caso tenha sido concluído, se os resultados foram exibidos. Se o processo não foi concluído, a tela exibirá o progresso.  
  
9. Clique em **Cancelar** para terminar a atividade Política de Correspondência, perder seu trabalho e retornar à página inicial do DQS.  
  
##  <a name="FollowUp"></a> Acompanhamento: após a criação de uma Política de Correspondência  
 Depois de criar uma política de correspondência, você pode executar um projeto de correspondência a partir da base de dados de conhecimento que contém a política de correspondência. Para obter mais informações, consulte [Executar um projeto de correspondência](../data-quality-services/run-a-matching-project.md).  
  
##  <a name="Tabs"></a> Guias Criador de Perfil e Resultados  
 As guias Criador de perfil e Resultados contêm estatísticas para as páginas Política de Correspondência e Resultados de Correspondência.  
  
###  <a name="Profiler"></a> Guia Criador de perfil  
 Clique na guia **Criador de perfil** para exibir estatísticas sobre o banco de dados de origem e para cada campo incluído na regra de política. As estatísticas serão atualizadas à medida que a regra de política for executada.  
  
 Para obter mais informações sobre como interpretar as estatísticas a seguir, consulte [Como definir parâmetros de regra de correspondência](#MatchingRules).  
  
 As estatísticas do banco de dados de origem incluem o seguinte:  
  
-   **Registros**: o número total de registros no banco de dados de origem  
  
-   **Valores Totais**: o número total de valores nos campos da fonte de dados  
  
-   **Novos Valores**: o número total de valores novos desde a execução anterior e seu percentual em relação ao todo  
  
-   **Valores Exclusivos**: o número total de valores exclusivos nos campos e seu percentual em relação ao todo  
  
-   **Novos Valores Exclusivos**: o número total de valores exclusivos novos nos campos e seu percentual em relação ao todo  
  
 As estatísticas de campo incluem o seguinte:  
  
-   **Nome do campo**  
  
-   **Nome do domínio**  
  
-   **Novo**: o número de novos valores e o percentual de novos valores em comparação com os valores existentes no domínio  
  
-   **Exclusivo**: o número de registros exclusivos no campo e seu percentual do total  
  
-   **Integridade**: a integridade de cada campo de origem mapeado para o exercício de correspondência  
  
###  <a name="Notifications"></a> Notificações de Política de Correspondência  
 Para a atividade de política de correspondência, as seguintes condições resultam em notificações:  
  
-   O campo está vazio em todos os registros; é recomendável eliminá-lo do mapeamento.  
  
-   A pontuação de integridade de campo é muito baixa; talvez você queira eliminá-lo do mapeamento.  
  
-   Todos os valores em um campo são inválidos; você deve verificar o mapeamento e a relevância das regras de domínio para o conteúdo do campo.  
  
-   Há um nível baixo de valores válidos no campo; você deve verificar o mapeamento e a relevância das regras de domínio para o conteúdo do campo.  
  
-   Há um nível alto de exclusividade neste campo. O uso desse campo na política de correspondência pode diminuir os resultados correspondentes.  
  
###  <a name="ResultsTab"></a> Guia Resultados Correspondentes  
 Clique na guia **Resultados de Correspondência** para exibir estatísticas para a execução da regra de política de correspondência e a execução da regra anterior. Se você executou a mesma regra mais de uma vez com parâmetros diferentes, a tabela de resultados de correspondência exibirá estatísticas de ambas as execuções, permitindo a comparação delas. Você também poderá restaurar a regra anterior se quiser.  
  
 As estatísticas incluem o seguinte:  
  
-   O número total de registros no banco de dados  
  
-   O número total de registros de correspondência no banco de dados  
  
-   O número de registros no banco de dados que não são considerados duplicatas  
  
-   O número de clusters descobertos  
  
-   O tamanho médio do cluster (número de registros duplicados dividido pelo número de clusters)  
  
-   O menor número de duplicatas em um cluster  
  
-   O maior número de duplicatas em um cluster  
  
  

