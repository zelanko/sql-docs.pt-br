---
title: Implementar uma transformação pesquisa em modo Cache cheio usando o Gerenciador de Conexão de Cache | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- Lookup transformation [Integration Services]
ms.assetid: 58bc7611-5fb5-4113-9742-10959e06b94c
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: ddfed959b0f8147a8a4e48a011f65ec011f3846c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62833665"
---
# <a name="implement-a-lookup-transformation-in-full-cache-mode-using-the-cache-connection-manager"></a>Implementar uma Transformação de Pesquisa em modo de Cache Cheio usando o Gerenciador de Conexões de Cache
  Você pode configurar a transformação Pesquisa para usar o modo cache cheio e um gerenciador de conexões de cache. No modo cache cheio, o conjunto de dados de referência é carregado no cache antes que a transformação Pesquisa seja executada.  
  
> [!NOTE]  
>  O gerenciador de conexões do Cache não oferece suporte aos tipos de dados BLOB (objetos binários grandes) DT_TEXT, DT_NTEXT e DT_IMAGE. Se o conjunto de dados de referência contiver um tipo de dados BLOB, o componente irá falhar quando o pacote for executado. Você pode usar o **Editor do Gerenciador de Conexões de Cache** para modificar os tipos de dados da coluna. Para obter mais informações, consulte [Cache Connection Manager Editor](../cache-connection-manager-editor.md).  
  
 A transformação Pesquisa executa pesquisas ao unir dados em colunas de entradas através de uma fonte de dados conectada com colunas em um conjunto de dados de referência. Para obter mais informações, consulte [Lookup Transformation](../data-flow/transformations/lookup-transformation.md).  
  
 Você usa uma das opções a seguir para gerar um conjunto de dados de referência:  
  
-   Arquivo de cache (.caw)  
  
     Você configura o gerenciador de conexões de cache para ler dados de um arquivo de cache existente.  
  
-   Fonte de dados conectada no fluxo de dados  
  
     Você usa a transformação Cache para gravar dados de uma fonte de dados conectada no fluxo de dados em um gerenciador de conexões de cache. Os dados sempre são armazenados na memória.  
  
     Você deve adicionar a transformação Pesquisa em um fluxo de dados separado. Isto habilita a transformação Cache a popular o gerenciador de conexões de cache antes que a transformação Pesquisa seja executada. Os fluxos de dados podem estar no mesmo pacote ou em dois pacotes separados.  
  
     Se os fluxos de dados estiverem no mesmo pacote, use uma restrição de precedência para conectar os fluxos de dados. Isso habilita a transformação Cache a ser executada antes que a transformação Pesquisa seja executada.  
  
     Se os fluxos de dados estiverem em pacotes separados, você poderá usar a tarefa Executar Pacote para chamar o pacote filho do pacote pai. Você pode chamar vários pacotes filhos adicionando várias tarefas Executar Pacote à tarefa Contêiner Sequência no pacote pai.  
  
 Você pode compartilhar o conjunto de dados de referência armazenado em cache, entre as transformações Pesquisa usando um dos seguintes métodos:  
  
-   Configure a transformação Pesquisa em um único pacote para usar o mesmo gerenciador de conexões de cache.  
  
-   Configure os gerenciadores de conexões do cache em pacotes diferentes para usar o mesmo arquivo de cache.  
  
 Para mais informações, consulte os seguintes tópicos:  
  
-   [Transformação Cache](../data-flow/transformations/cache-transform.md)  
  
-   [Gerenciador de conexões de cache](cache-connection-manager.md)  
  
-   [Restrições de precedência](../control-flow/precedence-constraints.md)  
  
-   [Tarefa Executar Pacote](../control-flow/execute-package-task.md)  
  
-   [Contêiner da Sequência](../control-flow/sequence-container.md)  
  
 Para obter um vídeo que demonstra como implementar uma transformação Pesquisar no modo Cache Cheio usando o Gerenciador de Conexões do Cache, confira [Como implementar uma transformação de pesquisa no modo de cache cheio (vídeo do SQL Server)](https://go.microsoft.com/fwlink/?LinkId=131031).  
  
### <a name="to-implement-a-lookup-transformation-in-full-cache-mode-in-one-package-by-using-cache-connection-manager-and-a-data-source-in-the-data-flow"></a>Para implementar uma transformação Pesquisa em modo cache cheio em um pacote usando o gerenciador de conexões de cache e uma fonte de dados no fluxo de dados  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], abra um projeto [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] e, então, abra um pacote.  
  
2.  Na guia **Fluxo de Controle** , adicione duas tarefas de Fluxo de Dados e, então, conecte as tarefas usando um conector verde:  
  
3.  No primeiro fluxo de dados, adicione uma transformação Cache e, então, conecte a transformação a uma fonte de dados.  
  
     Configure a fonte de dados como necessário.  
  
4.  Clique duas vezes na transformação Cache e, depois, em **Editor de Transformação Cache**, na página **Gerenciador de Conexões** , clique em **Novo** para criar um novo gerenciador de conexões de Cache.  
  
5.  Clique na guia **Colunas** da caixa de diálogo **Editor do Gerenciador de Conexões de Cache** e, então, especifique quais colunas são as de índice usando a opção **Posição de Índice** .  
  
     Para colunas sem-índice, a posição de índice é 0. Para colunas de índice, a posição de índice é um número sequencial positivo.  
  
    > [!NOTE]  
    >  Quando a transformação Pesquisa é configurada para usar um gerenciador de conexões de Cache, somente as colunas de índice no conjunto de dados de referência podem ser mapeadas para as colunas de entrada. Além disso, todas as colunas de índice devem ser mapeadas. Para obter mais informações, consulte [Cache Connection Manager Editor](../cache-connection-manager-editor.md).  
  
6.  Para salvar o cache em um arquivo, em **Editor do Gerenciador de Conexões de Cache**, na guia **Geral** , configure o gerenciador de conexões de cache definindo as seguintes opções:  
  
    -   Selecione **Usar Cache de Arquivo**.  
  
    -   Em **Nome do arquivo**, digite o caminho do arquivo ou clique em **Procurar** para selecionar o arquivo.  
  
         Se você digitar um caminho para um arquivo que não existe, o sistema criará o arquivo quando você executar o pacote.  
  
    > [!NOTE]  
    >  O nível de proteção do pacote não se aplica ao arquivo de cache. Se o arquivo de cache tiver informações confidenciais, use uma lista de controle de acesso (ACL) para restringir o acesso ao local ou à pasta na qual você deseja armazenar o arquivo. Você deve habilitar o acesso apenas para determinadas contas. Para obter mais informações, consulte [Acesso aos arquivos usados por pacotes](../access-to-files-used-by-packages.md).  
  
7.  Configure o Cache Transform como necessário. Para obter mais informações, consulte [Editor de Transformação Cache &#40;Página Gerenciador de Conexões&#41;](../cache-transformation-editor-connection-manager-page.md) e [Editor de Transformação Cache &#40;Página Mapeamentos&#41;](../cache-transformation-editor-mappings-page.md).  
  
8.  No segundo fluxo de dados, adicione uma transformação Pesquisa e, então, configure a transformação fazendo as tarefas seguintes:  
  
    1.  Conecte a transformação Pesquisa ao fluxo de dados arrastando um conector de uma fonte ou transformação anterior para a transformação Pesquisa.  
  
        > [!NOTE]  
        >  Uma transformação Pesquisa talvez não seja validada se essa transformação se conectar a um arquivo simples que contém um campo de data vazio. A transformação será validada se o gerenciador de conexões para o arquivo simples tiver sido configurado para reter valores nulos. Para garantir a validação da transformação Pesquisa, no **Editor de Fonte de Arquivo Simples**, na página **Gerenciador de Conexões**, selecione a opção **Reter valores nulos da origem como valores nulos no fluxo de dados** .  
  
    2.  Clique duas vezes na fonte ou transformação anterior para configurar o componente.  
  
    3.  Clique duas vezes na transformação Pesquisa e, então, em **Editor de Transformação Pesquisa**, na página **Geral** , selecione **Cache cheio**.  
  
    4.  Na área **Tipo de conexão** , selecione **Gerenciador de conexões de cache**.  
  
    5.  Na lista **Especificar como manipular linhas sem entradas correspondentes** , selecione uma opção de tratamento de erros.  
  
    6.  Na página **Conexão** , da lista **Gerenciador de conexões de cache** , selecione um gerenciador de conexões de cache.  
  
    7.  Clique na página **Colunas** e, então, arraste pelo menos uma coluna da lista **Colunas de Entrada Disponíveis** para uma coluna na lista **Coluna de Pesquisa Disponível** .  
  
        > [!NOTE]  
        >  A transformação Pesquisa mapeia automaticamente colunas que têm o mesmo nome e o mesmo tipo de dados.  
  
        > [!NOTE]  
        >  Estas colunas devem ter tipos de dados correspondentes a serem mapeados. Para obter mais informações, consulte [Integration Services Data Types](../data-flow/integration-services-data-types.md).  
  
    8.  Na lista **Colunas de Pesquisa Disponíveis** , selecione colunas. Então, na lista **Operação de Pesquisa** , especifique se os valores das colunas de pesquisa substituem os valores na coluna de entrada ou se são gravados em uma nova coluna.  
  
    9. Para configurar a saída de erro, clique na página **Saída de Erro** e defina as opções de tratamento de erros. Para obter mais informações, consulte [Editor de Transformação Pesquisa &#40;página Saída de Erro&#41;](../lookup-transformation-editor-error-output-page.md).  
  
    10. Clique em **OK** para salvar suas alterações na transformação Pesquisa.  
  
9. Execute o pacote.  
  
### <a name="to-implement-a-lookup-transformation-in-full-cache-mode-in-two-packages-by-using-cache-connection-manager-and-a-data-source-in-the-data-flow"></a>Para implementar uma transformação Pesquisa em modo cache cheio em dois pacotes usando o gerenciador de conexões de cache e uma fonte de dados no fluxo de dados  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], abra um projeto [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] e, então, abra dois pacotes.  
  
2.  Na guia Fluxo de Controle em cada pacote, adicione uma tarefa de Fluxo de Dados.  
  
3.  No pacote pai, adicione uma transformação Cache ao fluxo de dados e, então, conecte a transformação à fonte de dados.  
  
     Configure a fonte de dados como necessário.  
  
4.  Clique duas vezes na transformação Cache e, depois, em **Editor de Transformação Cache**, na página **Gerenciador de Conexões** , clique em **Novo** para criar um novo gerenciador de conexões de Cache.  
  
5.  No **Editor do Gerenciador de Conexões de Cache**, na guia **Geral** , configure o gerenciador de conexões de cache definindo as seguintes opções:  
  
    -   Selecione **Usar Cache de Arquivo**.  
  
    -   Em **Nome do arquivo**, digite o caminho do arquivo ou clique em **Procurar** para selecionar o arquivo.  
  
         Se você digitar um caminho para um arquivo que não existe, o sistema criará o arquivo quando você executar o pacote.  
  
    > [!NOTE]  
    >  O nível de proteção do pacote não se aplica ao arquivo de cache. Se o arquivo de cache tiver informações confidenciais, use uma lista de controle de acesso (ACL) para restringir o acesso ao local ou à pasta na qual você deseja armazenar o arquivo. Você deve habilitar o acesso apenas para determinadas contas. Para obter mais informações, consulte [Acesso aos arquivos usados por pacotes](../access-to-files-used-by-packages.md).  
  
6.  Clique na guia **Colunas** e, então, especifique quais são as colunas de índice usando a opção **Posição do Índice** .  
  
     Para colunas sem-índice, a posição de índice é 0. Para colunas de índice, a posição de índice é um número sequencial positivo.  
  
    > [!NOTE]  
    >  Quando a transformação Pesquisa é configurada para usar um gerenciador de conexões de Cache, somente as colunas de índice no conjunto de dados de referência podem ser mapeadas para as colunas de entrada. Além disso, todas as colunas de índice devem ser mapeadas. Para obter mais informações, consulte [Cache Connection Manager Editor](../cache-connection-manager-editor.md).  
  
7.  Configure o Cache Transform como necessário. Para obter mais informações, consulte [Editor de Transformação Cache &#40;Página Gerenciador de Conexões&#41;](../cache-transformation-editor-connection-manager-page.md) e [Editor de Transformação Cache &#40;Página Mapeamentos&#41;](../cache-transformation-editor-mappings-page.md).  
  
8.  Para popular o gerenciador de conexões de cache usado no segundo pacote faça uma das opções a seguir:  
  
    -   Execute o pacote pai.  
  
    -   Clique duas vezes no gerenciador de conexões de cache que você criou na etapa 4, clique em **Colunas**, selecione as linhas e, então, pressione CTRL+C para copiar os metadados da coluna.  
  
9. No pacote filho, crie um gerenciador de conexões de cache clicando com o botão direito do mouse na área **Gerenciadores de Conexões** , clicando em **Nova Conexão**, selecionando **CACHE** na caixa de diálogo **Adicionar Gerenciador de Conexões SSIS** e, então, clicando em **Adicionar**.  
  
     A área **Gerenciadores de Conexões** aparece na parte inferior das guias **Fluxo de Controle**, **Fluxo de Dados**e **Manipuladores de Eventos** do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] Designer.  
  
10. No **Editor do Gerenciador de Conexões de Cache**, na guia **Geral** , configure o gerenciador de conexões de cache para ler os dados do arquivo de cache selecionado definindo as seguintes opções:  
  
    -   Selecione **Usar Cache de Arquivo**.  
  
    -   Em **Nome do arquivo**, digite o caminho do arquivo ou clique em **Procurar** para selecionar o arquivo.  
  
    > [!NOTE]  
    >  O nível de proteção do pacote não se aplica ao arquivo de cache. Se o arquivo de cache tiver informações confidenciais, use uma lista de controle de acesso (ACL) para restringir o acesso ao local ou à pasta na qual você deseja armazenar o arquivo. Você deve habilitar o acesso apenas para determinadas contas. Para obter mais informações, consulte [Acesso aos arquivos usados por pacotes](../access-to-files-used-by-packages.md).  
  
11. Se você copiou os metadados de coluna na etapa 8, clique em **Colunas**, selecione a linha vazia e, então, pressione CTRL+V para colar os metadados de coluna.  
  
12. Adicione uma transformação Pesquisa e, então, configure a transformação fazendo o seguinte:  
  
    1.  Conecte a transformação Pesquisa ao fluxo de dados arrastando um conector de uma fonte ou transformação anterior para a transformação Pesquisa.  
  
        > [!NOTE]  
        >  Uma transformação Pesquisa talvez não seja validada se essa transformação se conectar a um arquivo simples que contém um campo de data vazio. A transformação será validada se o gerenciador de conexões para o arquivo simples tiver sido configurado para reter valores nulos. Para garantir a validação da transformação Pesquisa, no **Editor de Fonte de Arquivo Simples**, na página **Gerenciador de Conexões**, selecione a opção **Reter valores nulos da origem como valores nulos no fluxo de dados** .  
  
    2.  Clique duas vezes na fonte ou transformação anterior para configurar o componente.  
  
    3.  Clique duas vezes na transformação Pesquisa e, então, selecione **Cache cheio** na página **Geral** do **Editor de Transformação Pesquisa**.  
  
    4.  Selecione **Gerenciador de conexões de cache** na área **Tipo de conexão** .  
  
    5.  Selecione uma opção para tratamento de erros para as linhas sem entradas correspondentes na lista **Especificar como lidar com linhas com entradas não correspondentes** .  
  
    6.  Na página **Conexão** , da lista **Gerenciador de conexões de cache** , selecione o gerenciador de conexões de cache que você adicionou.  
  
    7.  Clique na página **Colunas** e, então, arraste pelo menos uma coluna da lista **Colunas de Entrada Disponíveis** para uma coluna na lista **Coluna de Pesquisa Disponível** .  
  
        > [!NOTE]  
        >  A transformação Pesquisa mapeia automaticamente colunas que têm o mesmo nome e o mesmo tipo de dados.  
  
        > [!NOTE]  
        >  Estas colunas devem ter tipos de dados correspondentes a serem mapeados. Para obter mais informações, consulte [Integration Services Data Types](../data-flow/integration-services-data-types.md).  
  
    8.  Na lista **Colunas de Pesquisa Disponíveis** , selecione colunas. Então, na lista **Operação de Pesquisa** , especifique se os valores das colunas de pesquisa substituem os valores na coluna de entrada ou se são gravados em uma nova coluna.  
  
    9. Para configurar a saída de erro, clique na página **Saída de Erro** e defina as opções de tratamento de erros. Para obter mais informações, consulte [Editor de Transformação Pesquisa &#40;página Saída de Erro&#41;](../lookup-transformation-editor-error-output-page.md).  
  
    10. Clique em **OK** para salvar suas alterações na transformação Pesquisa.  
  
13. Abra o pacote pai, adicione uma tarefa Executar Pacote ao fluxo de controle e, então, configure a tarefa para chamar o pacote filho. Para obter mais informações, consulte [Execute Package Task](../control-flow/execute-package-task.md).  
  
14. Execute os pacotes.  
  
### <a name="to-implement-a-lookup-transformation-in-full-cache-mode-by-using-cache-connection-manager-and-an-existing-cache-file"></a>Para implementar uma transformação Pesquisa em modo cache cheio usando o gerenciador de conexões de cache e um arquivo de cache existente  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], abra um projeto [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] e, então, abra um pacote.  
  
2.  Clique com o botão direito do mouse na área **Gerenciadores de Conexões** e, então, clique em **Nova Conexão**.  
  
     A área **Gerenciadores de Conexões** aparece na parte inferior das guias **Fluxo de Controle**, **Fluxo de Dados**e **Manipuladores de Eventos** do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] Designer.  
  
3.  Use a caixa de diálogo **Adicionar Gerenciador de Conexões SSIS** , selecione **CACHE**e, então, clique em **Adicionar** para adicionar um gerenciador de conexões de cache.  
  
4.  Clique duas vezes no gerenciador de conexões de cache para abrir o **Editor do Gerenciador de Conexões de Cache**.  
  
5.  No **Editor do Gerenciador de Conexões de Cache**, na guia **Geral** , configure o gerenciador de conexões de cache definindo as seguintes opções:  
  
    -   Selecione **Usar Cache de Arquivo**.  
  
    -   Em **Nome do arquivo**, digite o caminho do arquivo ou clique em **Procurar** para selecionar o arquivo.  
  
    > [!NOTE]  
    >  O nível de proteção do pacote não se aplica ao arquivo de cache. Se o arquivo de cache tiver informações confidenciais, use uma lista de controle de acesso (ACL) para restringir o acesso ao local ou à pasta na qual você deseja armazenar o arquivo. Você deve habilitar o acesso apenas para determinadas contas. Para obter mais informações, consulte [Acesso aos arquivos usados por pacotes](../access-to-files-used-by-packages.md).  
  
6.  Clique na guia **Colunas** e, então, especifique quais são as colunas de índice usando a opção **Posição do Índice** .  
  
     Para colunas sem-índice, a posição de índice é 0. Para colunas de índice, a posição de índice é um número sequencial positivo.  
  
    > [!NOTE]  
    >  Quando a transformação Pesquisa é configurada para usar um gerenciador de conexões de Cache, somente as colunas de índice no conjunto de dados de referência podem ser mapeadas para as colunas de entrada. Além disso, todas as colunas de índice devem ser mapeadas. Para obter mais informações, consulte [Cache Connection Manager Editor](../cache-connection-manager-editor.md).  
  
7.  Na guia **Fluxo de Controle** , adicione uma tarefa de Fluxo de Dados ao pacote e adicione uma transformação Pesquisa ao fluxo de dados.  
  
8.  Configure a transformação Pesquisa fazendo o seguinte:  
  
    1.  Conecte a transformação Pesquisa ao fluxo de dados arrastando um conector de uma fonte ou transformação anterior para a transformação Pesquisa.  
  
        > [!NOTE]  
        >  Uma transformação Pesquisa talvez não seja validada se essa transformação se conectar a um arquivo simples que contém um campo de data vazio. A transformação será validada se o gerenciador de conexões para o arquivo simples tiver sido configurado para reter valores nulos. Para garantir a validação da transformação Pesquisa, no **Editor de Fonte de Arquivo Simples**, na página **Gerenciador de Conexões**, selecione a opção **Reter valores nulos da origem como valores nulos no fluxo de dados** .  
  
    2.  Clique duas vezes na fonte ou transformação anterior para configurar o componente.  
  
    3.  Clique duas vezes na transformação Pesquisa e, então, em **Editor de Transformação Pesquisa**, na página **Geral** , selecione **Cache cheio**.  
  
    4.  Selecione **Gerenciador de conexões de cache** na área **Tipo de conexão** .  
  
    5.  Selecione uma opção para tratamento de erros para as linhas sem entradas correspondentes na lista **Especificar como lidar com linhas com entradas não correspondentes** .  
  
    6.  Na página **Conexão** , da lista **Gerenciador de conexões de cache** , selecione o gerenciador de conexões de cache que você adicionou.  
  
    7.  Clique na página **Colunas** e, então, arraste pelo menos uma coluna da lista **Colunas de Entrada Disponíveis** para uma coluna na lista **Coluna de Pesquisa Disponível** .  
  
        > [!NOTE]  
        >  A transformação Pesquisa mapeia automaticamente colunas que têm o mesmo nome e o mesmo tipo de dados.  
  
        > [!NOTE]  
        >  Estas colunas devem ter tipos de dados correspondentes a serem mapeados. Para obter mais informações, consulte [Integration Services Data Types](../data-flow/integration-services-data-types.md).  
  
    8.  Na lista **Colunas de Pesquisa Disponíveis** , selecione colunas. Então, na lista **Operação de Pesquisa** , especifique se os valores das colunas de pesquisa substituem os valores na coluna de entrada ou se são gravados em uma nova coluna.  
  
    9. Para configurar a saída de erro, clique na página **Saída de Erro** e defina as opções de tratamento de erros. Para obter mais informações, consulte [Editor de Transformação Pesquisa &#40;página Saída de Erro&#41;](../lookup-transformation-editor-error-output-page.md).  
  
    10. Clique em **OK** para salvar suas alterações na transformação Pesquisa.  
  
9. Execute o pacote.  
  
## <a name="see-also"></a>Consulte também  
 [Implementar uma transformação Pesquisa em modo de cache cheio por meio da transformação Gerenciador de Conexões OLE DB](lookup-transformation-full-cache-mode-ole-db-connection-manager.md)   
 [Implementar uma pesquisa no modo Sem cache ou Cache parcial](../data-flow/transformations/implement-a-lookup-in-no-cache-or-partial-cache-mode.md)   
 [Transformações do Integration Services](../data-flow/transformations/integration-services-transformations.md)  
  
  
