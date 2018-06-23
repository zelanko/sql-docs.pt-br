---
title: Trabalhos do SQL Server Agent para pacotes | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- jobs [Integration Services]
- automatic package execution
- scheduling packages [Integration Services]
- SQL Server Agent [Integration Services]
ms.assetid: ecf7a5f9-b8a7-47f1-9ac0-bac07cb89e31
caps.latest.revision: 52
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: c42d355ea40731d1f0774434242eac73b70cc14f
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36115250"
---
# <a name="sql-server-agent-jobs-for-packages"></a>Trabalhos do SQL Server Agent para pacotes
  Você pode automatizar e agendar a execução de pacotes do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] usando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent. Você pode agendar pacotes que são implantados no servidor do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] e está armazenado no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], o Armazenamento de Pacotes [!INCLUDE[ssIS](../../includes/ssis-md.md)] e o sistema de arquivos.  
  
## <a name="sections-in-this-topic"></a>Seções neste tópico  
 Este tópico contém as seguintes seções:  
  
-   [Agendando trabalhos no SQL Server Agent](#jobs)  
  
-   [Agendando pacotes do Integration Services](#packages)  
  
-   [Solucionando problemas de pacotes agendados](#trouble)  
  
##  <a name="jobs"></a> Scheduling Jobs in SQL Server Agent  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] O Agent é o serviço instalado pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que permite automatizar e agendar tarefas executando trabalhos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent. O serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent deve estar sendo executado antes que os trabalhos possam ser executados automaticamente. Para obter mais informações, consulte [Configure SQL Server Agent](../../ssms/agent/configure-sql-server-agent.md).  
  
 O nó do **SQL Server Agent** é exibido no Pesquisador de Objetos em [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] quando você se conecta a uma instância do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)].  
  
 Para automatizar uma tarefa recorrente, crie um trabalho na caixa de diálogo **Novo Trabalho** . Para obter mais informações, consulte [Implementar trabalhos](../../ssms/agent/implement-jobs.md).  
  
 Depois de criar o trabalho, adicione pelo menos uma etapa. Um trabalho pode incluir várias etapas, e cada etapa pode executar uma tarefa diferente. Para obter mais informações, consulte [Gerenciar etapas de trabalho](../../ssms/agent/manage-job-steps.md).  
  
 Depois de criar o trabalho e as etapas do trabalho, crie uma agenda para executar o trabalho. Entretanto, você também pode criar um trabalho agendado para execução manual. Para obter mais informações, veja [Criar e anexar agendamentos a trabalhos](../../ssms/agent/create-and-attach-schedules-to-jobs.md).  
  
 Você pode aperfeiçoar o trabalho configurando opções de notificação, como especificar um operador para enviar uma mensagem de email quando o trabalho for concluído ou adicionar alertas. Para obter mais informações, consulte [Alertas](../../ssms/agent/alerts.md).  
  
##  <a name="packages"></a> Scheduling Integration Services Packages  
 Quando você cria um trabalho do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent para agendar pacotes do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , é necessário adicionar pelo menos uma etapa e definir o tipo da etapa para o **Pacote do SQL Server Integration**. Um trabalho pode incluir várias etapas, e cada etapa pode executar um pacote diferente.  
  
 A execução de um pacote do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] de uma etapa de trabalho é semelhante à execução de um pacote com os utilitários **dtexec** (dtexec.exe) e **DTExecUI** (dtexecui.exe). Em vez de configurar as opções de tempo de execução para um pacote usando as opções de linha de comando ou a caixa de diálogo **Executar Utilitário de Pacote** , defina as opções de tempo de execução na caixa de diálogo **Nova Etapa do Trabalho** . Para obter mais informações sobre as opções para executar um pacote, consulte [Utilitário dtexec](dtexec-utility.md).  
  
 Para obter mais informações, consulte [Agendar um pacote usando o SQL Server Agent](../schedule-a-package-by-using-sql-server-agent.md).  
  
 Para assistir a um vídeo que demonstra como usar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent para executar um pacote, consulte a home page de vídeos, [Como automatizar a execução de pacotes usando o SQL Server Agent (vídeo do SQL Server)](http://go.microsoft.com/fwlink/?LinkId=141771), na Biblioteca MSDN.  
  
##  <a name="trouble"></a> Solução de problemas  
 Uma etapa de trabalho do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent não inicia um pacote, embora o pacote seja executado com êxito no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] e na linha de comando. Há algumas razões comuns para esse problema e várias soluções recomendadas. Para obter mais informações, consulte os recursos a seguir.  
  
-   [!INCLUDE[msCoName](../../includes/msconame-md.md)] Artigo da Base de Dados de Conhecimento, [Um pacote SSIS não é executado quando você chama o pacote SSIS a partir de uma etapa de trabalho do SQL Server Agent](http://support.microsoft.com/kb/918760)  
  
-   Vídeo [Solução de problemas: execução de pacotes SSIS usando o SQL Server Agent (vídeo do SQL Server)](http://go.microsoft.com/fwlink/?LinkId=141772), na Biblioteca MSDN.  
  
 Depois que uma etapa de trabalho do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent iniciar um pacote, a execução do pacote poderá falhar ou o pacote poderá ser executado com êxito, mas com resultados inesperados. Você pode usar uma das ferramentas a seguir para solucionar esses problemas.  
  
-   Para pacotes armazenados no banco de dados MSDB do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , o repositório de pacotes de [!INCLUDE[ssIS](../../includes/ssis-md.md)] , ou em uma pasta no computador local, você pode usar o **Visualizador do Arquivo de Log** , bem como todos os logs e arquivos de despejo de depuração gerados durante a execução do pacote.  
  
     **Para usar o Visualizador do Arquivo de Log, siga os procedimentos a seguir.**  
  
    1.  Clique com o botão direito do mouse no trabalho do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent no Pesquisador de Objetos. Em seguida, clique em **Exibir Histórico**.  
  
    2.  Localize a execução do trabalho na caixa **Resumo do arquivo de log** com a mensagem **falha no trabalho** na coluna **Mensagem** .  
  
    3.  Expanda o nó do trabalho, e clique na etapa de trabalho para exibir os detalhes da mensagem na área abaixo da caixa **Resumo do arquivo de log** .  
  
-   Para pacotes armazenados no banco de dados SSISDB, você também pode usar o **Visualizador do Arquivo de Log** , bem como todos os logs e arquivos de despejo de depuração gerados durante a execução do pacote. Além de isso, você pode usar os relatórios do servidor do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
     **Para localizar informações nos relatórios para a execução do pacote associada à execução de um trabalho, siga os procedimentos abaixo.**  
  
    1.  Siga as etapas anteriores para exibir os detalhes da mensagem para a etapa de trabalho.  
  
    2.  Localize a ID da execução listada na mensagem.  
  
    3.  Expanda o nó Catálogo do Integration Services no Pesquisador de Objetos.  
  
    4.  Clique com o botão direito do mouse em SSISDB, aponte para Relatórios, depois para Relatórios Padrão e, então, clique em Todas as Execuções.  
  
    5.  No relatório **Todas as Execuções** , localize a ID de execução na coluna **ID** . Clique em **Visão Geral**, **Todas as Mensagens**ou **Desempenho de Execução** para exibir informações sobre essa execução de pacote.  
  
         Para obter mais informações sobre os relatórios Visão Geral, Todas as Mensagens e Desempenho de Execução, consulte [Relatórios do servidor do Integration Services](../reports-for-the-integration-services-server.md).  
  
## <a name="external-resources"></a>Recursos externos  
  
-   Artigo da Base de Dados de Conhecimento [Um pacote do SSIS não é executado quando você chama o pacote do SSIS a partir de uma etapa de trabalho do SQL Server Agent](http://support.microsoft.com/kb/918760), no site do [!INCLUDE[msCoName](../../includes/msconame-md.md)]  
  
-   Vídeo [Solução de problemas: execução de pacotes SSIS usando o SQL Server Agent (vídeo do SQL Server)](http://go.microsoft.com/fwlink/?LinkId=141772), na Biblioteca MSDN  
  
-   Vídeo [Como automatizar a execução de pacotes usando o SQL Server Agent (vídeo do SQL Server)](http://go.microsoft.com/fwlink/?LinkId=141771), na Biblioteca MSDN  
  
-   Artigo técnico [Checking SQL Server Agent jobs using Windows PowerShell](http://go.microsoft.com/fwlink/?LinkId=165675)(Verificando trabalhos do SQL Server Agent usando o Windows PowerShell), em mssqltips.com  
  
-   Artigo técnico [Auto alert for SQL Agent jobs when they are enabled or disabled](http://go.microsoft.com/fwlink/?LinkId=165676)(Alerta automático para trabalhos do SQL Agent quando estão habilitados ou desabilitados), em mssqltips.com  
  
-   Entrada de blog, [Configuring SQL Agent Jobs to Write to Windows Event Log](http://go.microsoft.com/fwlink/?LinkId=220745)(Configurando trabalhos do SQL Agent para gravação Log de Eventos do Windows), em mssqltips.com.  
  
  