---
title: Usar comparação de esquema para comparar definições de banco de dados diferentes
description: Saiba como comparar definições de banco de dados com a Comparação de Esquemas. Confira como excluir diferenças específicas e atualizar o destino ou então criar um script de atualização.
ms.prod: sql
ms.technology: ssdt
ms.topic: conceptual
f1_keywords:
- sql.data.tools.schemacompare.SchemaCompareOptionsDialog
- sql.data.tools.schemacompare.watermark.f1
- sql.data.tools.schemacompare.f1
- sql.data.tools.schemacompare.connectiondialog.f1
- sql.data.tools.schemacompare.connectiondialog.error.f1
ms.assetid: 7f0905a4-081c-46e2-bd7d-325b63e5c675
author: markingmyname
ms.author: maghan
ms.reviewer: “”
ms.custom: seo-lt-2019
ms.date: 02/09/2017
ms.openlocfilehash: 2347297adfbc9d4df88c7df32fffefa4990010d8
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85895826"
---
# <a name="how-to-use-schema-compare-to-compare-different-database-definitions"></a>Como fazer: Usar comparação de esquema para comparar definições de banco de dados diferentes

O SQL Server Data Tools (SSDT) inclui um utilitário de Comparação de Esquemas que você poderá usar para comparar duas definições de banco de dados.  A origem e o destino da comparação podem ser qualquer combinação do banco de dados conectado, do projeto de banco de dados do SQL Server, do instantâneo ou do arquivo .dacpac.  Os resultados da comparação aparecem como um conjunto de ações que devem ser executadas com o destino para torná-lo igual à origem.  Uma vez que a comparação esteja concluída, você poderá atualizar o destino diretamente (se o destino for um projeto ou um banco de dados) ou gerar um script de atualização que tenha o mesmo efeito.  
  
As diferenças entre a origem e o destino aparecem em uma grade para facilitar a revisão.  Você poderá analisar e revisar cada diferença na grade de resultados ou no formulário de script.  Em seguida, poderá excluir diferenças específicas seletivamente.  
  
Você também pode salvar comparações como parte de um projeto de Banco de dados do SQL Server ou como um arquivo autônomo.  Você poderá ainda definir opções que controlam o escopo da comparação e os aspectos da atualização.  Em seguida, poderá salvar a comparação para poder repetir facilmente a mesma comparação posteriormente ou usá-la como ponto de partida para uma nova comparação.  
  
O procedimento a seguir compara o esquema de um projeto de banco de dados com um banco de dados conectado.  
  
> [!WARNING]  
> Se um projeto for especificado como o destino da comparação, o comprimento de caminho máximo com suporte (excluindo a letra da unidade, o dois-pontos e a barra invertida à frente) para o projeto será de 256 caracteres. Se seu caminho de projeto exceder 256 caracteres, você ainda poderá comparar seu esquema com um banco de dados ou outro projeto. Porém, você não poderá atualizar seu esquema.  
  
> [!WARNING]  
> Os procedimentos a seguir utilizam entidades criadas em procedimentos anteriores nas seções [Desenvolvimento de banco de dados conectado](../ssdt/connected-database-development.md) e [Desenvolvimento de banco de dados offline orientado a projetos](../ssdt/project-oriented-offline-database-development.md).  
  
### <a name="to-compare-database-definitions"></a>Para comparar definições de banco de dados  
  
1.  No menu **Ferramentas**, selecione **SQL Server** e clique em **Nova Comparação de Esquemas**.  
  
    Como alternativa, clique com o botão direito do mouse no projeto **TradeDev**, no **Gerenciador de Soluções**, e selecione **Comparação de Esquemas**.  
  
    A janela **Comparação de Esquemas** é aberta e o Visual Studio automaticamente atribui a ela um nome, como `SqlSchemaCompare1`.  
  
    Dois menus suspensos com uma seta verde entre eles aparecem logo abaixo da barra de ferramentas da janela **Comparação de Esquemas**. Esses menus permitem que você selecione definições de banco de dados para a origem e o destino da comparação.  
  
2.  No menu suspenso **Selecionar Origem**, escolha **Selecionar Origem** para abrir a caixa de diálogo **Selecionar Esquema de Origem**.  
  
    Observe que, se você abriu a janela **Comparação de Esquemas** clicando com o botão direito do mouse no nome do projeto, o esquema de origem já estará preenchido e você poderá passar para a etapa 4.  
  
3.  Selecione o botão de opção **Projeto** e selecione o projeto de banco de dados **TradeDev** que você criou no procedimento anterior.  
  
4.  No menu suspenso **Selecionar Destino**, na **Janela de Comparação de Esquemas**, escolha **Selecionar Destino** para abrir a caixa de diálogo **Selecionar Esquema de Destino**. Na seção **Esquema**, clique no botão de opção **Banco de Dados** e, em seguida, clique no botão **Nova Conexão**.  
  
5.  Na caixa de diálogo **Propriedades de Conexão**, insira o nome do servidor onde o banco de dados `TradeDev` reside e verifique se as credenciais de autenticação corretas são fornecidas. Selecione **TradeDev** em **Conectar a um banco de dados** e clique em **OK**.  
  
    Você também pode clicar no botão **Opções** na barra de ferramentas da **Janela de Comparação de Esquemas** para especificar quais objetos são comparados, que tipos de diferenças são ignorados e outras configurações.  
  
6.  Clique no botão **Comparar** na barra de ferramentas da **Janela de Comparação de Esquemas** para iniciar o processo de comparação.  
  
    Quando a comparação estiver concluída, as diferenças estruturais entre o projeto e o banco de dados aparecerão no painel **Resultados**, na parte superior da janela. Por padrão, os resultados da comparação agrupam todas as diferenças por ação (como Excluir, Alterar ou Adicionar). O painel **Resultados** exibe uma linha para cada objeto de banco de dados que difere entre as definições de banco de dados. Cada linha identifica o objeto no esquema de origem ou destino (ou ambos), bem como a ação que será executada no esquema de destino para tornar o objeto de destino igual ao objeto de origem.  Se um objeto tiver sido refatorado e renomeado ou movido para um novo esquema, os nomes da origem e do destino serão diferentes, e o nome da origem aparecerá em negrito para realçar a diferença.  
  
    Por padrão, a lista de resultados oculta os objetos iguais em ambos os esquemas ou que não têm suporte para atualização (por exemplo, objetos internos).  Você poderá clicar nos botões de filtro apropriados na barra de ferramentas para mostrar esses objetos.  
  
    Para alterar a preferência de agrupamento, clique na lista suspensa **Agrupar Resultados** na barra de ferramentas.  Selecione **Tipo** para agrupar os resultados por tipo de objeto (por exemplo, por tabelas, exibições ou procedimentos armazenados).  
  
7.  Localize a tabela `Products` no grupo `Tables`. Clique na linha e observe se as definições de origem e destino da tabela aparecem no painel **Definições de Objeto** com as diferenças realçadas. Você também poderá expandir a linha da tabela `Products` no painel **Resultados** para inspecionar os elementos específicos que são diferentes na tabela.  
  
8.  Por padrão, todas as diferenças são incluídas no escopo da ação Atualizar Destino. Você pode excluir as diferenças que não deseja sincronizar. Para isso, desmarque a coluna **Ação** no centro de cada linha. Como alternativa, clique com o botão direito do mouse em uma linha no painel Esquema e selecione **Excluir**. Observe que a linha fica acinzentada imediatamente. Quando for o momento de atualizar o banco de dados de destino, essa linha não será considerada para nenhuma alteração pendente.  
  
    Você também poderá clicar com o botão direito do mouse em uma linha de grupo e selecionar **Excluir Tudo** ou **Incluir Tudo**, o que é equivalente a desmarcar ou marcar todas as diferenças nesse grupo. Quando você agrupa resultados por esquema, isso é útil para incluir ou excluir todas as alterações de um esquema específico.  
  
    > [!WARNING]  
    > Se a linha que está sendo excluída tiver objetos dependentes (por exemplo, uma linha **Tabela** que seja referenciada por uma linha **Exibição**), a linha excluída será desabilitada, mas sua caixa de seleção não será desmarcada. Quando todas as linhas que dependem dela forem desmarcadas, uma linha desabilitada será desmarcada. Além disso, se uma linha for refatorada (renomeada ou movida para outro esquema), a caixa de seleção será desabilitada para essa linha e qualquer uma de suas linhas filho dependentes.  
    >   
    > Observe que, se você atualizar a comparação, essas diferenças que você escolheu ignorar serão ignoradas.  
  
Para atualizar o esquema do destino, você tem duas opções. Você poderá atualizar o destino diretamente na janela **Comparação de Esquemas**, se o destino for um banco de dados ou um projeto, ou gerar um script de atualização, se o destino for um banco de dados ou um arquivo de banco de dados.  Um script gerado é exibido no Editor Transact\-SQL, no qual você pode inspecionar o script e executá-lo em um banco de dados. Os procedimentos a seguir descrevem essas opções mais detalhadamente.  
  
> [!WARNING]  
> A atualização falhará porque nossa alteração envolve alterar uma coluna de NOT NULL para NULL e, com isso, causa perda de dados. Se desejar prosseguir com a atualização, clique no botão **Opções** (o quinto a partir da esquerda) na barra de ferramentas para a Comparação de Esquemas e desmarque a opção **Bloquear implantação incremental se houver perda de dados**.  
  
### <a name="to-update-directly-in-the-schema-compare-window"></a>Para atualizar diretamente na janela Comparação de Esquemas  
  
1.  Clique no botão **Atualizar** na barra de ferramentas da janela Comparação de Esquemas.  
  
2.  Examine o script de alteração gerado. Você pode salvar o script usando o menu Arquivo/Novo. Isto pode ser útil para situações em que você não tem autorização para atualizar um banco de dados de produção e, nesse caso, você pode dar o script para um DBA implantar posteriormente.  
  
3.  Se você tiver a permissão necessária para atualizar o banco de dados, clique no botão **Executar Consulta** no painel de edição para executar o script.  
  
### <a name="to-update-by-script"></a>Para atualizar por script  
  
1.  Clique no botão **Gerar Script** (o quarto a partir da esquerda) na barra de ferramentas da janela Comparação de Esquemas.  
  
    O script gerado é exibido em uma nova janela do Editor Transact\-SQL  
  
    > [!WARNING]  
    > Somente arquivos .dacpac produzidos pelo processo de instantâneo do SSDT oferecem suporte a esse comportamento.  Você não pode ter como destino um arquivo .dacpac produzido pelas ferramentas ou estrutura de Aplicativo da Camada de Dados (DAC) SQL neste momento.  
  
2.  Examine o script de alteração gerado. Você pode salvar o script usando o comando de menu **Arquivo/Salvar** ou Arquivo/Salvar como.  
  
    Um script salvo pode ser prático nas situações em que você não tem autorização para atualizar um banco de dados de produção. Nesses casos, você pode fornecer o script a um DBA para implantação posterior.  
  
    Como alternativa, agora você pode conectar o Editor Transact\-SQL a um servidor apropriado e executar o script diretamente. Para poder executar esse procedimento, você deve ter a permissão necessária para criar ou atualizar o banco de dados. Se você tiver a permissão necessária para atualizar o banco de dados, clique no botão **Executar Consulta** no painel de edição para executar o script.  
  
3.  Clique no botão **Conectar**. Essa ação estabelece conexão com o servidor atual ou solicita que você insira ou selecione um na caixa de diálogo Conectar ao Servidor.  Observe que o nome de banco de dados é definido no script como uma variável de comando.  
  
4.  Inspecione o script e, se necessário, faça quaisquer alterações nas variáveis de comando que definem o nome do banco de dados de destino, o prefixo associado e os caminhos de arquivo.  
  
5.  Clique no botão **Executar** na barra de ferramentas do painel de edição para executar o script.  
  
