---
title: "Executar um projeto de correspond&#234;ncia | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "data-quality-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dqs.matchingproject.map.f1"
  - "sql13.dqs.matchingproject.matching.f1"
  - "sql13.dqs.matchingproject.export.f1"
ms.assetid: 6aa9d199-83ce-4b5d-8497-71eef9258745
caps.latest.revision: 36
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 36
---
# Executar um projeto de correspond&#234;ncia
  Este tópico descreve como executar a correspondência de dados no [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS). O processo de correspondência identifica clusters de registros de correspondência com base em regras de correspondência na política de correspondência, designa um registro de cada cluster como o sobrevivente com base em uma regra de sobrevivência, e exporta os resultados. O DQS executa o processo de correspondência, também chamado de eliminação de duplicação, em um processo assistido por computador, mas você cria regras de correspondência interativamente e seleciona a regra de correspondência a partir de várias opções; assim, você controla o processo de correspondência.  
  
 A correspondência é executada em três etapas: um processo de mapeamento no qual você identifica a fonte de dados e mapeia domínios para a fonte de dados, um processo de correspondência no qual você executa a análise de correspondência, e um processo de sobrevivência e exportação no qual você designa a regra de sobrevivência e exporta os resultados correspondentes. Cada um desses processos é executado em uma página separada do assistente da atividade de correspondência, permitindo que você percorra páginas diferentes, para executar o processo novamente e fechar um processo de correspondência específico e, depois, retornar ao mesmo estágio do processo. O DQS fornece estatísticas sobre a fonte de dados, as regras de correspondência e os resultados correspondentes que permitem a você tomar decisões conscientes sobre a correspondência e refinar o processo de correspondência.  
  
 Você deve se preparar para a correspondência, criando uma política de correspondência com uma ou mais regras de correspondência e executando a política em dados de exemplo. O processo de projeto de correspondência está separado do processo de política de correspondência, e uma base de dados de conhecimento não é populada com o conhecimento de correspondência obtido do projeto de correspondência. Para obter mais informações sobre como criar uma política de correspondência, consulte [Create a Matching Policy](../data-quality-services/create-a-matching-policy.md).  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Prerequisites"></a> Pré-requisitos  
  
-   Você deve ter criado uma base de dados de conhecimento com uma política de correspondência que consiste em uma ou mais regras de correspondência.  
  
-   O Microsoft Excel deverá ser instalado no computador [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] se os dados de origem a serem correspondidos estiverem em um arquivo do Excel. Caso contrário, você não poderá selecionar o arquivo do Excel no estágio de mapeamento. Os arquivos criados pelo Microsoft Excel podem ter a extensão .xlsx, .xls ou .csv. Se a versão de 64 bits do Excel for usada, somente arquivos do Excel 2003 (.xls) terão suporte; não haverá suporte para os arquivos do Excel 2007 ou 2010 (.xlsx). Se você estiver usando a versão de 64 bits do Excel 2007 ou 2010, salve o arquivo como .xls ou .csv ou instale uma versão de 32 bits do Excel.  
  
###  <a name="Security"></a> Segurança  
  
####  <a name="Permissions"></a> Permissões  
 Você deve ter a função dqs_kb_editor ou dqs_administrator no banco de dados DQS_MAIN para executar um projeto de correspondência.  
  
##  <a name="StartingaMatchingProject"></a> Primeira etapa: iniciando uma projeto de correspondência  
 Você executa a atividade de correspondência em um projeto de qualidade de dados criado no aplicativo cliente DQS.  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)] [Executar o aplicativo de cliente de qualidade de dados](../data-quality-services/run-the-data-quality-client-application.md).  
  
2.  Na tela inicial do [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] , clique em **Novo Projeto de Qualidade de Dados** para executar a correspondência em um novo projeto de qualidade de dados. Insira um nome para o projeto de qualidade de dados, insira uma descrição e selecione a base de dados conhecimento a ser usada para correspondência em **Usar base de dados de conhecimento**. Clique em **Correspondência** da atividade. Clique em **Avançar** para prosseguir para o estágio de mapeamento.  
  
3.  Clique em **Abrir projeto de qualidade de dados** para fazer a correspondência em um projeto existente de qualidade de dados. Selecione o projeto e clique em **Avançar**. (Ou você pode clicar em um projeto sob **Projeto de qualidade de dados recente**.) Se você abrir um projeto de correspondência que foi fechado, prosseguirá para o estágio de atividade de projeto de correspondência foi fechada (conforme indicado pelo **estado** coluna na tabela de projetos ou no nome do projeto em **projeto de qualidade de dados recente**). Se você abrir um projeto de correspondência que foi concluído, você passará para o **exportar** página (e não poderá voltar para as telas anteriores).  
  
##  <a name="MappingStage"></a> Estágio de mapeamento  
 No estágio de mapeamento, identifique a origem dos dados nos quais você executará a correspondência e mapeie colunas de origem para domínios para disponibilizar os domínios para a atividade de política de correspondência.  
  
1.  Na página **Mapa** , para executar a correspondência em um banco de dados, deixe **Fonte de Dados** como **SQL Server**, selecione o banco de dados no qual deseja executar a correspondência e selecione a tabela. O banco de dados de origem deve estar presente na mesma instância do SQL Server que o servidor do DQS. Caso contrário, ele não será exibido na lista suspensa.  
  
2.  Para executar a correspondência nos dados em uma planilha do Excel, selecione **Arquivo do Excel** para **Fonte de Dados**, clique em **Procurar** e selecione o arquivo do Excel, deixando a opção **Usar primeira linha como cabeçalho** selecionada, caso apropriado. Em **Planilha**, selecione a planilha no arquivo do Excel que será a origem dos dados. O Excel deve ser instalado no computador do [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] para selecionar um arquivo do Excel. Se o Excel não estiver instalado no computador do [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] , o botão **Procurar** não estará disponível e você será notificado abaixo dessa caixa de texto que o Excel não está instalado.  
  
3.  Em **Mapeamentos**, selecione um campo na fonte de dados para **Coluna de Origem**e selecione o domínio correspondente. Repita para todos os domínios que você usa no processo de correspondência. Cada domínio que é definido na política de comparação deve ser mapeado para a coluna de origem apropriada. A página Mapa exibe os domínios que foram definidos na política de comparação e as regras na política de comparação no painel da direita.  
  
    > [!NOTE]  
    >  Você poderá mapear sua fonte de dados para um domínio DQS somente se o tipo de dados de origem tiver suporte no DQS e corresponder ao tipo de dados de domínio do DQS. Para obter mais informações sobre tipos de dados que oferecem suporte no DQS, consulte [Supported SQL Server and SSIS Data Types for DQS Domains](../data-quality-services/supported-sql-server-and-ssis-data-types-for-dqs-domains.md).  
  
4.  Clique o **mais (+)** controle para adicionar uma linha à tabela mapeamentos ou **menos (-)** controle para remover uma linha.  
  
5.  Clique em **Visualizar fonte de dados** para visualizar os dados na tabela do SQL Server ou visualizar os dados selecionados ou a planilha do Excel selecionada.  
  
6.  Clique em **Exibir/Selecionar domínios compostos** para exibir uma lista de domínios compostos disponíveis na base de dados de conhecimento e selecione conforme apropriado para mapeamento.  
  
7.  Clique em **Avançar** para prosseguir para o estágio de correspondência.  
  
    > [!NOTE]  
    >  Clique em **Fechar** para salvar o estágio do projeto correspondente e retornar à página inicial do DQS. Na próxima vez que abrir este projeto, você iniciará no mesmo estágio. Clique em **Cancelar** para terminar a atividade de correspondência, perder seu trabalho e retornar à página inicial do DQS.  
  
##  <a name="MatchingStage"></a> Estágio de correspondência  
 Neste estágio, você executa um processo de correspondência assistido por computador que mostra quantas correspondências existem nos dados de origem com base nas regras de correspondência. Este processo gerará uma tabela de resultados correspondentes que mostra os clusters identificados pelo DQS, cada registro no cluster com sua ID de registro e sua pontuação de correspondência e o registro principal inicial para o cluster. O registro principal no cluster é selecionado aleatoriamente. Você determina o registro sobrevivente selecionando a regra de sobrevivência na página **Exportar** ao executar o projeto de correspondência. Cada linha adicional em um cluster é considerada uma correspondência; sua pontuação correspondente (em comparação com o registro principal) é fornecida na tabela de resultados. O número do cluster é igual à ID do registro principal no cluster.  
  
 Nos resultados correspondentes, você pode filtrar os dados desejados e rejeitar as correspondências não desejadas. Também é possível exibir os dados de criação de perfil do processo de correspondência como um todo, as especificações sobre as regras de correspondência que se aplicam e as estatísticas sobre os resultados correspondentes como um todo. O processo de correspondência pode identificar clusters sobrepostos e não sobrepostos e, se for executado várias vezes, pode ser executado em dados recém-copiados da origem e reindexados, ou em dados anteriores.  
  
1.  Sobre o **página correspondência**, selecione **sobrepostos clusters** na lista suspensa para exibir os registros dinâmicos e registros a seguir para todos os clusters quando a correspondência é executada, mesmo que grupos de clusters tenham registros em comum. Selecione **Clusters não sobrepostos** para exibir clusters que tenham registros em comum como um cluster único quando a correspondência for executada.  
  
2.  Clique em **recarregar os dados da origem** (o padrão) para copiar dados da fonte de dados na tabela de preparação e reindexá-los quando você executar o projeto de correspondência. Clique em **executar nos dados anteriores** para executar um projeto de correspondência sem copiar os dados na tabela de preparação e reindexar os dados. A opção**Executar nos dados anteriores** está desabilitada para a primeira execução do projeto de correspondência ou se você alterar o mapeamento na página **Mapa** e depois pressionar **Sim** no pop-up seguinte. Em ambos os casos, você deverá reindexar. Não será necessário reindexar se o projeto de correspondência não tiver sido alterado. A execução nos dados anteriores pode ajudar no desempenho.  
  
3.  Clique em **Iniciar** para executar a correspondência na fonte de dados selecionada.  
  
4.  Clique em **Parar** se você desejar parar o projeto de correspondência e descartar os resultados.  
  
5.  Após a conclusão do processo de correspondência, verifique se os clusters na tabela **Resultados Correspondentes** são apropriados, e exiba as estatísticas nas guias **Criador de Perfil** e **Resultados Correspondentes** para verificar se você está obtendo os resultados necessários. Exiba os registros correspondentes selecionando **Correspondente** em **Filtro** ou exiba registros não correspondentes selecionando **Sem correspondência**.  
  
6.  Se você tiver várias regras de correspondência na política de correspondência, clique na guia **Regras de Correspondência** para identificar o ícone para cada regra e, depois, verifique qual regra identificou um registro como uma correspondência, identificando a regra na coluna **Regra** da tabela **Resultados Correspondentes** .  
  
7.  Se você selecionar um registro não dinâmico na tabela e clique no **Exibir detalhes** ícone (ou clique duas vezes o registro), o DQS exibirá um **detalhes da pontuação de correspondência** pop-up que exibe o registro clicado duas vezes e seu registro dinâmico (e os valores em todos os campos), a pontuação entre eles e uma busca detalhada da correspondência de pontuação contribuições de cada campo. Ao clicar duas vezes em um registro dinâmico, você não exibirá o pop-up.  
  
8.  Clique no ícone **Recolher Tudo** para recolher os registros exibidos na tabela **Resultados Correspondentes** para incluir apenas o registro dinâmico, e não os registros duplicados. Clique em **Expandir Tudo** para expandir os registros exibidos na tabela Resultados Correspondentes para incluir todos os registros duplicados.  
  
9. Para rejeitar um registro dos resultados correspondentes, clique na caixa de seleção **Rejeitado** para o registro.  
  
10. Para alterar a pontuação mínima correspondente que determina o nível de correspondência deve ter um registro a ser exibido, selecione o **Min. Pontuação de correspondência** ícone acima do lado direito da tabela e insira um número mais alto. A pontuação mínima de correspondência é definida por padrão em 80%. Clique em **Atualizar** para alterar o conteúdo da tabela.  
  
11. Após a conclusão da análise, o botão **Iniciar** se transforma em um botão **Reiniciar** . Clique em **Reiniciar** para executar o projeto de análise novamente. No entanto, os resultados da análise anterior ainda não foram salvos; portanto, clicar em **Reiniciar** ocasionará a perda dos dados anteriores. Para continuar, clique em **Sim** na janela pop-up. Durante a execução da análise, não saia da página; do contrário, o processo de análise será encerrado.  
  
12. Clique em **Avançar** para prosseguir para o estágio de sobrevivência e exportação.  
  
##  <a name="SurvivorshipandExportStage"></a> Estágio de sobrevivência e exportação  
 No processo de sobrevivência, os Data Quality Services determinam um registro de sobrevivente para cada cluster, que substituirá os outros registros que correspondem a ele no cluster. Ele exporta os resultados da correspondência e/ou sobrevivência para uma tabela no banco de dados do SQL Server, um arquivo .csv ou um arquivo do Excel.  
  
 A sobrevivência é opcional. Você pode exportar os resultados sem executar a sobrevivência; nesse caso, o DQS usaria o registro dinâmico que foi designado na análise correspondente. Se dois ou mais registros em um cluster obedecerem a regra de sobrevivência, o processo de sobrevivência selecionará a menor ID de registro entre os registros conflitantes para ser a sobrevivente. Você pode exportar os sobreviventes para arquivos ou tabelas diferentes usando regras de sobrevivência diferentes.  
  
1.  Na página **Exportar** , selecione o destino para onde você deseja exportar os dados correspondentes em **Tipo de Destino**: **SQL Server**, **Arquivo CSV**ou **Arquivo do Excel**.  
  
    > [!IMPORTANT]  
    >  Se você estiver usando uma versão de 64 bits do Excel, não poderá exportar os dados compatíveis para um arquivo do Excel; você só poderá exportar para um banco de dados do SQL Server ou para um arquivo .csv.  
  
2.  Se você selecionou **SQL Server** para **Tipo de Destino**, selecione o banco de dados para exportar os resultados em **Nome de Banco de Dados**.  
  
    > [!IMPORTANT]  
    >  O banco de dados de destino deve estar presente na mesma instância do SQL Server que o servidor do DQS. Caso contrário, ele não será exibido na lista suspensa.  
  
3.  Marque a caixa de seleção **resultados correspondentes** para exportar resultados correspondentes (consulte acima para obter uma explicação) para a tabela designada em um banco de dados do SQL Server ou para o arquivo do Excel ou designado. csv. Marque a caixa de seleção **resultados de sobrevivência** para exportar resultados de sobrevivência (consulte acima para obter uma explicação) para a tabela designada em um banco de dados do SQL Server ou para o arquivo do Excel ou designado. csv.  
  
     Isto será exportado para resultados correspondentes:  
  
    -   Uma lista de clusters e os registros correspondentes em cada cluster, inclusive o nome de regra e a contagem. O registro dinâmico será marcado como "Dinâmico". Os clusters aparecerão primeiro na lista de exportação.  
  
    -   Uma lista dos registros sem correspondência, com “NULL” nas colunas Pontuação e Nome da Regra. Esses registros serão anexados à lista de exportação depois dos clusters.  
  
     Isto será exportado para resultados de sobrevivência:  
  
    -   Uma lista dos registros sobreviventes, conforme determinado pelo processo de sobrevivência, de acordo com a regra de sobrevivência. Esses registros aparecem primeiro na lista de exportação.  
  
    -   Uma lista dos registros sem correspondência que não são incluídos nos clusters de registros correspondentes. Esses registros são adicionados depois dos resultados de sobreviventes.  
  
4.  Se você selecionou **SQL Server** para **Tipo de Destino**, insira o nome das tabelas para onde deseja exportar os resultados em **Nome da Tabela**. Se você exportar resultados correspondentes e resultados de sobrevivência, as tabelas de destino deverão ter nomes diferentes que são exclusivos do banco de dados.  
  
5.  Se você selecionou **Arquivo CSV** para **Tipo de Destino**, insira o arquivo e o caminho do arquivo CSV para onde deseja exportar em **Arquivo CSV**.  
  
6.  Se você selecionou **Arquivo do Excel** para **Tipo de Destino**, insira o arquivo e o caminho do arquivo do Excel para onde deseja exportar em **Nome de Arquivo do Excel**. Você não poderá exportar para um arquivo do Excel se estiver usando uma versão de 64 bits do Excel.  
  
7.  Selecione a regra de sobrevivência da seguinte forma:  
  
    -   Selecione **dinamizar registro** (o padrão) para identificar o registro sobrevivente como o registro dinâmico inicial escolhido arbitrariamente pelo DQS.  
  
    -   Selecione **Registro mais completo e mais longo** para identificar o registro sobrevivente como aquele com o maior número de campos populados e com o maior número de termos em cada campo. Todos os campos de origem são verificados, até mesmo os campos que não foram mapeados para um domínio na página **Mapa** .  
  
    -   Selecione **Registro mais completo** para identificar o registro sobrevivente como aquele com o maior número de campos populados. Um campo populado contém pelo menos um valor (cadeia de caracteres, numérico ou ambos). Todos os campos de origem são verificados, até mesmo os campos que não foram mapeados para um domínio na página Mapa. Um campo populado contém pelo menos um valor (cadeia de caracteres, numérico ou ambos).  
  
    -   Selecione **Registro mais longo** para identificar o registro sobrevivente como aquele com o maior número de termos em seus campos de origem. Para determinar o comprimento de cada registro, o DQS verifica o comprimento dos termos em todos os campos de origem, até mesmo nos campos que não foram mapeados para um domínio na página **Mapa** .  
  
8.  Exiba as estatísticas na guia **Criador de Perfil** para garantir que você está obtendo os resultados necessários.  
  
9. Clique em **Exportar** para exportar os resultados. Isso exibe uma caixa de diálogo Exportação de Correspondência que mostra o progresso e os resultados da exportação.  
  
    -   Se você selecionou **SQL Server** como o destino de dados, uma nova tabela com o nome especificado será criada no banco de dados selecionado.  
  
    -   Se você selecionou **Arquivo CSV** como o destino de dados, um arquivo .csv será criado no local no computador [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] com o nome do arquivo especificado antes na caixa **Nome do arquivo Csv** .  
  
    -   Se você selecionou **Arquivo do Excel** como o destino de dados, um arquivo .xlsx será criado no local no computador [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] com o nome do arquivo especificado antes na caixa **Nome do arquivo do Excel** .  
  
10. Verifique se a exportação foi concluída com êxito e clique em **Fechar**.  
  
11. Clique em **Concluir** para concluir a projeto de correspondência.  
  
    > [!NOTE]  
    >  Se você concluiu um projeto de correspondência e o utilizou novamente, ele usará a base de dados de conhecimento existente quando ele foi publicado. Ele não usará as alterações feitas na base de dados de conhecimento desde a conclusão do projeto. Para usar essas alterações, ou para usar uma nova base de dados de conhecimento, você terá que criar um novo projeto de correspondência. Por outro lado, se ele já foi criado, mas não concluído, um projeto de correspondência, quaisquer alterações publicadas na política de correspondência serão usados se você executar a correspondência no projeto.  
  
##  <a name="FollowUp"></a> Acompanhamento: após executar um projeto de correspondência  
 Depois executar uma projeto de correspondência, você pode alterar a política de correspondência na base de dados de conhecimento, e criar e executar outro projeto de correspondência com base na política de correspondência atualizada. Para obter mais informações, consulte [Create a Matching Policy](../data-quality-services/create-a-matching-policy.md).  
  
##  <a name="Profiler"></a> Guias Criador de Perfil e Resultados  
 As guias Criador de Perfil e Resultados contêm estatísticas para o processo de correspondência.  
  
### Guia Criador de perfil  
 Clique na guia **Criador de perfil** para exibir estatísticas sobre o banco de dados de origem e para cada campo incluído na regra de política. As estatísticas serão atualizadas à medida que a regra de política for executada. A criação de perfis o ajuda a avaliar a eficácia do processo de eliminação de duplicação, ajudando a determinar até que ponto o processo pode melhorar a qualidade dos dados. A precisão na criação de perfis não é importante para um projeto de correspondência.  
  
 As estatísticas do banco de dados de origem incluem o seguinte:  
  
-   **Registros**: o número total de registros no banco de dados  
  
-   **Valores Totais**: o número total de valores nos campos  
  
-   **Novos Valores**: o número total de valores novos desde a execução anterior e seu percentual em relação ao todo  
  
-   **Valores Exclusivos**: o número total de valores exclusivos nos campos e seu percentual em relação ao todo  
  
-   **Novos Valores Exclusivos**: o número total de valores exclusivos novos nos campos e seu percentual em relação ao todo  
  
 As estatísticas de campo incluem o seguinte:  
  
-   **Campo**: nome do campo que foi incluído nos mapeamentos.  
  
-   **Domínio**: o nome do domínio que foi mapeado para o campo.  
  
-   **Novo**: o número de novas correspondências localizadas e sua porcentagem do total  
  
-   **Exclusivo**: o número de registros exclusivos no campo e seu percentual do total  
  
-   **Integridade**: a porcentagem de conclusão da execução da regra.  
  
### Notificações de Política de Correspondência  
 Para a atividade de política de correspondência, as seguintes condições resultam em notificações:  
  
-   O campo está vazio em todos os registros; é recomendável eliminá-lo do mapeamento.  
  
-   A pontuação de integridade de campo é muito baixa; talvez você queira eliminá-lo do mapeamento.  
  
-   Todos os valores em um campo são inválidos; você deve verificar o mapeamento e a relevância das regras de domínio para o conteúdo do campo.  
  
-   Há um nível baixo de valores válidos no campo; você deve verificar o mapeamento e a relevância das regras de domínio para o conteúdo do campo.  
  
-   Há um nível alto de exclusividade neste campo. O uso desse campo na política de correspondência pode diminuir os resultados correspondentes.  
  
### Guia Regras de Correspondência  
 Clique nesta guia para exibir uma lista das regras na política de correspondência e as condições em uma regra.  
  
 **Lista de regras**  
 Exibe uma lista de todas as regras de correspondência na política de correspondência. Selecione uma das regras para exibir as condições na regra na tabela de Regra de Correspondência.  
  
 **Tabela Regra de Correspondência**  
 Exibe cada condição na regra selecionada, inclusive domínio, valor de semelhança, peso e seleção pré-requisitada.  
  
### Guia Resultados Correspondentes  
 Clique na guia **Resultados Correspondentes** para exibir estatísticas para a análise da fonte de dados que usa o conhecimento selecionado para o projeto e as regras de correspondência nessa base de dados de conhecimento. As estatísticas incluem o seguinte:  
  
-   O número total de registros no banco de dados  
  
-   O número total de registros de correspondência no banco de dados  
  
-   O número de registros no banco de dados que não são considerados duplicatas  
  
-   O número de clusters descobertos  
  
-   O tamanho médio do cluster (número de registros duplicados dividido pelo número de clusters)  
  
-   O menor número de duplicatas em um cluster  
  
-   O maior número de duplicatas em um cluster  
  
  