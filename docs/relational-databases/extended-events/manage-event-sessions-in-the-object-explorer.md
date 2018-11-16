---
title: Gerenciar sessões de evento no Pesquisador de Objetos | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xevents
ms.topic: conceptual
ms.assetid: 16849e38-d3fb-414d-8dcb-797b5ffce6ee
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 9cf09d6a2e6c4b1699c6c3e6d213bea0d617f2a3
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/15/2018
ms.locfileid: "51681304"
---
# <a name="manage-event-sessions-in-the-object-explorer"></a>Gerenciar sessões de evento no Pesquisador de Objetos
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  Este tópico aborda as ações que você pode executar no **Pesquisador de Objetos** que afetam os Eventos Estendidos:  
  
-   Criar uma sessão de Eventos Estendidos  
  
-   Iniciando ou interrompendo uma sessão de Eventos Estendidos  
  
-   Exportar uma sessão de Eventos Estendidos  
  
-   Importar um modelo da sessão de Eventos Estendidos  
  
-   Editar uma sessão de Eventos Estendidos  
  
-   Excluir uma sessão de Eventos Estendidos  
  
## <a name="create-an-extended-events-session"></a>Criar uma sessão de Eventos Estendidos  
 Para obter mais informações sobre como criar uma sessão de Eventos Estendidos, consulte [Criar uma sessão de Eventos Estendidos](https://msdn.microsoft.com/library/34b1e95a-a80e-4aca-9201-abde47f2ca74).  
  
## <a name="starting-or-stopping-an-extended-events-session"></a>Iniciando ou interrompendo uma sessão de Eventos Estendidos  
 Você pode iniciar ou interromper uma sessão de Eventos Estendidos através do **Editor de Consultas** usando a instrução **ALTER EVENT SESSION** ou usando o nó **Eventos Estendidos** do **Pesquisador de Objetos**.  
  
 Quando você interrompe uma sessão de eventos, a sessão não é mais listada como uma sessão ativa no DMV (exibição de gerenciamento dinâmico) sys.dm_xe_sessions. No entanto, a definição de sessão permanece intacta e você pode reiniciar a sessão. Para remover completamente uma definição de sessão, você deve excluir a sessão.  
  
 Para iniciar ou interromper uma sessão de Eventos Estendidos, você deve ter a permissão ALTER ANY EVENT SESSION.  
  
 Ao interromper uma sessão que usa um destino na memória, como o buffer de anéis, particionamento, emparelhamento de eventos ou destinos do contador de eventos síncrono, todas as informações armazenadas no buffer da sessão (a coluna target_data do sys.dm_xe_session_targets DMV) serão perdidas. Para acessar os dados do evento após interromper a sessão, salve os dados antes de interrompê-la ou configure a sessão para usar o destino de arquivo.  
  
### <a name="start-or-stop-an-extended-events-session-using-query-editor"></a>Iniciar ou interromper uma sessão de Eventos Estendidos usando o Editor de Consultas  
 Para iniciar uma sessão, emita as seguintes instruções, substituindo *session_name* pelo nome da sessão de Eventos Estendidos:  
  
```  
ALTER EVENT SESSION [session_name]  
ON SERVER  
STATE = START  
```  
  
 Para interromper uma sessão, emita as seguintes instruções, substituindo *session_name* pelo nome da sessão de Eventos Estendidos:  
  
```  
ALTER EVENT SESSION [session_name]  
ON SERVER  
STATE = STOP  
```  
  
### <a name="start-or-stop-an-extended-events-session-in-object-explorer"></a>Iniciar ou interromper uma sessão de Eventos Estendidos no Pesquisador de Objetos  
 Para iniciar ou interromper uma sessão de Eventos Estendidos no **Pesquisador de Objetos**, expanda os nós **Gerenciamento**, **Eventos Estendidos**e **Sessões** , clique com o botão direito do mouse em uma sessão e clique em **Iniciar Sessão** ou **Interromper Sessão**.  
  
## <a name="export-an-extended-events-session-template"></a>Exportar um modelo da sessão de Eventos Estendidos  
 Você pode exportar uma sessão de Eventos Estendidos usando o **Pesquisador de Objetos**e salvá-la como um arquivo de modelo .xml. Por exemplo, talvez você queira exportar uma sessão e aplicar o modelo a uma nova sessão de eventos usando o **Assistente para Nova Sessão** ou o assistente **Nova Sessão** .  
  
 Quando você exportar uma sessão, não se esqueça de salvar o arquivo de modelo em um local que use o sistema de arquivos NTFS e de restringir o acesso aos usuários que tenham autorização para exibir as informações.  
  
 Para exportar uma sessão de Eventos Estendidos usando o **Pesquisador de Objetos**:  
  
1.  Expanda os nós **Gerenciamento**, **Eventos Estendidos**e **Sessões**  
  
2.  Clique com o botão direito do mouse na sessão a ser exportada e selecione **Export Session (Exportar Sessão)**.  
  
3.  Na caixa de diálogo **Salvar Como** , selecione um local para salvar o arquivo, digite o nome do arquivo na caixa **Nome de arquivo** e clique em **Salvar**.  
  
     Se você salvar o arquivo no local de modelo [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] padrão, o modelo aparecerá na lista suspensa de modelos predefinidos quando você usar o **Assistente para Nova Sessão** e a caixa de diálogo **Nova Sessão** .  
  
## <a name="import-an-extended-events-session-template"></a>Importar um modelo da sessão de Eventos Estendidos  
 Usando o **Pesquisador de Objetos**, você pode importar um modelo para uma sessão de Eventos Estendidos. Por exemplo, talvez você queira fazer isso para criar uma sessão de um modelo que foi exportado de outra instância de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Para importar uma sessão de Eventos Estendidos, você deve ter as permissões de **ALTER ANY EVENT SESSION** necessárias.  
  
 Antes de importar um arquivo de modelo, verifique se ele é de uma fonte confiável. os arquivos de modelo devem ser salvos em um local que use o sistema de arquivos NTFS e onde o acesso aos usuários que tenham autorização para exibir as informações seja restrito.  
  
 Para importar uma sessão de Eventos Estendidos:  
  
1.  No **Pesquisador de Objetos**, expanda os nós **Gerenciamento**e **Eventos Estendidos** .  
  
2.  Clique com o botão direito do mouse em **Sessões** e selecione **Nova Sessão**.  
  
3.  Especifique um nome para a sessão.  
  
4.  Expanda a caixa suspensa **Modelo** .  
  
5.  Clique em **\<Arquivo De…> Abrir** e procure a sessão (arquivo XML) que você deseja importar.  
  
 A sessão aparece abaixo do nó **Sessões** . Por padrão, a sessão não é iniciada.  
  
## <a name="edit-an-extended-events-session"></a>Editar uma sessão de Eventos Estendidos  
 Você pode editar uma sessão de Eventos Estendidos no Pesquisador de Objetos.  
  
 Para editar uma sessão de Eventos Estendidos:  
  
1.  No **Pesquisador de Objetos**, expanda os nós **Gerenciamento**, **Eventos Estendidos**e **Sessões** .  
  
2.  Clique com o botão direito do mouse em uma sessão e selecione **Propriedades**.  
  
3.  Na seção **Selecionar uma página** , selecione as páginas que deseja editar.  
  
4.  Depois que você terminar de revisar a sessão de eventos, clique em **OK**.  
  
## <a name="script-an-event-session-definition-using-includetsqlincludestsql-mdmd"></a>Criar o script de uma definição de sessão de eventos usando o [!INCLUDE[tsql](../../includes/tsql-md.md)]  
 O Assistente para Nova Sessão e a caixa de diálogo Nova Sessão têm uma opção Script que gera o [!INCLUDE[tsql](../../includes/tsql-md.md)] que define a sessão de Eventos Estendidos.  
  
 Você pode acessar o [!INCLUDE[tsql](../../includes/tsql-md.md)] de uma sessão de Eventos Estendidos existente clicando o botão direito do mouse no nome da sessão, selecionando **Sessão de Script como**e selecionando **Create para**.  
  
## <a name="delete-an-extended-events-session"></a>Excluir uma sessão de Eventos Estendidos  
 Você pode excluir uma sessão de Eventos Estendidos:  
  
-   No Editor de Consultas usando **DROP EVENT SESSION**.  
  
-   No **Pesquisador de Objetos**.  
  
 Quando você exclui uma sessão de eventos, todas as informações de configuração são removidas e a definição de sessão não aparece mais na exibição de catálogo sys.server_event_sessions.  
  
> [!NOTE]  
>  system_health e AlwaysOn_health são incluídas com [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]; não as exclua. system_health é habilitada por padrão (para obter mais informações, consulte [Usar a sessão de system_health](../../relational-databases/extended-events/use-the-system-health-session.md)). AlwaysOn_health está desativada por padrão. Essas sessões coletam dados que podem ser úteis para diagnosticar problemas de desempenho.  
  
 Para excluir uma sessão de Eventos Estendidos, você deve ter a permissão ALTER ANY EVENT SESSION.  
  
 Para excluir uma sessão de Eventos Estendidos no **Pesquisador de Objetos**:  
  
1.  Expanda os nós **Gerenciamento**, **Eventos Estendidos**e **Sessões** .  
  
2.  Clique com o botão direito do mouse em uma sessão e selecione **Excluir**.  
  
3.  Na caixa de diálogo **Excluir Objeto** , clique em **OK**.  
  
4.  Depois que você terminar de revisar a sessão de eventos, clique em **OK**.  
  
 Para excluir uma sessão de Eventos Estendidos no **Editor de Consultas**, emita as seguintes instruções, substituindo *session_name* pelo nome da sessão de Eventos Estendidos que você deseja excluir:  
  
```  
DROP EVENT SESSION [session_name]  
ON SERVER  
```  
  
  
