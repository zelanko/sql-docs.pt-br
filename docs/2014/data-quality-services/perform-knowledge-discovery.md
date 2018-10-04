---
title: Executar a descoberta de conhecimento | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- data-quality-services
ms.topic: conceptual
f1_keywords:
- sql12.dqs.kb.kbanalyze.f1
- sql12.dqs.kb.viewselectcd.f1
- sql12.dqs.kb.kbmap.f1
- sql12.dqs.kb.kbterms.f1
ms.assetid: 34a0ea16-02e6-46ed-90bc-dede68687f63
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: a0c7809182a67707055cb595ed2dc9a51a0067b2
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48076046"
---
# <a name="perform-knowledge-discovery"></a>Executar a descoberta da base de dados de conhecimento
  Este tópico descreve como criar uma base de dados de conhecimento através da descoberta da base de dados de conhecimento. No processo de descoberta, o [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS) analisa os dados em uma fonte de dados de exemplo através de um processo assistido por computador e adiciona o conhecimento obtido na base de dados de conhecimento. Esse conhecimento pode ser modificado e aprimorado na etapa **Gerenciar Valores de Domínio** da atividade de descoberta da base de dados de conhecimento ou na atividade de gerenciamento de domínio.  
  
 A descoberta da base de dados de conhecimento é um processo controlado por assistente que inclui três etapas, que devem ser concluídas.  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Prerequisites"></a> Pré-requisitos  
 O Microsoft Excel deverá ser instalado no computador do [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] se os dados de origem nos quais você está executado a descoberta estiverem em um arquivo do Excel. Caso contrário, você não poderá selecionar o arquivo do Excel no estágio de mapeamento. Os arquivos criados pelo Microsoft Excel podem ter a extensão .xlsx, .xls ou .csv. Se a versão de 64 bits do Excel for usada, somente arquivos do Excel 2003 (.xls) terão suporte; não haverá suporte para os arquivos do Excel 2007 ou 2010 (.xlsx). Se você estiver usando a versão de 64 bits do Excel 2007 ou 2010, salve o arquivo como .xls ou .csv ou instale uma versão de 32 bits do Excel.  
  
###  <a name="Security"></a> Segurança  
  
####  <a name="Permissions"></a> Permissões  
 Você deve ter a função dqs_kb_editor ou dqs_administrator no banco de dados DQS_MAIN para criar uma base de dados de conhecimento.  
  
##  <a name="FirstStep"></a> Primeiro etapa: Iniciar descoberta da base de dados de conhecimento  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)] [Executar o aplicativo Data Quality Client](../../2014/data-quality-services/run-the-data-quality-client-application.md).  
  
2.  Para executar a descoberta em uma nova base de dados de conhecimento, clique em **Nova base de dados de conhecimento**, insira o nome e a descrição, e especifique para que você está criando a base de dados de conhecimento, se aplicável. Para executar a descoberta da base de dados de conhecimento em uma base de dados de conhecimento existente, clique em **Abrir base de dados de conhecimento**e selecione uma base de dados de conhecimento.  
  
3.  Selecione **Descoberta da Base de Dados de Conhecimento** como a atividade e clique em **Criar** para criar a nova base de dados de conhecimento ou em **Abrir** para abrir uma base de dados de conhecimento existente.  
  
##  <a name="Mapping"></a> Estágio de mapeamento  
  
1.  No campo **Fonte de Dados** , selecione **SQL Server** (o padrão) ou **Arquivo do Excel**.  
  
    > [!NOTE]  
    >  Nessa página, você estabelece uma conexão com uma fonte de dados do SQL Server ou do Excel e faz o mapeamento entre as colunas da fonte de dados e um domínio na base de dados de conhecimento. A tabela Mapeamentos exibe todas as colunas do banco de dados de origem que serão analisadas para adicionar conhecimento aos domínios correspondentes. São feitos mapeamentos entre as colunas da fonte de dados e um domínio da base de dados de conhecimento.  
  
2.  Se a fonte de dados for o **SQL Server**, faça o seguinte:  
  
    1.  No campo **Banco de Dados** , selecione o banco de dados de origem que será analisado para criar a base de dados de conhecimento. A caixa de texto suspensa listará os bancos de dados que estão disponíveis. O banco de dados de origem deve estar presente na mesma instância do SQL Server que o [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)]. Caso contrário, ele não será exibido na lista suspensa.  
  
    2.  No campo **Tabela/Exibição** , selecione a tabela ou exibição que você deseja analisar para criar a base de dados de conhecimento. Esta tabela ou exibição deve ser dados de exemplo, e não um banco de dados de origem inteiro no qual a limpeza ou correspondência de dados está sendo executada. A caixa de texto suspensa listará as tabelas e exibições que estão disponíveis para o banco de dados selecionado.  
  
3.  Se a fonte de dados for o **Excel**, faça o seguinte:  
  
    1.  Clique em **Procurar** e selecione o arquivo do Excel que será analisado para criar a base de dados de conhecimento. O Excel deve ser instalado no computador do [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] para selecionar um arquivo do Excel. Se o Excel não estiver instalado no computador do [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] , o botão Procurar não estará disponível e você será notificado abaixo dessa caixa de texto que o Excel não está instalado.  
  
    2.  Marque a caixa de seleção **Usar primeira linha como cabeçalho** se a primeira linha do arquivo do Excel contiver dados de cabeçalho.  
  
4.  Na tabela **Mapeamentos** , mapeie cada coluna de origem na qual deseja executar a descoberta de dados de conhecimento para um domínio da base de dados de conhecimento, da seguinte maneira:  
  
    1.  Crie um mapeamento selecionando uma coluna de origem na lista suspensa da coluna **Coluna de Origem** de uma linha vazia e, em seguida, selecionando um domínio na lista suspensa da coluna **Domínio** na mesma linha, caso exista um domínio. Se não existir nenhum domínio, clique em **Criar um domínio** ou **Criar um domínio composto** para criar um domínio. Para obter mais informações, consulte [Criar uma regra de domínio](../../2014/data-quality-services/create-a-domain-rule.md) ou [Criar um domínio composto](../../2014/data-quality-services/create-a-composite-domain.md).  
  
    2.  Repita a etapa anterior para cada mapeamento. Para alterar o número de linhas na tabela, clique em **Adicionar um mapeamento de coluna**ou selecione uma linha e clique em **Remover o mapeamento de coluna selecionado**. Se você clicar em **Remover o mapeamento de coluna selecionado** quando uma linha populada estiver selecionada, a linha selecionada será excluída mesmo que exista uma linha não populada.  
  
        > [!NOTE]  
        >  Você poderá mapear sua fonte de dados para um domínio DQS para realizar descoberta de conhecimento somente se o tipo de dados de origem tiver suporte no DQS e corresponder ao tipo de dados de domínio do DQS. Para obter mais informações sobre os tipos de dados com suporte, consulte [O SQL Server com suporte e tipos de dados do SSIS para domínios do DQS](../../2014/data-quality-services/supported-sql-server-and-ssis-data-types-for-dqs-domains.md).  
  
    3.  Clique em **Exibir/selecionar domínios compostos** para exibir os domínios compostos que foram definidos. Se nenhum domínio composto foi definido, o controle não estará disponível.  
  
    4.  Clique em **Visualizar fonte de dados** para exibir uma janela popup com todos os dados da fonte de dados selecionada na caixa de texto de **Tabela/Exibição** ou **Arquivo do Excel** .  
  
5.  Clique em **Avançar** para passar para a página **Descobrir** do assistente de Descoberta da Base de Dados de Conhecimento. Também é possível selecionar o seguinte:  
  
    -   Clique em **Cancelar** para encerrar a atividade de Descoberta da Base de Dados de Conhecimento, o que resultará na perda do trabalho, e retornar à home page do DQS.  
  
    -   Clique em **Fechar** para retornar à home page do DQS enquanto salva o trabalho. A base de dados de conhecimento ficará bloqueada para você, e o estado da base de dados de conhecimento da tabela de bases de dados de conhecimento na tela **Abrir Base de Dados de Conhecimento** será **Descoberta - Mapeamento**. Depois de clicar em **Fechar**para executar a atividade de Gerenciamento de Domínio, você precisará clicar em **Descoberta da Base de Dados de Conhecimento** na tela **Abrir base de dados de conhecimento** , prosseguir para a tela **Gerenciamento da Base de Dados de Conhecimento: Gerenciar Termos do Domínio** , clicar em **Concluir**e, em seguida, clicar em **Sim** para publicar a base de dados de conhecimento ou em **Não** para salvar o trabalho na base de dados de conhecimento e sair.  
  
##  <a name="Discover"></a> Estágio de descoberta  
  
1.  Clique em **Iniciar** para analisar a fonte de dados.  
  
    > [!NOTE]  
    >  A descoberta é executada nas colunas inseridas na tabela **Mapeamentos** da página **Mapa** . O domínio mapeado para cada coluna será populado com o conhecimento extraído da descoberta. Se o domínio for um domínio composto, o conhecimento será adicionado aos domínios individuais que compõem o domínio composto.  
  
2.  Enquanto o processo de descoberta está em execução, verifique o status de conclusão exibido para cada etapa da descoberta: **Pré-processando Registros**, **Executando Regras de Domínio**e **Executando Descoberta**. As porcentagens de conclusão e o status da conclusão serão mostrado para cada um desses estágios.  
  
3.  Quando a análise for concluída, verifique se a linha de status abaixo das estatísticas de conclusão indica que ela foi concluída com êxito.  
  
    > [!NOTE]  
    >  Se você sair da tela antes que o arquivo seja carregado, o processo de carregamento de arquivo será encerrado.  
  
4.  Depois que a análise for concluída, verifique as estatísticas na guia **Criador de Perfil** para ver o status dos dados. Para obter mais informações, consulte **Criação de Perfil de Dados e Notificações no DQS**.  
  
5.  Após a conclusão da análise, o botão **Iniciar** se transforma em um botão **Reiniciar** . Clique **Reiniciar** para executar o processo de análise novamente. No entanto, os resultados da análise anterior ainda não foram salvos; portanto, clicar em **Reiniciar** ocasionará a perda dos dados anteriores. Para continuar, clique em **Sim** na janela pop-up. Durante a execução da análise, não saia da página; do contrário, o processo de análise será encerrado.  
  
6.  Clique em **Avançar** para passar para a página **Gerenciar Valores de Domínio** do assistente de Descoberta da Base de Dados de Conhecimento. Nessa página, você pode modificar o conhecimento adicionado aos domínios da base de dados de conhecimento. Também é possível selecionar o seguinte:  
  
    -   Clique em **Cancelar** para encerrar a atividade de Descoberta da Base de Dados de Conhecimento, o que resultará na perda do trabalho, e retornar à home page do DQS.  
  
    -   Clique em **Fechar** para retornar à home page do DQS enquanto salva o trabalho. A base de dados de conhecimento será bloqueada para você, e o estado da base de dados de conhecimento na tabela de bases de dados de conhecimento na tela **Abrir Base de Dados de Conhecimento** será **Descoberta - Descobrir**. Depois de clicar em **Fechar**para executar a atividade de Gerenciamento de Domínio, você precisará clicar em **Descoberta da Base de Dados de Conhecimento** na tela **Abrir base de dados de conhecimento** , prosseguir para a tela **Gerenciamento da Base de Dados de Conhecimento: Gerenciar Termos do Domínio** , clicar em **Concluir**e, em seguida, clicar em **Sim** para publicar a base de dados de conhecimento ou em **Não** para salvar o trabalho na base de dados de conhecimento e sair.  
  
    -   Clique para retornar à página **Descobrir** .  
  
##  <a name="Manage"></a> Estágio de gerenciamento dos resultados da descoberta de dados  
 Depois que você executar a atividade de descoberta da base de dados de conhecimento, poderá alterar os valores da seguinte maneira:  
  
-   Adicione um valor de domínio à lista de valores ou selecione um valor e exclua-o da lista  
  
-   Altere o status de um valor de domínio conforme designado pelo processo de descoberta do DQS, modificando-o para correto, em erro ou inválido  
  
-   Insira um valor substituto para um valor que está em erro ou é inválido  
  
-   Defina dois ou mais valores como sinônimos e altere o valor principal conforme definido pelo processo de descoberta, com o resultado que o valor principal substituirá o valor do sinônimo, caso a propriedade **Usar Valor Principal** tenha sido definida quando você criou o domínio  
  
-   Importar valores de domínio de um arquivo do Excel.  
  
 A tabela **Valor** exibe o conhecimento adicionado à base de dados de conhecimento para um domínio único. Você seleciona esse domínio na lista de domínios do painel à esquerda. As colunas do campo são as seguintes:  
  
-   A coluna **Valor** exibe todos os valores que o processo de descoberta adicionou ao domínio selecionado de um campo no exemplo de dados. Qualquer valor projetado como erro será mostrado como sinônimo de um valor projetado como correto.  
  
-   A coluna **Frequência** exibe o número de instâncias do valor no campo de banco de dados de exemplo para o qual o domínio é mapeado. Para um domínio composto, somente esses valores com uma frequência maior que ou igual a 20 são exibidos. Os dados de Frequência estão disponíveis porque o processo de descoberta da base de dados de conhecimento ainda tem uma conexão com o banco de dados de exemplo. Os dados de frequência não estão disponíveis na tabela de domínios na guia Valores do Domínio da tela Gerenciamento de Domínio porque o processo de gerenciamento de domínio não tem uma conexão com o banco de dados de exemplo.  
  
-   A coluna **Tipo** exibe o status do valor, conforme determinado pelo processo de descoberta. Uma marca de verificação verde indica que o valor está correto ou corrigido; uma cruz vermelha indica que o valor está com erro; um triângulo laranja com um ponto de exclamação indica que o valor é inválido. Um valor inválido não está em conformidade com os requisitos de dados do domínio. Um valor com erro pode ser válido, mas não é o valor correto para fins de dados.  
  
-   A coluna **Corrigir para** mostra um valor correto para o qual o valor original, marcado como erro ou inválido, será alterado. O DQS pode propor o valor correto como resultado do processo de descoberta.  
  
 Gerencie os resultados da descoberta da seguinte maneira:  
  
1.  No painel **Lista de Domínios** à esquerda, selecione um domínio para definir valores de domínio. Faça o seguinte para modificar os valores exibidos.  
  
    -   Exiba os resultados desejados na tabela, com base no status, selecionando o status na lista **Filtro** .  
  
    -   Localize os dados que você deseja verificar ou modificar inserindo uma ou mais letras a serem procuradas na caixa de texto Localizar. Isso realçará essas letras onde quer que eles ocorram em qualquer valor exibido.  
  
    -   Clique em **Mostrar Somente Novo** para restringir os valores exibidos na tabela somente aos valores que foram descobertos na sessão atual, e não nas sessões anteriores.  
  
    -   Clique no botão **Expandir Tudo** para exibir todos os valores em qualquer grupo de sinônimos quando o estado atual for recolhido ou clique no botão **Recolher Tudo** para ocultar todos os dados, menos o valor principal em qualquer grupo de sinônimos quando o estado atual for expandido.  
  
    -   Clique no botão **Mostrar/Ocultar o Painel de Histórico de Alterações de Valores de Domínio** para exibir uma visualização pop-up na parte inferior da tabela de valores que mostra as alterações recentes feitas na coleção de valores de domínio.  
  
2.  Localize qualquer correção proposta pelo Data Quality Services definindo **Filtro** como **Erro**. Verifique se o valor é mesmo um erro e se o valor na coluna **Corrigir para** é apropriado.  
  
3.  Defina **Filtro** como **Todos os Valores** e verifique se o estado dos valores é apropriado. Para alterar o estado de um valor, selecione o valor e clique no botão **Definir valores de domínio selecionados como corrigidos** (marca de verificação), no botão **Definir valores de domínio selecionados como erros** (cruz) ou no botão **Definir valores de domínio selecionados como inválidos** (triângulo).  
  
4.  Para alterar o estado de um valor, faça o seguinte:  
  
    1.  **Definir valores de domínio selecionados como corrigidos**: para alterar o estado de um valor de Erro ou Inválido para Correto, selecione o valor e clique em **Definir valores de domínio selecionados como corrigidos** (marca de verificação) na seta para baixo da barra de ícones ou na lista suspensa de Tipo. Se o valor com erro ou inválido for agrupado com um valor correto, exclua esse valor após a operação.  
  
    2.  **Definir valores de domínio selecionados como erros**: para alterar o estado de um valor de Correto ou Inválido para Erro, selecione o valor e clique no ícone **Definir valores de domínio selecionados como erros** (cruz) na seta para baixo da barra de ícones ou na lista suspensa de Tipo. Insira uma correção na coluna **Corrigir para** ou deixe em branco.  
  
    3.  **Definir valores de domínio selecionados como inválidos**: para alterar o estado de um valor de Correto ou Erro para Inválido, selecione o valor e clique no ícone **Definir valores de domínio selecionados como inválidos** (triângulo) na seta para baixo da barra de ícones ou na lista suspensa de Tipo. Insira uma correção na coluna **Corrigir para** ou deixe em branco.  
  
    4.  **Corrigir para:** Após definir um valor como erro ou inválido, insira um novo valor na coluna **Corrigir para** . O DQS adicionará uma nova linha para o valor substituto, o designará como correto e agrupará os dois valores. O novo valor será mostrado como o valor principal, com o valor principal em negrito e o valor com erro ou inválido recuado.  
  
5.  Para designar valores como um grupo de sinônimos, selecione diversos valores corretos e continue da seguinte maneira:  
  
    -   **Definir valores de domínio selecionados como sinônimos**: clique para definir os valores selecionados como sinônimos. O DQS designará um dos valores como o valor principal que substituirá os outros.  
  
        > [!NOTE]  
        >  Se você selecionar dois ou mais valores em um grupo e outro valor fora do grupo, e defini-los como sinônimos, você obterá uma mensagem de erro incorreta. Após fechar a mensagem de erro pop-up, os valores serão definidos corretamente como sinônimos.  
  
    -   **Quebrar relação entre os sinônimos selecionados**: clique para desfazer a designação de sinônimo.  
  
    -   **Definir valores de domínio selecionados como um valor principal de seu grupo**: altere o valor principal do grupo selecionando um valor no grupo que não esteja designado como valor principal e clicando no botão **Definir valores de domínio selecionados como um valor principal de seu grupo** .  
  
6.  **Verificador Ortográfico**: se você tiver habilitado o Verificador Ortográfico na página Propriedades de Domínio, localize qualquer valor que tenha um sublinhado vermelho ondulado, a indicação de que o Verificador Ortográfico está sugerindo uma correção. Clique com o botão direito do mouse no valor com sublinhado e selecione uma correção, caso ela se aplique. O tipo de valor se torna (ou permanece como) um erro, e a correção será adicionada à coluna **Corrigir para** . Clique na seta para baixo para ver outras correções propostas. Insira uma correção manualmente para adicioná-la ao dicionário do Verificador Ortográfico para que você possa selecioná-la como uma correção. Para obter mais informações, consulte [Usar o verificador ortográfico DQS](../../2014/data-quality-services/use-the-dqs-speller.md) e [Definir propriedades de domínio](../../2014/data-quality-services/set-domain-properties.md).  
  
    > [!NOTE]  
    >  Para usar o Verificador Ortográfico, você pode habilitá-lo na página **Propriedades de Domínio** ou, se ele estiver desabilitado na página **Propriedades de Domínio** , você poderá clicar no ícone **Habilitar/Desabilitar o Verificador Ortográfico** na página **Gerenciar Resultados de Descoberta de Dados** para habilitá-lo nessa página.  
  
7.  **Adicionar novo valor de domínio**: adicione um novo valor ao domínio clicando no botão **Adicionar novo valor de domínio** para adicionar uma linha ao fim da tabela. Depois que você inserir um valor, a linha será reposicionada em ordem alfabética.  
  
8.  **Importar valores de domínio do Excel**: adicione novos valores de uma planilha do Excel clicando na seta para baixo do ícone **Importar Valores** e selecionando **Importar valores de domínio do Excel**. Insira o nome de arquivo, selecione **Usar primeira linha como cabeçalho** , se apropriado, e clique em **OK**. Para obter mais informações, consulte [Importar valores de um arquivo do Excel para um domínio](../../2014/data-quality-services/import-values-from-an-excel-file-into-a-domain.md).  
  
9. **Importar valores de projeto**: adicione novos valores de um projeto de qualidade de dados clicando na seta para baixo do ícone **Importar Valores** e selecionando **Importar valores de projeto**. Insira o nome de arquivo, selecione **Usar primeira linha como cabeçalho** , se apropriado, e clique em **OK**. Selecione o projeto a partir do qual você importará valores e clique em **OK**. Os valores importados serão exibidos. Clique em **Concluir**. Para obter mais informações, consulte Importar valores de projeto para um domínio.  
  
10. **Excluir valores de domínio selecionados**: remova um ou mais valores existentes do domínio selecionando os valores e clicando no botão **Excluir valores de domínio selecionados** . A entrada DQS_NULL não pode ser excluída; portanto, se você escolher diversos valores para serem excluídos, e a entrada DQS_NULL for um deles, a operação falhará.  
  
11. Clique em **Concluir** para concluir a atividade de descoberta da base de dados de conhecimento. Uma janela pop-up será exibida se você não tiver revisado cada domínio. Clique em **Sim** para continuar revisando ou em **Não** para continuar. Se você clicar em Não, outra janela pop-up será exibida permitindo que você faça o seguinte:  
  
    1.  **Publicar**: a base de dados de conhecimento será publicada para o usuário atual ou para outros usuários. A base de dados de conhecimento não será bloqueada, o estado da base de dados de conhecimento (na tabela de bases de dados de conhecimento) será definido como vazio e as atividades de Gerenciamento de Domínio e Descoberta da Base de Dados de Conhecimento estarão disponíveis. Você será retornado à home page. Para concluir o processo, clique em **Sim** na janela pop-up.  
  
    2.  **Não**: seu trabalho será salvo, a base de dados de conhecimento permanecerá bloqueada e o estado da base de dados de conhecimento será definido como Em serviço. As atividades de Gerenciamento de Domínio e Descoberta da Base de Dados de Conhecimento estarão disponíveis. Você será retornado à home page.  
  
    3.  **Cancelar**: a janela pop-up será fechada e você permanecerá na página **Gerenciar Valor de Domínio** .  
  
12. Também é possível clicar no seguinte:  
  
    -   **Cancelar** para encerrar a atividade de Descoberta da Base de Dados de Conhecimento, o que resultará na perda do trabalho, e retornar à home page do DQS.  
  
    -   **Fechar** para retornar à home page do DQS enquanto salva o trabalho. A base de dados de conhecimento será bloqueada para você, e o estado da base de dados de conhecimento na tabela de bases de dados de conhecimento na tela **Abrir Base de Dados de Conhecimento** será **Descoberta – Gerenciamento de Valor**.  
  
    -   Clique em **Voltar** para retornar à página **Descobrir** . Depois de clicar em **Fechar**para executar a atividade de Gerenciamento de Domínio, você precisará clicar em **Descoberta da Base de Dados de Conhecimento** na tela **Abrir base de dados de conhecimento** , prosseguir para a tela **Gerenciamento da Base de Dados de Conhecimento: Gerenciar Termos do Domínio** , clicar em **Concluir**e, em seguida, clicar em **Sim** para publicar a base de dados de conhecimento ou em **Não** para salvar o trabalho na base de dados de conhecimento e sair.  
  
##  <a name="FollowUp"></a> Acompanhamento: Após executar a descoberta de dados de conhecimento  
 Após adicionar conhecimento ao caso de conhecimento no processo de descoberta de conhecimento assistido por computador, você poderá usar a base de dados de conhecimento para um projeto de limpeza imediatamente ou poderá executar o gerenciamento de domínio antes da limpeza. Para obter mais informações sobre a limpeza de dados ou o gerenciamento de domínio, consulte [Limpeza de dados](../../2014/data-quality-services/data-cleansing.md) ou [Gerenciando um domínio](../../2014/data-quality-services/managing-a-domain.md).  
  
##  <a name="Meaning"></a> O significado dos valores corretos, com erro e inválidos  
 Cada valor na tabela **Valor** da página **Valores de Domínio** recebe a configuração de **Tipo** **Correto**, **Erro**ou **Inválido**. O tipo do valor é gerado inicialmente pela atividade de descoberta da base de dados de conhecimento, e você pode alterar isso da forma que achar mais conveniente. O tipo final, com base na descoberta e nas alterações interativas, é gerado pela atividade de limpeza. Essas configurações têm os seguintes significados:  
  
-   **Correto:** este é um valor que pertence ao domínio e não tem nenhum erro de sintaxe. Por exemplo, “Chicago” em um domínio Cidade está correto.  
  
-   **Erro:** este é um valor que pertence ao domínio, mas é um valor incorreto. Por exemplo, “Shicago” em vez de “Chicago” em um domínio Cidade é um erro. O DQS designa um valor como erro; ele detecta um erro de sintaxe e uma correção associada no processo de descoberta. Os erros de sintaxe incluem erros de ortografia.  
  
-   **Inválido:** este é um valor que não pertence ao domínio e não tem correção. Por exemplo, o valor “12345” em um domínio Cidade é inválido. O DQS designa um valor como inválido quando desobedece a uma regra de domínio.  
  
 Você pode alterar o tipo de um valor manualmente para qualquer um dos outros dois valores. O DQS não impõe validade e semânticas de erro em operações manuais. Você pode inserir uma correção para obter um valor inválido sem alterar seu status. Você pode designar um valor como inválido até mesmo se ele não desobedecesse a uma regra de domínio. Você pode designar um valor como erro até mesmo se o processo de descoberta não indicasse que ele tem um erro de sintaxe. Você também pode remover uma correção para um valor Erro, que é marcado como Correto, sem alterar seu status.  
  
 Quando você está executando uma limpeza interativa de dados na página **Gerenciar e Exibir Resultados** da atividade **Limpeza** , os valores inválidos e com erro serão incluídos na guia **Inválido** da página **Gerenciar e Exibir Resultados** .  
  
##  <a name="Display"></a> How to Display the Appropriate Values  
 Você pode modificar a exibição da seguinte maneira:  
  
-   Execute o recurso**Filtro** para filtrar os resultados desejados na tabela, com base no status, selecionando o status na lista suspensa **Filtro** .  
  
-   **Localize** os dados que você deseja verificar ou modificar inserindo uma ou mais letras a serem procuradas na caixa de texto **Localizar** . Isso realçará essas letras onde quer que eles ocorram em qualquer valor exibido.  
  
-   Clique em **Mostrar Somente Novo** para restringir os valores exibidos na tabela somente aos valores que foram descobertos na sessão atual, e não nas sessões anteriores.  
  
-   Clique no botão **Expandir Tudo** para exibir todos os valores em qualquer grupo de sinônimos quando o estado atual for recolhido.  
  
-   Clique no botão **Recolher Tudo** para ocultar todos os valores em qualquer grupo de sinônimos, exceto o valor principal, quando o estado atual for expandido.  
  
-   Clique no botão **Mostrar/Ocultar o Painel de Histórico de Alterações de Valores de Domínio** para exibir uma visualização pop-up na parte inferior da tabela de valores que mostra as alterações recentes feitas na coleção de valores de domínio.  
  
##  <a name="Profiler"></a> Estatísticas do criador de perfil  
 A guia Criador de Perfil fornece estatísticas que indicam a qualidade dos dados de origem. Essas estatísticas não medem a qualidade da base de dados de conhecimento. A criação de perfil na descoberta da base de dados de conhecimento fornece ideias sobre a integridade e a exclusividade. A criação de perfil na descoberta da base de dados de conhecimento não está medindo a exatidão. A criação de perfil no gerenciamento de conhecimento ajuda você a avaliar até que ponto a fonte de dados é valiosa para compilar e aprimorar o conhecimento em uma base de dados de conhecimento.  
  
 A guia **Criador de Perfil** fornece as seguintes estatísticas para o processo de descoberta, por campo e domínio:  
  
-   **Registros**: quantos registros no exemplo de dados foram descobertos  
  
-   **Valores Totais**: quantos valores totais foram localizados para cada campo e no total  
  
-   **Novos Valores**: Quanto dos valores totais de cada campo e de todos os campos mapeados eram novos desde o último processo de descoberta, e seu percentual em relação aos valores totais  
  
-   **Valores Exclusivos**: Quanto dos valores totais de cada campo e de todos os campos mapeados eram exclusivos, e seu percentual em relação aos valores totais  
  
-   **Novos Valores Exclusivos**: Quanto dos valores exclusivos de cada campo e de todos os campos mapeados eram novos desde o último processo de descoberta, e seu percentual em relação aos valores totais  
  
-   **Válido em Valores de Domínio**: Quanto dos valores totais de cada campo e de todos os campos mapeados eram válidos, e seu percentual em relação aos valores totais  
  
 As estatísticas de campo incluem o seguinte:  
  
-   **Campo**: o nome do campo no banco de dados de origem  
  
-   **Domínio**: o nome do domínio que é mapeado para o campo  
  
-   **Novo**: o número de novos valores e o percentual de novos valores em comparação com os valores existentes no campo  
  
-   **Exclusivo**: o número de registros exclusivos no campo e seu percentual do total  
  
-   **Válido no Domínio**: o número de valores de domínio válidos e seu percentual em relação ao total  
  
-   **Integridade**: a integridade de cada campo de origem mapeado para o exercício de correspondência  
  
 A criação de perfil na descoberta da base de dados de conhecimento fornece ideias sobre a integridade. Se a criação de perfil estiver informando que um campo está relativamente incompleto, talvez você queira removê-lo da base de dados de conhecimento de um projeto de qualidade de dados. A criação de perfil talvez não forneça estatísticas confiáveis de integridade para domínios compostos. Se você precisar de estatísticas de integridade, use domínios únicos, em vez de domínios compostos. Para utilizar domínios compostos, talvez você queira criar uma base de dados de conhecimento com domínios únicos para a criação de perfil, a fim de determinar a integridade e criar outro domínio com um domínio composto para o processo de limpeza. Por exemplo, a criação de perfil pode mostrar 95% de integridade para registros de endereço usando um domínio composto, mas pode haver um nível muito mais alto de não integridade para uma das colunas, por exemplo, uma coluna de CEP. Neste exemplo, talvez você queira medir a integridade da coluna de CEP com um domínio único. A criação de perfil provavelmente fornecerá estatísticas de exatidão confiáveis para domínios compostos, pois é possível medir a exatidão para várias colunas juntas. O valor desses dados está na agregação composta, de modo que talvez você queira medir a exatidão com um domínio composto.  
  
 As estatísticas são exibidas na guia Criador de Perfil nas seguintes fases:  
  
-   Na fase **Pré-processando registros** , o DQS carrega os dados e os indexa. Isso é feita registro por registro ou lote por lote; portanto, o progresso pode ser exibido por registros. Durante a execução dessa etapa, a maioria dos dados de criação de perfil pode ser gerada, com exceção dos valores de **Válido no Domínio** .  
  
-   Na fase **Executando Regras de Domínio** , a coluna **Válido no Domínio** é populada à medida que as regras de domínio são executadas como uma unidade atômica de cada valor de domínio.  
  
-   Na fase **Executando a Descoberta** , nenhum dado novo é atualizado na guia Criador de Perfil. Os erros de sintaxe encontrados podem ser vistos na próxima etapa do assistente, a fase **Gerenciar Valores de Domínio**.  
  
 Para a atividade de descoberta da base de dados de conhecimento, as seguintes condições resultam em notificações:  
  
-   Não há valores novos em um campo; é recomendável eliminá-lo do mapeamento.  
  
-   Há alguns valores novos em um campo; talvez seja necessário eliminá-lo do mapeamento.  
  
-   Um campo está vazio; é recomendável eliminá-lo do mapeamento.  
  
-   A pontuação de integridade de campo é muito baixa; talvez você queira eliminá-lo do mapeamento.  
  
-   Todos os valores em um campo são inválidos; você deve verificar o mapeamento e a relevância das regras de domínio para o conteúdo do campo.  
  
-   Há um nível baixo de valores válidos no campo; você deve verificar o mapeamento e a relevância das regras de domínio para o conteúdo do campo.  
  
 Para obter mais informações sobre a criação de perfil, consulte [Perfil de dados e notificações no DQS](../../2014/data-quality-services/data-profiling-and-notifications-in-dqs.md).  
  
  
