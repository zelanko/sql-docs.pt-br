---
title: Criar uma sessão de eventos estendidos usando a caixa de diálogo nova sessão | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
f1_keywords:
- SQL12.SSMS.XEDISPLAY.GROUPING.F1
- SQL12.SSMS.XEDISPLAY.AGGREGATION.F1
- SQL12.SSMS.XEDISPLAY.NEWMERGEDCOLUMN.F1
- SQL12.SSMS.XENEWEVENTSESSION.GENERAL.F1
- SQL12.SSMS.XEDISPLAY.EDITCOLUMNS.F1
- SQL12.SSMS.XEDISPLAY.FILTERS.F1
helpviewer_keywords:
- Extended Events Dialog Box
ms.assetid: 6b2244bc-df6a-4b0a-990e-ddd8d42f7907
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: e1135b4738aea40d4bf426dffc6bcccb64c9f59e
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/27/2018
ms.locfileid: "52408683"
---
# <a name="create-an-extended-events-session-using-the-new-session-dialog"></a>Criar uma sessão de Eventos Estendidos usando a caixa de diálogo Nova Sessão
  A caixa de diálogo Nova Sessão permite definir uma sessão de Eventos Estendidos que captura, exibe e analisa seus dados. A caixa de diálogo Nova Sessão expõe toda a funcionalidade de Eventos Estendidos.  
  
 O [Assistente para Nova Sessão](../ssms/object/object-explorer.md) também permite definir uma sessão de Eventos Estendidos com suporte para grande parte da funcionalidade de Eventos Estendidos.  
  
## <a name="before-you-begin"></a>Antes de começar  
 Para abrir a caixa de diálogo Nova Sessão no Pesquisador de Objetos, expanda o nó **Gerenciamento** e, em seguida, expanda **Eventos Estendidos**. Clique com o botão direito do mouse em **Sessões**e clique em **Nova Sessão**.  
  
##  <a name="BeforeYouBegin"></a> Permissões  
 Para criar uma sessão de Eventos Estendidos, você deve ter a permissão ALTER ANY EVENT SESSION.  
  
## <a name="to-create-an-extended-events-session-using-the-new-session-dialog"></a>Para criar uma sessão de Eventos Estendidos usando a caixa de diálogo Nova Sessão  
 Use a página **Geral** para selecionar um modelo e agendar uma sessão de evento.  
  
#### <a name="to-select-a-template-and-schedule-an-event-session"></a>Para selecionar um modelo e agendar uma sessão de evento  
  
1.  No Pesquisador de Objetos, expanda o nó **Gerenciamento** e, em seguida, expanda **Eventos Estendidos**. Clique com o botão direito do mouse em **Sessões**e clique em **Nova Sessão**.  
  
2.  Na página **Geral** , na caixa **Nome da sessão** , digite um nome significativo para a sessão de evento.  
  
3.  Na caixa **Modelo** , selecione o modelo que deseja usar na lista suspensa.  
  
     Você pode selecionar um modelo de um conjunto de modelos pré-configurados criados para problemas comuns ou selecionar **Do Arquivo** para usar um arquivo de modelo exportado de uma definição de sessão anterior. Observe que você também pode alterar a configuração da sessão após aplicar o modelo.  
  
4.  Na seção **Agendar** , se você quiser iniciar a sessão ao inicializar o servidor, marque a caixa de seleção **Iniciar a sessão de evento na inicialização do servidor** .  
  
     Para iniciar a sessão após criá-la, marque a caixa de seleção **Iniciar a sessão de evento imediatamente após a inicialização da sessão** .  
  
5.  Para exibir os dados dinâmicos da sessão de evento, clique em **Observar dados dinâmicos na tela à medida que eles são capturados**. Os dados dinâmicos começarão a exibir o rastreamento imediatamente depois que a sessão for criada.  
  
6.  Na seção **Rastreamento de causalidade** , marque a caixa de seleção **Controlar como os eventos estão relacionados uns aos outros** para controlar o trabalho entre várias tarefas.  
  
     Para obter mais informações sobre rastreamento de causalidade, consulte "Conteúdo e características da sessão" na [sessões de eventos estendidos do SQL Server](../relational-databases/extended-events/sql-server-extended-events-sessions.md) tópico.  
  
     Para adicionar eventos à sua sessão, na seção **Selecionar uma página** , clique em **Eventos**.  
  
    > [!NOTE]  
    >  Clique em **OK** somente depois de terminar de criar a sessão de evento.  
  
 Use a página **Eventos** para localizar e adicionar os eventos que deseja capturar para a sessão.  
  
#### <a name="to-add-events-to-a-session"></a>Para adicionar eventos a uma sessão  
  
1.  Na caixa de diálogo Nova Sessão, na seção **Selecionar uma página** , selecione **Eventos**.  
  
2.  Na página **Eventos** , clique em **Selecionar** (o botão **Selecionar** ficará esmaecido se você já estiver na tela **Selecionar os eventos que você deseja capturar** ).  
  
     Você pode procurar qualquer palavra na tabela inserindo o texto que deseja procurar na caixa **Biblioteca de eventos** . Por exemplo, se quiser encontrar o evento **lock_acquired** , insira **lock** ou **lock acquire**.  
  
3.  Na seção **Biblioteca de eventos** , especifique como você procurará os eventos que deseja capturar na lista suspensa. Por exemplo, você pode procurar nomes de evento ou nomes de evento e suas descrições. Insira seus critérios de pesquisa na caixa **Pesquisar** .  
  
    > [!NOTE]  
    >  Os eventos do canal de **Depuração** são ocultos por padrão. Para exibir os eventos de depuração, selecione **Depurar** na lista suspensa **Canal** .  
  
     Aparecerão detalhes dos eventos selecionados no painel Detalhes na **Biblioteca de eventos**.  
  
     Os eventos são classificados por nome em ordem alfabética. Você pode realizar a classificação por outros detalhes de evento clicando no título de coluna apropriado. Por exemplo, você pode realizar a classificação pela coluna **Categoria** ou **Canal** .  
  
4.  Selecione o(s) evento(s) que você deseja capturar e clique na seta para a direita a fim de movê-los para a seção **Eventos Selecionados** .  
  
    > [!NOTE]  
    >  Você pode selecionar vários eventos ao mesmo tempo na **Biblioteca de eventos** usando as teclas CTRL ou SHIFT.  
  
     Para configurar os eventos selecionados, clique em **Configurar**.  
  
    > [!NOTE]  
    >  Clique em **OK** somente depois de terminar de criar a sessão de evento.  
  
 Use a página **Armazenamento de dados** para adicionar destinos a uma sessão de evento. Os destinos armazenam dados de evento e podem executar ações como salvar eventos em um arquivo para exibição e agregação posterior dos dados de evento da sessão. Para obter mais informações sobre os destinos dos Eventos Estendidos, consulte [SQL Server Extended Events Targets](../../2014/database-engine/sql-server-extended-events-targets.md).  
  
 Estes são os destinos que você pode usar em uma sessão de Eventos Estendidos:  
  
-   **etw_classic_sync_target**. Use para correlacionar eventos do SQL Server com o sistema operacional Windows ou os dados de evento de aplicativo.  
  
-   **event_counter**. Conta todos os eventos especificados ocorridos depois que uma sessão de Evento Estendido é iniciada. Use para obter informações sobre as características da carga de trabalho sem adicionar a sobrecarga de uma coleção de eventos completa.  
  
-   **event_file**. Use para gravar a saída da sessão de evento de buffers de memória completos em disco.  
  
-   **histogram**. Use para contar o número de vezes que um evento especificado ocorre com base em uma coluna de eventos ou uma ação específica.  
  
-   **pair_matching**. Use para determinar quando um evento emparelhado especificado não ocorre em um conjunto correspondente.  
  
-   **ring_buffer**. Use para manter os dados do evento na memória em uma base PEPS (primeiro a entrar, primeiro a sair) ou em uma base PEPS por evento.  
  
#### <a name="to-configure-global-fields-for-a-session"></a>Para configurar campos globais de uma sessão  
  
1.  Na página **Eventos** , após selecionar o(s) evento(s) que você deseja adicionar à sessão de evento, clique em **Configurar**.  
  
     Depois que você clicar em **Configurar**, a seção **Biblioteca de eventos** será recolhida e a seção **Eventos selecionados** deslizará para a esquerda da página. A seção **Opções de configuração do evento** usada para configurar os eventos aparece no lado direito da página. Use as guias desta página para configurar ações durante para sua sessão de evento.  
  
2.  Na guia **Campos Globais** , selecione os campos que deseja aplicar aos eventos selecionados.  
  
     Você pode selecionar vários campos para cada evento.  
  
    > [!NOTE]  
    >  Se dois eventos que já estão selecionados tiverem ações configuradas diferentes, os Eventos Estendidos exibirão as ações parcialmente verificadas. Para localizar rapidamente quais ações você habilitou, você pode realizar a classificação pelo status habilitado/desabilitado clicando no título de coluna acima das caixas de seleção.  
  
3.  Na guia  **Filtros** , aplique os filtros (também chamados predicados) para limitar os eventos que deseja capturar.  
  
     Se um filtro for aplicado ao evento selecionado, uma marca de verificação aparecerá na coluna.  
  
    > [!NOTE]  
    >  Você pode selecionar vários eventos ao qual deseja aplicar um filtro usando as teclas CTRL ou SHIFT. No entanto, somente os campos de evento comuns aparecerão para configuração. Se dois eventos selecionados já tiverem filtros diferentes configurados para eles, o filtro não aparecerá. A reconfiguração dos filtros substituirá os valores de filtro existentes.  
  
    > [!NOTE]  
    >  Quando você configurar uma cláusula de grupo para o filtro, serão removidos os parênteses redundantes do filtro depois que o resultado for salvo. Por exemplo, se você criar um agrupamento de filtros **Cláusula 1** e **Cláusula 2**, aparecerão parênteses delimitando as cláusulas. Depois que você salvar o filtro, os parênteses redundantes serão removidos. A remoção dos parênteses não afetará a lógica do filtro.  
  
4.  Na guia **Campos de Evento** , selecione os campos de evento que deseja aplicar a um evento selecionado.  
  
     Os eventos contêm vários campos que sempre são coletados; eles são exibidos na guia **Campos de Evento** sem caixas de seleção. Um evento também pode ter campos opcionais que não são coletados por padrão (por exemplo, os campos opcionais caros não são selecionados). Os campos opcionais também são listados na guia **Campos de Evento** com caixas de seleção. Para coletar um campo opcional, marque a caixa de seleção em frente ao campo opcional.  
  
    > [!NOTE]  
    >  As opções de campo de evento exibirão campos que serão capturados e exibidos nos resultados do rastreamento. (Os Eventos Estendidos exibem apenas tipos de dados dos campos de evento. Por exemplo, os campos de evento somente leitura não são exibidos.) Se você selecionar dois ou mais eventos, a caixa de diálogo Nova Sessão exibirá um espaço em branco na guia **Campos de Evento** .  
  
5.  Para adicionar destinos a uma sessão de evento, na seção **Selecionar uma página** , selecione **Armazenamento de Dados**.  
  
    > [!NOTE]  
    >  Clique em **OK** somente depois de terminar de criar a sessão de evento.  
  
#### <a name="to-add-targets-to-an-event-session"></a>Para adicionar destinos a uma sessão de evento  
  
1.  Na caixa de diálogo Nova Sessão, na seção **Selecionar uma página** , selecione **Armazenamento de Dados**.  
  
2.  Na página **Armazenamento de Dados** , selecione o tipo de destino na lista suspensa.  
  
     Depois que você selecionar o tipo de destino, a descrição de destino será exibida. Você só poderá adicionar um destino uma vez. Se você já adicionou o destino à sessão, ele não aparecerá na lista suspensa.  
  
3.  Clique em **Adicionar** para adicionar um destino para a sessão de evento. Se você deseja remover um destino, clique em **Remover**.  
  
     As propriedades de destino aparecem abaixo da seção **Destinos** , dependendo do destino selecionado.  
  
4.  Estas são as propriedades que você pode especificar, sujeitas aos destinos selecionados:  
  
    |Destino|Propriedades de destino|  
    |------------|-----------------------|  
    |**etw_classic_sync_target**|**Nome do arquivo de log de sessão no servidor**. Insira o nome do arquivo de log e do diretório no servidor ou clique em **Procurar** para localizar e selecionar o arquivo de log.<br /><br /> **Tamanho máximo do log do arquivo**. Insira o tamanho máximo do arquivo de log para o evento ETW (Rastreamento de Eventos para Windows). O padrão é 20 megabytes (MB). Você pode selecionar outra unidade de armazenamento na lista suspensa.<br /><br /> **Tamanho do buffer**. Insira o tamanho de buffer na memória para o evento de sessão. O valor padrão é 128 KB (quilobytes). Você pode selecionar outra unidade de armazenamento na lista suspensa.<br /><br /> **Nome da sessão**. Insira um nome de sessão ETW significativo.<br /><br /> **Repetir se houver erro ao gravar no ETW**. Marque essa caixa de seleção para repetir a publicação do evento no subsistema ETW.<br /><br /> **Número máximo de tentativas**. Insira o número máximo de vezes que você tentará publicar o evento novamente no subsistema ETW antes de remover o evento. O número máximo de novas tentativas é zero (0). Para esta propriedade de destino, zero (0) significa nenhuma nova tentativa.|  
    |**event_counter**|Não há nenhuma propriedade de destino para o contador de eventos.|  
    |**event_file**|**Nome do arquivo no servidor**. Insira o diretório e o nome do arquivo de destino no servidor ou clique em **Procurar** para localizar e selecionar o arquivo de destino.<br /><br /> **Tamanho máximo de arquivo**. Especifique o tamanho máximo de arquivo do destino de arquivo. Se você não especificar o tamanho máximo do arquivo, este crescerá até que o disco fique cheio. O tamanho de arquivo padrão é 1 GB (gigabyte). Você pode selecionar outra unidade de armazenamento na lista suspensa.<br /><br /> **Habilitar substituição de arquivo**. Marque esta caixa de seleção para habilitar substituição de arquivo do destino de arquivo.<br /><br /> **Número máximo de arquivos**. Insira o número máximo de arquivos a serem retidos no sistema de arquivos.|  
    |**Histograma**|**Evento para filtrar em**. Selecione o evento a ser filtrado na lista suspensa. Você pode realizar a filtragem em qualquer evento existente na sessão de evento. Você também pode selecionar  **\<None >** na lista suspensa para incluir todos os eventos e os buckets base na ação.<br /><br /> **Basear buckets em: Ação**. Selecione esta opção para basear os buckets no nome de ação usado como fonte de dados e selecione a ação na lista suspensa.<br /><br /> **Basear buckets em: Campo**. Selecione esta opção para basear os buckets no campo de evento usado como fonte de dados e selecione o campo na lista suspensa.<br /><br /> **Número máximo de buckets**. Insira o número máximo de buckets a serem retidos. Quando esse valor for atingido, a sessão de evento ignorará quaisquer novos eventos que não pertençam aos buckets existentes.|  
    |**pair_matching**|**Eventos: Começar com**. Selecione o nome de evento na lista suspensa que especifica o evento inicial em uma sequência emparelhada.<br /><br /> **Eventos: Terminar com**. Selecione o nome de evento na lista suspensa que especifica o evento final em uma sequência emparelhada.<br /><br /> **Campos e ações: Começar com**. Selecione o campo inicial e/ou ação em uma sequência emparelhada na lista suspensa.<br /><br /> **Campos e ações: Terminar com**. Selecione o campo final e/ou ação em uma sequência emparelhada na lista suspensa.<br /><br /> **Descartar os novos eventos não emparelhados se ocorrer pressão de memória**. Marque esta caixa de seleção para interromper a coleta de eventos no destino pair_matching quando o computador estiver sob pressão de memória. Quando não houver mais nenhuma pressão de memória, a coleta de eventos será retomada.<br /><br /> **Máximo de eventos órfãos**. Especifique o número máximo de eventos órfãos a ser mantido na memória.|  
    |**ring_buffer**|**Número de eventos a serem mantidos**. Use as setas para cima e para baixo a fim de especificar o número de eventos a ser mantido. O padrão é 1000.<br /><br /> **Tamanho máximo da memória do buffer**. Insira a quantidade máxima de memória ser usada. Os eventos existentes são removidos quando esse valor é atingido. O tamanho de memória padrão é 0 MB (megabytes), que significa ilimitado. Você pode selecionar outra unidade de armazenamento na lista suspensa.<br /><br /> **Manter um número específico de eventos (por tipo) quando o buffer estiver cheio**. Selecione esta opção para manter um número de eventos especificado para cada tipo no buffer.<br /><br /> **Número de eventos a serem mantidos (por tipo)**. Insira o número preferido de eventos de cada tipo a ser mantido no buffer.|  
  
5.  Se você deseja definir propriedades de configuração avançadas, selecione **Avançado** na seção **Selecionar uma página** .  
  
    > [!NOTE]  
    >  Clique em **OK** somente depois de terminar de criar a sessão de evento.  
  
#### <a name="to-set-advanced-configurations"></a>Para definir configurações avançadas  
  
1.  Na caixa de diálogo Nova Sessão, na seção **Selecionar uma página** , selecione **Avançado**.  
  
2.  Na página **Avançado** , para especificar as opções de **Modo de retenção de evento** da sessão de evento, faça o seguinte:  
  
    1.  **Perda única de evento**. Selecione esta opção para permitir a perda de um único evento.  
  
    2.  **Perda múltipla de evento**. Selecione esta opção para permitir a perda de vários eventos.  
  
    3.  **Nenhuma perda de eventos**. Selecione esta opção para impedir a perda de evento. A seleção dessa opção não é recomendável.  
  
        > [!NOTE]  
        >  Alguns eventos como **sqlos.wait_info** não são compatíveis com o modo de retenção de evento **Nenhuma perda de eventos** .  
  
3.  Para especificar as opções **Latência máxima de expedição** da sessão de evento, faça o seguinte:  
  
    1.  **Em segundos**. Selecione esta opção para prolongar ou encurtar a latência máxima de expedição. Use as setas para cima e para baixo a fim de especificar a latência máxima de expedição em segundos.  
  
    2.  **Ilimitado**. Selecione esta opção para que os eventos sejam expedidos somente quando o buffer estiver cheio.  
  
4.  Na caixa **Tamanho máximo da memória** , insira o tamanho máximo da memória. Os eventos existentes são removidos quando esse valor é atingido. Você pode selecionar outra unidade de armazenamento na lista suspensa.  
  
5.  Na caixa **Tamanho máximo de evento** , insira o tamanho máximo dos eventos que são muito grandes para caber no **Tamanho máximo da memória**. Se você não estiver coletando eventos muito grandes, não será necessário configurar essa opção. Você pode selecionar outra unidade de armazenamento na lista suspensa.  
  
6.  Para especificar as opções **Modo de partição de memória** da sessão de evento, faça o seguinte:  
  
    1.  **None**. Selecione esta opção se você não desejar um modo de partição de memória.  
  
    2.  **Por nó**. Selecione esta opção se você não desejar particionar a memória por nó.  
  
    3.  **Por CPU**. Selecione esta opção se você desejar particionar a memória por CPU.  
  
 Para restaurar os valores padrão de configuração das propriedades de sessão precedentes, clique em **Restaurar Padrões**.  
  
## <a name="see-also"></a>Consulte também  
 [Criar uma sessão de eventos estendidos usando o Editor de consultas](../../2014/database-engine/create-an-extended-events-session-using-query-editor.md)   
 [Criar uma sessão de eventos estendidos usando o Assistente de &#40;Pesquisador de objetos&#41;](../ssms/object/object-explorer.md)   
 [Criar script de uma sessão de evento estendido](../../2014/database-engine/script-an-extended-event-session.md)  
  
  
