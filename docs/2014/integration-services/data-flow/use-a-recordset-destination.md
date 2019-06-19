---
title: Usar um destino do conjunto de registros | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- Recordset destination
ms.assetid: a7b143dc-8008-404f-83b0-b45ffbca6029
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: b87d71f8299c55e033adc21e25e29e8fb3d5e9d6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62899949"
---
# <a name="use-a-recordset-destination"></a>Usar um destino do conjunto de registros
  O destino do Conjunto de Registros não salva dados em uma fonte de dados externa. Em vez disso, o destino do Conjunto de Registros salva dados na memória em um conjunto de registros armazenado em uma variável de pacote do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] do tipo de dados `Object`. Depois que o destino do Conjunto de Registros salva os dados, geralmente você usa um contêiner Loop Foreach com o enumerador ADO Foreach para processar uma linha do conjunto de registros de cada vez. O enumerador ADO Foreach salva o valor de cada coluna da linha atual em uma variável de pacote separada. Em seguida, as tarefas que você configura dentro do contêiner Loop Foreach leem esses valores das variáveis e executam alguma ação com eles.  
  
 Você pode usar o destino do Conjunto de Registros em muitos cenários diferentes. Estes são alguns exemplos:  
  
-   É possível usar uma tarefa Enviar Email e a linguagem da expressão do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] para enviar uma mensagem de email personalizada para cada linha no conjunto de registros.  
  
-   Você pode usar um componente Script configurado como fonte, dentro de uma tarefa de fluxo de dados, para ler os valores nas colunas do fluxo de dados. Em seguida, é possível usar transformações e destinos para transformar e salvar a linha. Neste exemplo, a tarefa de fluxo de dados é executada uma vez para cada linha.  
  
 As seções a seguir primeiro descrevem o processo geral de uso do destino do Conjunto de Registros e depois mostram um exemplo específico de como utilizar o destino.  
  
## <a name="general-steps-to-using-a-recordset-destination"></a>Etapas gerais para o uso de um destino do conjunto de registros  
 O procedimento a seguir resume as etapas necessárias para salvar dados em um destino do Conjunto de Registros e usar o contêiner Loop Foreach para processar cada linha.  
  
#### <a name="to-save-data-to-a-recordset-destination-and-process-each-row-by-using-the-foreach-loop-container"></a>Para salvar dados em um destino do Conjunto de Registros e processar cada linha usando o contêiner Loop Foreach  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], crie ou abra um pacote do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
2.  Crie uma variável que conterá o conjunto de registros salvo na memória pelo destino do Conjunto de Registros e defina o tipo de variável como `Object`.  
  
3.  Crie mais variáveis dos tipos apropriados para conter os valores de cada coluna no conjunto de registros que você deseja usar.  
  
4.  Adicione e configure o gerenciador de conexões necessário para a fonte de dados que você planeja usar no fluxo de dados.  
  
5.  Adicione uma tarefa de fluxo de dados ao pacote e, na guia Fluxo de Dados do [!INCLUDE[ssIS](../../includes/ssis-md.md)] Designer, configure fontes e transformações para carregar e transformar os dados.  
  
6.  Adicione um destino do Conjunto de Registros ao fluxo de dados e conecte-o às transformações. Para a propriedade `VariableName` do destino do Conjunto de Registros, insira o nome da variável criada para conter o conjunto de registros.  
  
7.  Na guia Fluxo de Controle do [!INCLUDE[ssIS](../../includes/ssis-md.md)] Designer, adicione um contêiner Loop Foreach e conecte esse contêiner após a tarefa de fluxo de dados. Em seguida, abra o **Editor de Loop Foreach** para definir o contêiner com as seguintes configurações:  
  
    1.  Na página **Coleção** , selecione o Enumerador ADO Foreach. Em seguida, para **Variável de origem do objeto ADO**, selecione a variável que contém o conjunto de registros.  
  
    2.  Na página **Mapeamentos de Variáveis** , mapeie o índice com base em zero de cada coluna que você deseja usar para a variável apropriada.  
  
         Em cada iteração do loop, o enumerador popula essas variáveis com os valores de coluna da linha atual.  
  
8.  Dentro do contêiner Loop Foreach, adicione e configure tarefas para processar uma linha do conjunto de registros de cada vez, lendo os valores das variáveis.  
  
## <a name="example-of-using-the-recordset-destination"></a>Exemplo de uso do destino do Conjunto de Registros  
 No exemplo a seguir, a tarefa de fluxo de dados carrega informações sobre os funcionários de [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] da tabela Sales.SalesPerson em um destino do Conjunto de Registros. Em seguida, um contêiner Loop Foreach lê uma linha de dados de cada vez e chama uma tarefa Enviar Email. A tarefa Enviar Email usa expressões para enviar uma mensagem de email personalizada a cada vendedor sobre o valor de seu bônus.  
  
#### <a name="to-create-the-project-and-configure-the-variables"></a>Para criar o projeto e configurar as variáveis  
  
1.  No [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)], crie um novo projeto do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
2.  No menu **SSIS** , selecione **Variáveis**.  
  
3.  Na janela **Variáveis** , crie as variáveis que conterão o conjunto de registros e os valores de coluna da linha atual:  
  
    1.  Crie uma variável denominada `BonusRecordset` e defina seu tipo como `Object`.  
  
         A variável `BonusRecordset` contém o conjunto de registros.  
  
    2.  Crie uma variável denominada `EmailAddress` e defina seu tipo como `String`.  
  
         A variável `EmailAddress` contém o endereço de email do vendedor.  
  
    3.  Crie uma variável denominada `FirstName` e defina seu tipo como `String`.  
  
         A variável `FirstName` contém o nome do vendedor.  
  
    4.  Crie uma variável denominada `Bonus` e defina seu tipo como `Double`.  
  
         A variável `Bonus` contém o valor do bônus do vendedor.  
  
#### <a name="to-configure-the-connection-managers"></a>Para configurar os gerenciadores de conexões  
  
1.  Na área Gerenciadores de Conexões do [!INCLUDE[ssIS](../../includes/ssis-md.md)] Designer, adicione e configure um novo gerenciador de conexões OLE DB que se conecta ao banco de dados de exemplo [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] .  
  
     A fonte OLE DB na tarefa de fluxo de dados usará esse gerenciador de conexões para recuperar dados.  
  
2.  Na área Gerenciadores de Conexões, adicione e configure um novo gerenciador de conexões SMTP que se conecta ao servidor SMTP disponível.  
  
     A tarefa Enviar Email dentro do contêiner Loop Foreach usará esse gerenciador de conexões para enviar emails.  
  
#### <a name="to-configure-the-data-flow-and-the-recordset-destination"></a>Para configurar o fluxo de dados e o destino do Conjunto de Registros  
  
1.  Na guia **Fluxo de Controle** do [!INCLUDE[ssIS](../../includes/ssis-md.md)] Designer, adicione uma tarefa de fluxo de dados à superfície de design.  
  
2.  Na guia **Fluxo de Dados** , adicione uma fonte OLE DB à tarefa de fluxo de dados e abra o **Editor de Origem OLE DB.**  
  
3.  Na página **Gerenciador de Conexões** do editor, defina a fonte com as seguintes configurações:  
  
    1.  Para **Gerenciador de Conexões OLE DB**, selecione o gerenciador de conexões OLE DB criado anteriormente.  
  
    2.  Para **Modo de acesso a dados**, selecione o **Comando SQL**.  
  
    3.  Em **Texto do comando SQL**, digite a seguinte consulta:  
  
        ```  
        SELECT     Person.Contact.EmailAddress, Person.Contact.FirstName, CONVERT(float, Sales.SalesPerson.Bonus) AS Bonus  
        FROM         Sales.SalesPerson INNER JOIN  
                              Person.Contact ON Sales.SalesPerson.SalesPersonID = Person.Contact.ContactID  
        ```  
  
        > [!NOTE]  
        >  É necessário converter o valor `currency` na coluna Bônus em um `float`, antes de carregar esse valor em uma variável de pacote cujo tipo é `Double`.  
  
4.  Na guia **Fluxo de Dados** , adicione um destino do Conjunto de Registros e conecte o destino após a fonte OLE DB.  
  
5.  Abra o **Editor de Destino do Conjunto de Registros**e defina o destino com as seguintes configurações:  
  
    1.  Sobre o **propriedades do componente** guia, para `VariableName` propriedade, selecione `User::BonusRecordset`.  
  
    2.  Na guia **Colunas de Entrada** , selecione todas as três colunas disponíveis.  
  
#### <a name="to-configure-the-foreach-loop-container-and-run-the-package"></a>Para configurar o contêiner Loop Foreach e executar o pacote  
  
1.  Na guia **Fluxo de Controle** do [!INCLUDE[ssIS](../../includes/ssis-md.md)] Designer, adicione um contêiner Loop Foreach e conecte esse contêiner após a tarefa de fluxo de dados.  
  
2.  Abra o **Editor de Loop Foreach**e defina o contêiner com as seguintes configurações:  
  
    1.  Sobre o **coleta** página, para **enumerador**, selecione **enumerador ADO Foreach**e para **variável de origem do objeto ADO**, selecione `User::BonusRecordset`.  
  
    2.  Sobre o **mapeamentos de variáveis** página, mapeie `User::EmailAddress` para índice 0, `User::FirstName` para índice 1 e `User::Bonus` para índice 2.  
  
3.  Na guia **Fluxo de Controle** , dentro do contêiner Loop Foreach, adicione uma tarefa Enviar Email.  
  
4.  Abra o **Editor da Tarefa Enviar Email**e, na página **Email** , defina a tarefa com as seguintes configurações:  
  
    1.  Para **SmtpConnection**, selecione o gerenciador de conexões SMTP configurado anteriormente.  
  
    2.  Em **De**, insira um endereço de email apropriado.  
  
         Se você usar seu próprio endereço de email, poderá confirmar a execução bem-sucedida do pacote. Você receberá recibos de impossibilidade de entrega das mensagens enviadas pela tarefa Enviar Email aos vendedores fictícios de [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)].  
  
    3.  Em **Para**, insira um endereço de email padrão.  
  
         Esse valor não será usado, mas será substituído em tempo de execução pelo endereço de email de cada vendedor.  
  
    4.  Em **Assunto**, digite "Seu bônus anual".  
  
    5.  Em **MessageSourceType**, selecione **Entrada Direta**.  
  
5.  Na página **Expressões** do **Editor da Tarefa Enviar Email**, clique no botão de reticências ( **...** ) para abrir o **Editor de Expressões de Propriedade**.  
  
6.  No **Editor de Expressões de Propriedade**, insira as seguintes informações:  
  
    1.  Em **ToLine**, adicione a seguinte expressão:  
  
        ```  
        @[User::EmailAddress]  
        ```  
  
    2.  Para a propriedade **MessageSource** , adicione a seguinte expressão:  
  
        ```  
        "Dear " +  @[User::FirstName] + ": The amount of your bonus for this year is $" +  (DT_WSTR, 12) @[User::Bonus] + ". Thank you!"  
        ```  
  
7.  Execute o pacote.  
  
     Caso tenha especificado um servidor SMTP válido e fornecido seu próprio endereço de email, você receberá recibos de impossibilidade de entrega que a tarefa Enviar Email envia aos vendedores fictícios de [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)].  
  
  
