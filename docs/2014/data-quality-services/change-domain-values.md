---
title: Alterar valores de domínio | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- data-quality-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.dqs.dm.values.f1
ms.assetid: 8c90ab70-3aea-4eaf-a174-4159485c87d3
caps.latest.revision: 30
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 0ef4a5f7264309be27c53f3a71ae6118a403c4ce
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37156707"
---
# <a name="change-domain-values"></a>Alterar valores de domínio
  Este tópico descreve como alterar e aumentar os metadados em uma base de dados de conhecimento no [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS). Depois que você gerar conhecimento através de descoberta de conhecimento, importar conhecimento para a base de dados de conhecimento ou domínios, ou utilizar outra base de dados de conhecimento como base para a base de dados de conhecimento, poderá alterar os valores de dados interativamente. A geração de base de dados de conhecimento não só aproveita processos assistidos por computador, mas lhe fornece os meios para usar seu próprio conhecimento para verificar valores de dados e alterá-los da seguinte forma:  
  
-   Adicione um valor de domínio à lista de valores ou selecione um valor e exclua-o da lista  
  
-   Altere o status de um valor de domínio conforme designado pelo processo de descoberta do DQS, modificando-o para correto, em erro ou inválido  
  
-   Insira um valor substituto para um valor que está em erro ou é inválido. Um valor será inválido se não pertencer ao domínio; por exemplo, se não estiver de acordo com o tipo de dados de domínio ou desobedecer uma regra de domínio. Um valor está em erro se pertence ao domínio, mas tem um erro de sintaxe.  
  
-   Defina dois ou mais valores como sinônimos e altere o valor principal conforme definido pelo processo de descoberta, com o resultado que o valor principal substituirá o valor do sinônimo, caso a propriedade **Usar Valor Principal** tenha sido definida quando você criou o domínio  
  
-   Importar valores de domínio de um arquivo do Excel  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Prerequisites"></a> Pré-requisitos  
 Para alterar um valor de domínio, você deve ter uma base de dados de conhecimento e um domínio aberto na atividade de Gerenciamento de Domínio.  
  
###  <a name="Security"></a> Segurança  
  
####  <a name="Permissions"></a> Permissões  
 Você deve ter a função dqs_kb_editor ou dqs_administrator no banco de dados DQS_MAIN para alterar valores de domínio.  
  
##  <a name="Change"></a> Alterar valores de domínio  
 A tabela **Valor** exibe o conhecimento adicionado à base de dados de conhecimento para um domínio único. Você pode selecionar um domínio diferente a qualquer momento na lista de domínios para exibir os valores desse domínio. As colunas do campo são as seguintes:  
  
-   A coluna **Valor** exibe todos os valores que o processo de descoberta adicionou ao domínio selecionado de um campo no exemplo de dados. Qualquer valor projetado como erro será mostrado como sinônimo de um valor projetado como correto.  
  
-   A coluna **Tipo** exibe o status do valor, conforme determinado pelo processo de descoberta. Uma marca de verificação verde indica que o valor está correto ou corrigido; uma cruz vermelha indica que o valor está com erro; um triângulo laranja com um ponto de exclamação indica que o valor é inválido. Um valor inválido não está em conformidade com os requisitos de dados do domínio. Um valor com erro pode ser válido, mas não é o valor correto para fins de dados.  
  
-   A coluna **Corrigir para** mostra um valor correto para o qual o valor original, marcado como erro ou inválido, será alterado. O DQS pode propor o valor correto como resultado do processo de descoberta.  
  
 Para alterar valores, faça o seguinte:  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)] [Executar o aplicativo Data Quality Client](../../2014/data-quality-services/run-the-data-quality-client-application.md).  
  
2.  Na tela inicial do [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] , abra ou crie uma base de dados de conhecimento. Selecione **Gerenciamento de Domínio** como a atividade e, depois, clique em **Abrir** ou **Criar**. Para obter mais informações, consulte [Criar uma base de dados de conhecimento](../../2014/data-quality-services/create-a-knowledge-base.md) ou [Abrir uma base de dados de conhecimento](../../2014/data-quality-services/open-a-knowledge-base.md).  
  
    > [!NOTE]  
    >  O gerenciamento de domínio é executado em uma página do cliente Data Quality Services que contém cinco guias para operações de gerenciamento de domínio separadas. Não se trata de um processo controlado por assistente; qualquer operação de gerenciamento pode ser executada separadamente.  
  
3.  Na **Lista de domínios** na página **Gerenciamento de Domínio** , selecione o domínio no qual você deseja alterar valores ou crie um novo domínio. Se você precisar criar um novo domínio, consulte [Criar um Domínio](../../2014/data-quality-services/create-a-domain.md). Clique na guia **Valores do Domínio** .  
  
4.  Exiba os valores que você precisa modificar na tabela **Valor** . Para obter mais informações, consulte [How to Display the Appropriate Values](#Display) abaixo.  
  
5.  Para alterar o estado de um valor, faça o seguinte:  
  
    -   **Definir valores de domínio selecionados como corrigidos**: para alterar o estado de um valor de Erro ou Inválido para Correto, selecione o valor e clique em **Definir valores de domínio selecionados como corrigidos** (marca de verificação) na seta para baixo da barra de ícones ou na lista suspensa de Tipo. Se o valor com erro ou inválido for agrupado com um valor correto, exclua esse valor após a operação.  
  
    -   **Definir valores de domínio selecionados como erros**: para alterar o estado de um valor de Correto ou Inválido para Erro, selecione o valor e clique no ícone **Definir valores de domínio selecionados como erros** (cruz) na seta para baixo da barra de ícones ou na lista suspensa de Tipo. Insira uma correção na coluna **Corrigir para** ou deixe em branco.  
  
    -   **Definir valores de domínio selecionados como inválidos**: para alterar o estado de um valor de Correto ou Erro para Inválido, selecione o valor e clique no ícone **Definir valores de domínio selecionados como inválidos** (triângulo) na seta para baixo da barra de ícones ou na lista suspensa de Tipo. Insira uma correção na coluna **Corrigir para** ou deixe em branco.  
  
    -   **Corrigir para:** Após definir um valor como erro ou inválido, insira um novo valor na coluna **Corrigir para** . O DQS adicionará uma nova linha para o valor substituto, o designará como correto e agrupará os dois valores. O novo valor será mostrado como o valor principal, com o valor principal em negrito e o valor com erro ou inválido recuado.  
  
6.  Para designar valores como um grupo de sinônimos, selecione diversos valores corretos e continue da seguinte maneira:  
  
    -   **Definir valores de domínio selecionados como sinônimos**: Para definir sinônimos, selecione diversos valores que estão corretos e clique no ícone **Definir valores de domínio selecionados como sinônimos** . O DQS agrupará os valores e designará um deles como o valor principal que substituirá os outros. Observe que, se forem agrupados dois valores, mas um do grupo estiver com erro ou for inválido, os valores não são sinônimos.  
  
        > [!NOTE]  
        >  Se você selecionar dois ou mais valores em um grupo e outro valor fora do grupo, e defini-los como sinônimos, você obterá uma mensagem de erro incorreta. Após fechar a mensagem de erro pop-up, os valores serão definidos corretamente como sinônimos.  
  
    -   **Quebrar relação entre os sinônimos selecionados**: Para desfazer a designação de sinônimo para dois ou mais valores, selecione os valores e clique no ícone **Quebrar relação entre os sinônimos selecionados** . Os valores devem ser agrupados e ambos devem estar corretos para que o desagrupamento de sinônimos funcione.  
  
    -   **Definir valores de domínio selecionados como um valor principal de seu grupo**: Para alterar o valor principal do grupo, selecione um valor no grupo que não esteja designado como o valor principal e clique no botão **Definir valores de domínio selecionados como um valor principal de seu grupo** . Isso definirá o valor principal como uma substituição para obter o outro valor. Essa operação funcionará apenas se você tiver definido dois ou mais valores de grupo e desejar alterar o valor principal a partir do valor designado pelo DQS. Observe que o valor principal é designado por uma linha azul com o valor em negrito.  
  
7.  **Verificador Ortográfico**: Se um valor tiver um sublinhado vermelho ondulado, o Verificador Ortográfico sugerirá uma correção para o valor. Clique com o botão direito do mouse no valor com sublinhado e selecione uma correção, caso ela se aplique. O tipo de valor se torna (ou permanece como) um erro, e a correção será adicionada à coluna **Corrigir para** . Clique na seta para baixo para ver outras correções propostas. Insira uma correção manualmente para adicioná-la ao dicionário do Verificador Ortográfico para que você possa selecioná-la como uma correção. Para obter mais informações, consulte [Usar o verificador ortográfico DQS](../../2014/data-quality-services/use-the-dqs-speller.md) e [Definir propriedades de domínio](../../2014/data-quality-services/set-domain-properties.md).  
  
    > [!NOTE]  
    >  Para usar o Verificador Ortográfico, você pode habilitá-lo na página **Propriedades de Domínio** ou, se ele estiver desabilitado na página **Propriedades de Domínio** , você poderá clicar no ícone **Habilitar/Desabilitar o Verificador Ortográfico** na página **Valores de Domínio** para habilitá-lo nessa página.  
  
8.  **Adicionar novo valor de domínio**: Clique para adicionar uma linha no final da tabela. Depois que você inserir um valor, a linha será reposicionada em ordem alfabética e será identificada como uma nova entrada por um símbolo de estrela anterior.  
  
9. **Importar valores de domínio do Excel**: Para adicionar novos valores de uma planilha do Excel, clique na seta para baixo do ícone **Importar Valores** e selecione **Importar valores de domínio do Excel**. Insira o nome de arquivo, selecione **Usar primeira linha como cabeçalho** , se apropriado, e clique em **OK**. Para obter mais informações, consulte [Importar valores de um arquivo do Excel para um domínio](../../2014/data-quality-services/import-values-from-an-excel-file-into-a-domain.md).  
  
10. **Importar valores de projeto**: Para adicionar novos valores de um projeto de qualidade de dados, clique na seta para baixo do ícone **Importar Valores** e selecione **Importar valores de projeto**. Insira o nome de arquivo, selecione **Usar primeira linha como cabeçalho** , se apropriado, e clique em **OK**. Selecione o projeto a partir do qual você importará valores e clique em **OK**. Os valores importados serão exibidos. Clique em **Concluir**. Para obter mais informações, consulte Importar valores de projeto para um domínio.  
  
11. **Excluir valores de domínio selecionados**: Para remover um ou mais valores existentes do domínio, selecione os valores na tabela Valor e clique no ícone **Excluir valores de domínio selecionados** . A entrada DQS_NULL não pode ser excluída; portanto, se você escolher diversos valores para serem excluídos, e a entrada DQS_NULL for um deles, a operação falhará.  
  
12. Clique em **Concluir** para concluir a atividade de gerenciamento de domínio, conforme descrito em [Terminar a atividade Gerenciamento de Domínio](../../2014/data-quality-services/end-the-domain-management-activity.md).  
  
##  <a name="FollowUp"></a> Acompanhamento: após alterar valores de domínio  
 Após alterar valores de domínio, você poderá executar outras tarefas de gerenciamento de domínio, executar a descoberta da base de dados de conhecimento para adicionar conhecimento ao domínio ou adicionar uma política de correspondência ao domínio. Para obter mais informações, consulte [Executar a descoberta de conhecimento](../../2014/data-quality-services/perform-knowledge-discovery.md), [Gerenciando um domínio](../../2014/data-quality-services/managing-a-domain.md) ou [Criar uma política de conciliação](../../2014/data-quality-services/create-a-matching-policy.md).  
  
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
  
##  <a name="Null"></a> Como tratar equivalentes nulos  
 Cada tabela de valor na guia **Valores de Domínio** inclui um valor DQS_NULL. Um nulo em uma fonte de dados aparecerá como SQL_NULL na tabela de valor. Você pode definir um ou mais equivalentes nulos como sinônimos de DQS_NULL. Quando você fizer isso, todos os nulos e equivalentes nulos serão processados como DQS_NULL.  
  
  
