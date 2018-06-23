---
title: Criar uma sessão de eventos estendidos usando o Assistente (Pesquisador de objetos) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- Sql12.ssms.XeWizard.Summary.f1
- Sql12.ssms.XeWizard.SetSessionProperties.f1
- Sql12.ssms.XeWizard.CaptureAddFields.f1
- Sql12.ssms.XeWizard.SelectEvents.f1
- Sql12.ssms.XeWizard.SpecifySessionTargets.f1
- Sql12.ssms.XeWizard.Welcome.f1
- sql12.ssms.XeWizard.Welcome.f1
- Sql12.ssms.XeWizard.ChooseTemplate.f1
- Sql12.ssms.XeWizard.SetSessionEventFilters.f1
- Sql12.ssms.XeWizard.Results.f1
helpviewer_keywords:
- Sql11.ssms.XeWizard.CaptureAddFields.f1
- Sql11.ssms.XeWizard.SetSessionEventFilters.f1
- Sql11.ssms.XeWizard.SpecifySessionTargets.f1
- Sql11.ssms.XeWizard.Results.f1
- Sql11.ssms.XeWizard.ChooseTemplate.f1
- Sql11.ssms.XeWizard.SetSessionProperties.f1
- Sql11.ssms.XeWizard.Welcome.f1
- Sql11.ssms.XeWizard.Summary.f1
- Sql11.ssms.XeWizard.SelectEvents.f1
ms.assetid: 80c0456f-17c0-41d8-b2aa-502a2f3bb6de
caps.latest.revision: 28
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 69a63b1b360a1ba1c0e9a106dbb78f215f9eca71
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36116217"
---
# <a name="create-an-extended-events-session-using-the-wizard-object-explorer"></a>Criar uma sessão de Eventos Estendidos usando o assistente (Pesquisador de Objetos)
  Para ajudar você a selecionar e capturar eventos no servidor, os Eventos Estendidos incluem um Assistente para Nova Sessão que o guiará pelas etapas de criação de uma sessão de Eventos Estendidos. O Assistente para Nova Sessão expõe a maioria da funcionalidade de Eventos Estendidos. A caixa de diálogo [Nova Sessão](../../2014/database-engine/create-an-extended-events-session-using-the-new-session-dialog.md) também permite definir uma sessão de Eventos Estendidos que captura, exibe e analisa seus dados. A caixa de diálogo Nova Sessão expõe toda a funcionalidade de Eventos Estendidos.  
  
### <a name="to-open-the-new-session-wizard"></a>Para abrir o Assistente para Nova Sessão  
  
1.  No Pesquisador de Objetos, expanda o nó **Gerenciamento** e, em seguida, expanda **Eventos Estendidos**.  
  
2.  Clique com o botão direito do mouse em **Sessões** e clique em **Assistente para Nova Sessão**.  
  
### <a name="use-the-following-new-session-wizard-pages-to-create-an-event-session"></a>Use as seguintes páginas do Assistente para Nova Sessão para criar uma sessão de evento.  
  
-   [Introdução](#BKMK_Welcome)  
  
-   [Definir propriedades de sessão](#BKMK_SetSessionProperties)  
  
-   [Escolher modelo](#BKMK_ChooseTemplate)  
  
-   [Selecionar eventos a serem capturados](#BKMK_SelectEventsToCapture)  
  
-   [Capturar campos globais](#BKMK_CaptureGlobalFields)  
  
-   [Definir filtros de eventos de sessão](#BKMK_SetSessionEventFilters)  
  
-   [Especificar armazenamento de dados de sessão](#BKMK_SpecifySessionDataOutput)  
  
-   [Resumo](#BKMK_Summary)  
  
-   [Criar sessão de evento](#BKMK_CreateEventSession)  
  
##  <a name="BKMK_Welcome"></a> Introdução  
 Na página **Introdução** , faça o seguinte:  
  
-   Na página **Introdução** do Assistente para Nova Sessão, clique em **Avançar**.  
  
     Marque a caixa de seleção **Não mostrar esta página novamente** caso pretenda usar o assistente mais de uma vez e não queira ler a introdução cada vez que o assistente for iniciado.  
  
##  <a name="BKMK_SetSessionProperties"></a> Definir propriedades de sessão  
 Na página **Definir Propriedades da Sessão** , faça o seguinte:  
  
-   Na caixa **Nome da sessão** , digite um nome significativo para a sessão de evento.  
  
     Para iniciar a sessão ao inicializar o servidor, marque a caixa de seleção **Iniciar a sessão de evento na inicialização do servidor** e clique em **Avançar**.  
  
##  <a name="BKMK_ChooseTemplate"></a> Escolher modelo  
 Na página **Escolher Modelo** , faça o seguinte:  
  
-   Selecione a opção **Usar este modelo de sessão de evento** para selecionar um dos modelos de um conjunto de modelos pré-configurados projetados para problemas comuns. Selecione o modelo desejado na lista suspensa e clique em **Avançar**.  
  
     -ou-  
  
-   Selecione a opção **Não usar um modelo** caso não deseje usar nenhum modelo pré-configurado e clique em **Avançar**.  
  
##  <a name="BKMK_SelectEventsToCapture"></a> Selecionar eventos a serem capturados  
 Na página **Selecionar Eventos a Serem Capturados** página, faça o seguinte:  
  
1.  Selecione os eventos que você deseja capturar na **Biblioteca de eventos**e clique na seta para a direita. Você pode selecionar vários eventos na Biblioteca de Eventos usando Shift+Clique ou Ctrl+Clique.  
  
     Na caixa da lista suspensa, você pode especificar como deseja procurar os eventos a serem capturados. Por exemplo, você pode procurar nomes de evento ou nomes de evento e suas descrições. Você pode procurar qualquer palavra na tabela inserindo o texto que deseja procurar na caixa **Biblioteca de eventos** . Por exemplo, para localizar o evento **lock_acquired** , insira **lock**ou **lock acquire**.  
  
     Os eventos selecionados aparecerão na caixa **Eventos selecionados** . Para remover eventos da caixa **Eventos selecionados** , clique na seta para a esquerda.  
  
2.  Depois que você selecionar os eventos a serem capturados, clique em **Avançar**.  
  
    > [!NOTE]  
    >  Os eventos do canal de **Depuração** são ocultos por padrão. Para exibir os eventos de depuração, selecione **Depurar** na lista suspensa **Canal** .  
  
##  <a name="BKMK_CaptureGlobalFields"></a> Capturar campos globais  
 Você usa campos globais (também denominados ações) para associar uma ou várias ações a seus eventos selecionados. Se você selecionou um modelo na página **Escolher Modelo** , todos os campos globais definidos no modelo serão exibidos nesta página.  
  
 Na página **Capturar Campos Globais** , faça o seguinte:  
  
-   Selecione os campos globais que você deseja capturar para a sessão de evento e clique em **Avançar**.  
  
     Você pode remover ou adicionar campos globais marcando ou desmarcando a caixa de seleção ao lado do campo global.  
  
    > [!NOTE]  
    >  As ações selecionadas são classificadas por **Nome** , permitindo que você exiba as ações associadas em ordem alfabética. Você pode realizar a classificação por descrição ou pelo status habilitar/desabilitar clicando no título de coluna ao lado do nome de campo.  
  
##  <a name="BKMK_SetSessionEventFilters"></a> Definir filtros de eventos de sessão  
 Você pode aplicar filtros (também denominados predicados) para limitar os eventos a serem capturados. Na página **Definir Filtros de Eventos de Sessão** , faça o seguinte:  
  
1.  Se você não estiver usando um modelo pré-configurado, crie seus critérios de filtro e clique em **Avançar**.  
  
     Se você estiver usando um modelo pré-configurado, na seção **Filtros do modelo (somente leitura)** , o Assistente para Nova Sessão listará os filtros já criados com base no modelo.  
  
2.  Na seção **Filtros adicionais** , você pode configurar filtros adicionais para a sessão de evento.  
  
     Os filtros que você configura se aplicam a todos os eventos selecionados. O Assistente para Nova Sessão não oferece suporte à configuração de filtros para cada evento.  
  
    > [!NOTE]  
    >  Quando você configurar uma cláusula de grupo para o filtro, serão removidos os parênteses redundantes do filtro depois que o resultado for salvo. Por exemplo, se você criar um agrupamento de filtros **Cláusula 1** e **Cláusula 2**, aparecerão parênteses delimitando as cláusulas. Depois que você salvar o filtro, os parênteses redundantes serão removidos. A remoção dos parênteses não afetará a lógica do filtro.  
  
##  <a name="BKMK_SpecifySessionDataOutput"></a> Especificar armazenamento de dados de sessão  
 Use a página **Especificar Armazenamento de Dados da Sessão** para especificar como coletar os dados para análise. Os Eventos Estendidos do SQL Server usam destinos para saída de dados. Os destinos armazenam dados de evento e podem executar ações como gravar um arquivo e agregar dados de evento. Especifique como coletar os dados para análise e, na página **Especificar Armazenamento de Dados da Sessão** , faça o seguinte:  
  
1.  Para conjuntos de dados grandes e registros históricos de criação, marque a caixa de seleção **Salvar dados em um arquivo para análise posterior** e faça o seguinte:  
  
    1.  Na caixa **Nome do arquivo no servidor** , insira o caminho e o nome do arquivo ou clique em **Procurar** para especificar o diretório de arquivos no servidor onde você deseja salvar os dados.  
  
    2.  Na caixa **Tamanho máximo de arquivo** , especifique um tamanho máximo de arquivo a ser usado como destino do arquivo. Se você não especificar o tamanho máximo do arquivo, este crescerá até que o disco fique cheio. O tamanho de arquivo padrão é 1 GB (gigabyte).  
  
    3.  Marque a caixa de seleção **Habilitar substituição de arquivo** para habilitar a substituição de arquivo para o destino de arquivo.  
  
    4.  Na caixa **Número máximo de arquivo** , especifique o número máximo de arquivos a ser retido no sistema de arquivos.  
  
2.  Para coletar dados recentes, marque a caixa de seleção **Trabalhar somente com os dados mais recentes (destino do buffer de anéis)** e faça o seguinte:  
  
    1.  Na caixa **Número de eventos a serem mantidos** , insira ou selecione o número de eventos que deseja manter usando as setas para cima e para baixo.  
  
    2.  Na caixa **Tamanho máximo da memória do buffer** , especifique a quantidade máxima de memória de buffer a ser usada. Os eventos existentes são removidos quando esse valor é atingido.  
  
    3.  Se você desejar manter um número específico de eventos de cada tipo no buffer, marque a caixa de seleção **Manter um número específico de eventos (por tipo) quando o buffer estiver cheio** .  
  
    4.  Na caixa **Número de eventos a serem mantidos (por tipo)** , insira ou selecione o número de eventos (por tipo) que deseja manter usando as setas para cima e para baixo.  
  
##  <a name="BKMK_Summary"></a> Resumo  
 Na página **Resumo** , faça o seguinte:  
  
1.  Verifique se suas seleções estão corretas. Expanda os nós de sessão de evento para verificar se todas as seleções serão incluídas na sessão de evento.  
  
2.  Clique em **Script** para exportar o script de criação de sessão para uma nova janela do Editor de Consultas.  
  
3.  Clique em **Concluir** para criar a sessão de evento.  
  
##  <a name="BKMK_CreateEventSession"></a> Criar sessão de evento  
 Na página **Criar Sessão de Evento** , depois que a sessão de evento for criada, faça o seguinte:  
  
1.  Clique em **Iniciar a sessão de evento imediatamente após a criação da sessão** para iniciar a sessão depois que você fechar o assistente. Você deve iniciar a sessão de evento imediatamente após a criação da sessão para que possa observar os dados dinâmicos.  
  
2.  Clique em **Observar dados dinâmicos na tela à medida que eles são capturados** para exibir os dados dinâmicos da sua sessão de evento. Os dados dinâmicos começarão a exibir o rastreamento imediatamente depois que a sessão for criada.  
  
## <a name="see-also"></a>Consulte também  
 [Criar uma sessão de Eventos Estendidos usando a caixa de diálogo Nova Sessão](../../2014/database-engine/create-an-extended-events-session-using-the-new-session-dialog.md)  
  
  