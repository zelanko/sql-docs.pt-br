---
title: "Implementa&#231;&#227;o do pacote pai | Microsoft Docs"
ms.custom: ""
ms.date: "03/04/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "pacotes pai [Integration Services]"
ms.assetid: d8f94830-fa27-4151-88df-cbdc6bf0fc80
caps.latest.revision: 24
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 24
---
# Implementa&#231;&#227;o do pacote pai
  Após o balanceamento de carga de pacotes SSIS em vários servidores, a etapa seguinte será criar o pacote pai após os pacotes filho terem sido criados e implantados e os trabalhos do SQL Server Agent remotos criados para executá-los. O pacote pai conterá muitas tarefas Executar Trabalho do SQL Server Agent, sendo cada tarefa responsável por chamar um trabalho diferente do SQL Server Agent que executa um dos pacotes filho. As tarefas Executar Trabalho do SQL Server Agent no pacote pai executam em turnos os vários trabalhos do SQL Server Agent. Cada tarefa no pacote pai contém informações, por exemplo, como se conectar ao servidor remoto e qual trabalho deve ser executado nesse servidor. Para obter mais informações, consulte [Execute SQL Server Agent Job Task](../../integration-services/packages/execute-sql-server-agent-job-task.md).  
  
 Para identificar o pacote pai que executa pacotes filho, em [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], clique com o botão direito do mouse no pacote no Gerenciador de Soluções e clique em **Pacote de Ponto de Entrada**.  
  
## Listando pacotes filho  
 Se você implantar o projeto que contém o pacote pai e os pacotes filhos no servidor do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], poderá ver uma lista dos pacotes filho executados pelo pacote pai. Quando você executa o pacote pai, um relatório **Visão geral** do mesmo é gerado automaticamente no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. O relatório lista os pacotes filho que foram executados pela tarefa Executar Pacote contida no pacote pai, como mostrado na imagem a seguir.  
  
 ![Relatório de visão geral com lista de pacotes filho](../../integration-services/packages/media/overviewreport-childpackagelisting.png "Relatório de visão geral com lista de pacotes filho")  
  
 Para obter mais informações sobre como acessar o relatório **Visão geral** , confira [Reports for the Integration Services Server](../../integration-services/performance/reports-for-the-integration-services-server.md).  
  
## Restrições de precedência no pacote pai  
 Quando você cria restrições de precedência entre as tarefas Executar Trabalho do SQL Server Agent no pacote pai, elas controlam somente a hora em que os trabalhos do SQL Server Agent são iniciados nos servidores remotos. As restrições de precedência não podem receber informações relacionadas ao êxito ou falha dos pacotes filho executados pelas etapas dos trabalhos do SQL Server Agent.  
  
 Isso significa que o êxito ou a falha do pacote filho não se propaga para o pai, porque a única função de Executar Trabalho do SQL Server Agent no pacote pai é solicitar ao trabalho do SQL Server Agent que execute o pacote filho. Depois que o trabalho do SQL Server Agent é chamado com êxito, o pacote pai recebe um resultado do <xref:Microsoft.SqlServer.Dts.Runtime.DTSExecResult.Success>.  
  
 A falha nesse cenário significa apenas que houve uma falha na chamada da tarefa remota do Trabalho do SQL Server Agent. Uma situação em que isso pode acontecer é quando o servidor remoto está inoperante e o agente não responde. No entanto, se o agente disparar, o pacote pai completará sua tarefa com êxito.  
  
> [!NOTE]  
>  Você pode usar uma tarefa Executar SQL que contém uma instrução Transact-SQL de **sp_start_job N'nome_do_pacote'**. Para obter mais informações, consulte [sp_start_job &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-start-job-transact-sql.md).  
  
## Ambiente de depuração  
 Durante o teste do pacote pai, use o ambiente de depuração do designer para executá-lo usando Depurar / Iniciar depuração (F5). Como alternativa, você pode usar o utilitário de prompt de comando, **dtexec**. Para saber mais, veja [dtexec Utility](../../integration-services/packages/dtexec-utility.md).  
  
  