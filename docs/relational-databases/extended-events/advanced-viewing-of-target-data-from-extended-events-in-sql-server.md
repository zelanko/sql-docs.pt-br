---
title: Exibição avançada de dados de destino de Eventos Estendidos no SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 05/24/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xevents
ms.topic: tutorial
ms.assetid: b2e839d7-1872-46d9-b7b7-6dcb3984829f
author: MightyPen
ms.author: genemi
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 030635af78475eebfa63169b712528b8beeafa38
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68021935"
---
# <a name="advanced-viewing-of-target-data-from-extended-events-in-sql-server"></a>Exibição avançada de dados de destino dos Eventos Estendidos no SQL Server

[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]


Este artigo ilustra como você pode usar os recursos avançados do SQL Server Management Studio (SSMS.exe) para exibir os dados de destino de eventos estendidos bem detalhadamente. Este artigo explica como:


- Abrir e exibir os dados de destino, de várias maneiras.
- Exportar os dados de destino para vários formatos, usando o menu ou a barra de ferramentas especial de eventos estendidos.
- Manipular os dados durante a exibição ou antes da exportação.



### <a name="prerequisites"></a>Prerequisites

O presente artigo pressupõe que você já saiba como criar e iniciar uma sessão de evento. Confira as instruções sobre como criar uma sessão de evento no início do seguinte artigo:

[Início rápido: Eventos estendidos no SQL Server](../../relational-databases/extended-events/quick-start-extended-events-in-sql-server.md)


Este artigo também pressupõe que você instalou uma versão mensal muito recente do SSMS. A ajuda da instalação está localizada em:

- [Baixar o SQL Server Management Studio (SSMS)](../../ssms/download-sql-server-management-studio-ssms.md)



### <a name="differences-with-azure-sql-database"></a>Diferenças do Banco de Dados SQL do Azure


Há um alto grau de paridade na implementação e nas funcionalidades de eventos estendidos nesses dois produtos: Microsoft SQL Server e Banco de Dados SQL do Azure. Mas existem algumas diferenças que afetam a interface do usuário do SSMS.


- Para o Banco de Dados SQL, o destino package0.event_file não pode ser um arquivo na unidade de disco local. Em vez disso, um contêiner do Armazenamento do Azure deve ser usado. Portanto, quando você estiver conectado ao Banco de Dados SQL, a interface do usuário do SSMS solicitará um contêiner de armazenamento, em vez de um caminho local e um nome de arquivo.


- Na interface do usuário do SSMS, quando você vir a caixa de seleção **Observar dados dinâmicos** esmaecida e desabilitada, isso ocorre porque esse recurso não está disponível para o Banco de Dados SQL.


- Alguns eventos estendidos são instalados com o SQL Server. No nó **Sessões** , podemos ver **AlwaysOn_health** , além de algumas outras. Elas não são visíveis durante a conexão ao Banco de Dados SQL, pois não existem para o Banco de Dados SQL.


O presente artigo foi escrito da perspectiva do SQL Server. O artigo usa o destino event_file, que é uma das diferenças. Outras menções de diferenças são limitadas a diferenças importantes ou não óbvias.


Para obter a documentação sobre os eventos estendidos específica ao Banco de Dados SQL do Azure, veja:

- [Eventos Estendidos no Banco de Dados SQL do Azure](https://azure.microsoft.com/documentation/articles/sql-database-xevent-db-diff-from-svr/)



## <a name="a-general-options"></a>A. Opções gerais


Geralmente, as opções avançadas são acessadas da seguinte maneira:


- O menu comum **Arquivo** > **Abrir** > **Arquivo**.
- Cliques com o botão direito do mouse no **Pesquisador de Objetos** em **Gerenciamento** > **Eventos Estendidos**.
- O menu especial **Eventos Estendidos**e a barra de ferramentas especial de eventos estendidos.
- Cliques com o botão direito do mouse no painel com guias que exibe os dados de destino.



## <a name="b-bring-target-data-into-ssms-for-display"></a>B. Inserir os dados de destino no SSMS para exibição


Há várias maneiras para inserir os dados de destino event_file na interface do usuário do SSMS. Quando você especifica um destino event_file, você define seu nome e caminho do arquivo:

- .XEL é a extensão do nome do arquivo.


- Sempre que a sessão de evento é iniciada, o sistema insere um inteiro grande em um novo nome de arquivo, para tornar o nome de arquivo exclusivo e diferente da ocasião anterior em que a sessão foi iniciada.
  - *Exemplo:* Checkpoint_Begins_ES_0_131103935140400000.xel


- O conteúdo de um .XEL não é um texto sem formatação que pode ser exibido com o Notepad.exe.
  - Se desejar, a maneira de acrescentar vários arquivos .XEL juntos será usar o menu **Arquivo** > **Abrir** > **Mesclar Arquivos de Eventos Estendidos**.



O SSMS pode exibir dados de qualquer destino. Mas as exibições são diferentes para os vários destinos:

- *event_file:* Os dados de um destino event_file são exibidos muito bem, com recursos avançados disponíveis.


- *ring_buffer:* Os dados de um destino de buffer de anéis são exibidos como um XML bruto.


- Para os outros destinos, a potência do monitor fica em algum ponto entre o de event_file e o de ring_buffer.
  - Outros destinos desse tipo incluem event_counter, histogram e pair_matching.


- *etw_classic_sync_target:* O SSMS não pode exibir dados do tipo de destino etw_classic_sync_target.



### <a name="b1-open-xel-with-menu-file--open--file"></a>B.1 Abra o .XEL com o menu Arquivo > Abrir > Arquivo


É possível abrir um arquivo .XEL individual com o menu padrão **Arquivo** > **Abrir** > **Arquivo**.

Você também pode arrastar e soltar um arquivo .XEL na barra de guias da interface do usuário do SSMS.



### <a name="b2-view-target-data"></a>B.2 Exibir dados de destino


A opção **Exibir Dados de Destino** exibe os dados que foram capturados até o momento.


No painel **Pesquisador de Objetos** , é possível expandir os nós e clicar com o botão direito do mouse:

- **Gerenciamento** > **Eventos Estendidos** > **Sessões** >  *[sua sessão]*  >  *[seu-nó-de-destino]*  > **Exibir Dados de Destino**.


Os dados de destino são exibidos em um painel com guias no SSMS. Isso é mostrado na captura de tela a seguir.


![seu destino > Exibir Dados de Destino](../../relational-databases/extended-events/media/xevents-ssms-ui20-viewtargetdata.png)


> [!NOTE] 
> A opção**Exibir Dados de Destino** exibe os *dados acumulados de vários arquivos .XEL* de determinada sessão de evento. Cada ciclo **Iniciar**-**Interromper** cria um arquivo com um inteiro derivado de tempo posteriormente inserido em seu nome, mas cada arquivo compartilha o mesmo nome raiz.



#### <a name="b3-watch-live-data"></a>B.3 Observar dados dinâmicos


Quando a sessão de evento estiver ativa no momento, talvez você queira observar os dados do evento em tempo real, conforme são recebidos pelo destino.


- **Gerenciamento** > **Eventos Estendidos** > **Sessões** >  *[sua-sessão]*  > **Observar Dados Dinâmicos**.


![sua sessão > Observar Dados Dinâmicos](../../relational-databases/extended-events/media/xevents-ssms-ui55-watchlivedata.png)


A exibição de dados é atualizada em um intervalo que pode ser especificado. Veja **Latência máxima de expedição** em:

- **Eventos Estendidos** > **Sessões** >  *[sua-sessão]*  > **Propriedades** > **Avançado** > **Latência máxima de expedição**



### <a name="b4-view-xel-with-sysfnxefiletargetreadfile-function"></a>B.4 Exibir .XEL com a função sys.fn_xe_file_target_read_file


Para o processamento em lotes, a seguinte função do sistema pode gerar um XML para os registros em um arquivo .XEL:

- [sys.fn\_xe\_file\_target\_read\_file](../../relational-databases/system-functions/sys-fn-xe-file-target-read-file-transact-sql.md)



## <a name="c-export-the-target-data"></a>C. Exportar os dados de destino


Depois de inserir os dados de destino no SSMS, você pode exportá-los para vários formatos, fazendo o seguinte:


1. Focalize a exibição de dados.

[!INCLUDE[freshInclude](../../includes/paragraph-content/fresh-note-steps-feedback.md)]

    - De repente, uma nova barra de ferramentas e um novo item de menu de eventos estendidos se tornarão visíveis.

    ![Exportar os dados exibidos, Eventos Estendidos > Exportar para > (.csv ou .xel, ou para uma tabela)](../../relational-databases/extended-events/media/xevents-ssms-ui75-menuextevent-exportto-xel.png)

2. Clique no novo item de menu **Eventos Estendidos**.
3. Clique em **Exportar para**e escolha um formato.



## <a name="d-manipulate-data-in-the-display"></a>D. Manipular os dados na exibição


A interface do usuário do SSMS oferece várias maneiras de manipular os dados, além de simplesmente exibir os dados no estado em que se encontram.



### <a name="d1-context-menus-in-the-data-display"></a>D.1 Menus de contexto na exibição de dados


Locais diferentes na exibição de dados oferecem menus de contexto diferentes ao clicar com o botão direito do mouse.



#### <a name="d11-right-click-a-data-cell"></a>D.1.1 Clicar com o botão direito do mouse em uma célula de dados


A captura de tela a seguir mostra o menu de conteúdo obtido quando você clica com o botão direito do mouse na exibição de dados. A captura de tela também mostra a expansão do item de menu **Copiar** .


![Clicar com o botão direito do mouse em uma célula, na exibição de dados](../../relational-databases/extended-events/media/xevents-ssms-ui25-rightclickcell.png)



#### <a name="d12-right-click-a-column-header"></a>D.1.2 Clicar com o botão direito do mouse em um cabeçalho de coluna


A captura de tela a seguir mostra o menu de contexto em um clique com o botão direito do mouse do cabeçalho **timestamp** .


![Clique com o botão direito do mouse em um cabeçalho de coluna, na exibição de dados. Além disso, a grade de detalhes.](../../relational-databases/extended-events/media/xevents-ssms-ui40-toolbar.png)


A captura de tela anterior também mostra a barra de ferramentas especial de eventos estendidos. O brilho do botão Detalhes indica que o botão está ativo. Portanto, a imagem mostra também a guia **Detalhes** , e a grade está presente como uma segunda parte da exibição de dados.



### <a name="d2-choose-columns-merge-columns"></a>D.2 Escolher colunas, Mesclar colunas


A opção **Escolher Colunas** permite controlar quais colunas de dados são exibidas e não. Você pode encontrar o item de menu **Escolher Colunas** em alguns locais diferentes:

- No menu **Eventos Estendidos** .
- Na barra de ferramentas de eventos estendidos.
- No menu de contexto de um cabeçalho na exibição de dados.


Quando você clica em **Escolher Colunas**, é exibida a caixa de diálogo homônima.


![A caixa de diálogo Escolher Colunas também oferece as opções Mesclar colunas](../../relational-databases/extended-events/media/xevents-ssms-ui35-choosecolumns.png)



#### <a name="d21-merge-columns"></a>D.2.1 Mesclar colunas


A caixa de diálogo **Escolher Colunas** tem uma seção dedicada à mesclagem de várias colunas em uma, para fins de:

- Exibição.
- Exportar.



### <a name="d3-filters"></a>D.3 Filtros


Na área de eventos estendidos, há dois tipos principais de filtros que podem ser especificados:

- *Filtros de pré-destino:* Filtros que reduzem a quantidade de dados enviada pelo mecanismo de eventos ao destino.

- *Filtros de pós-destino:* Filtros que podem ser selecionados na interface do usuário do SSMS para excluir alguns registros de destino da exibição.


Os filtros da exibição do SSMS são os seguintes:

- Um filtro de *intervalo de tempo* , que examina a coluna **timestamp** .
- Um filtro de *valores de coluna* .


A relação entre os filtros de tempo e de colunas é um booliano “*AND*”.


![Intervalo de tempo e filtros de coluna na caixa de diálogo Filtros](../../relational-databases/extended-events/media/xevents-ssms-ui45-filters.png)



### <a name="d4-grouping-and-aggregation"></a>D.4 Agrupamento e agregação


Agrupar linhas por valores correspondentes em determinada coluna é a primeira etapa para a agregação de resumo de dados.



#### <a name="d41-grouping"></a>D.4.1 Agrupamento


Na barra de ferramentas de eventos estendidos, o botão **Agrupamento** inicia uma caixa de diálogo que pode ser usada para agrupar os dados exibidos por determinada coluna. A próxima captura de tela mostra uma caixa de diálogo usada para agrupar pela coluna *name*.

![Barra de ferramentas > botão Agrupamento e a caixa de diálogo Agrupamento](../../relational-databases/extended-events/media/xevents-ssms-ui53-grouping.png)

Depois de realizar o agrupamento, a exibição terá uma nova aparência, como mostrado a seguir.

![Nova aparência da exibição após o Agrupamento](../../relational-databases/extended-events/media/xevents-ssms-ui54-grouped.png)



#### <a name="d42-aggregation"></a>D.4.2 Agregação


Depois que os dados exibidos forem agrupados, você poderá continuar para agregar dados em outras colunas.  A próxima captura de tela mostra os dados agrupados sendo agregados por *count*.

![Barra de ferramentas > botão Agregação e a caixa de diálogo Agregação](../../relational-databases/extended-events/media/xevents-ssms-ui51-aggregdialogcount.png)

Depois de realizar a agregação, a exibição terá uma nova aparência, como mostrado a seguir.

![Barra de ferramentas > botão Agregação e a caixa de diálogo Agregação](../../relational-databases/extended-events/media/xevents-ssms-ui52-aggregnewdisplay.png)



### <a name="d5-view-run-time-query-plan"></a>D.5 Exibir plano de consulta de tempo de execução


O evento **query_post_execution_showplan** permite ver o plano de consulta real na interface do usuário do SSMS. Quando o painel **Detalhes** estiver visível, você poderá ver um gráfico do plano de consulta na guia **Plano de Consulta** . Focalizando um nó no plano de consulta, você poderá ver uma lista de nomes de propriedade e seus valores para o nó.


![Plano de Consulta, com a lista de propriedades de um nó](../../relational-databases/extended-events/media/xevents-ssms-ui60-showplangraph.png)

## <a name="see-also"></a>Confira também

[XELite: Biblioteca multiplataforma para ler XEvents de arquivos XEL ou fluxos ao vivo do SQL](https://www.nuget.org/packages/Microsoft.SqlServer.XEvent.XELite/), lançado em maio de 2019.

[Cmdlet do PowerShell Read-SQLXEvent](https://www.powershellgallery.com/packages/SqlServer), lançado em julho de 2019.
