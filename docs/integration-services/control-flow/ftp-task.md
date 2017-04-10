---
title: "Tarefa FTP | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.designer.ftptask.f1"
helpviewer_keywords: 
  - "Tarefa FTP [Integration Services]"
ms.assetid: 41c3f2c4-ee04-460a-9822-bb9ae4036c2e
caps.latest.revision: 52
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 52
---
# Tarefa FTP
  A tarefa FTP carrega e baixa arquivos de dados, bem como gerencia diretórios em servidores. Por exemplo, um pacote pode baixar arquivos de dados de um servidor remoto ou de um local de Internet como parte de um fluxo de trabalho de pacote do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . Você pode usar a tarefa FTP para os seguintes propósitos:  
  
-   Copiar diretórios e arquivos de dados de um diretório para outro, antes ou depois de mover dados, e aplicar transformações nos dados.  
  
-   Fazer logon em um local FTP de origem e copiar arquivos ou pacotes em um diretório de destino.  
  
-   Baixar arquivos de um local FTP e aplicar transformações em dados de coluna antes de carregar os dados em um banco de dados.  
  
 Em tempo de execução, a tarefa FTP é conectada a um servidor usando um gerenciador de conexões de FTP. O gerenciador de conexões de FTP é configurado separadamente da tarefa FTP e, em seguida, é referido na tarefa FTP. O gerenciador de conexões de FTP inclui as configurações do servidor, as credenciais para acessar o servidor FTP e as opções como o tempo limite e o número de tentativas para conexão com o servidor. Para obter mais informações, consulte [Gerenciador de Conexões de FTP](../../integration-services/connection-manager/ftp-connection-manager.md).  
  
> [!IMPORTANT]  
>  O gerenciador de conexões de FTP dá suporte apenas para autenticação anônima e autenticação básica. Ele não suporta a Autenticação do Windows.  
  
 Ao acessar um arquivo local ou um diretório local, a tarefa FTP usa um gerenciador de conexões de arquivos ou informações de caminho armazenadas em uma variável. Por outro lado, ao acessar um arquivo remoto ou um diretório remoto, a tarefa FTP usa um caminho especificado diretamente no servidor remoto, conforme especificado no gerenciador de conexões de FTP, ou as informações de caminho armazenadas em uma variável. Para obter mais informações, consulte [Gerenciador de Conexões de Arquivos](../../integration-services/connection-manager/file-connection-manager.md) e [Variáveis do Integration Services &#40;SSIS&#41;](../../integration-services/integration-services-ssis-variables.md).  
  
 Isso significa que a tarefa FTP pode receber vários arquivos e excluir diversos arquivos remotos, mas a tarefa só poderá enviar um arquivo e só poderá excluir um arquivo local se usar um gerenciador de conexões, porque um gerenciador de conexões de arquivos pode acessar só um arquivo. Para acessar vários arquivos locais, a tarefa FTP deve usar uma variável para fornecer as informações de caminho. Por exemplo, uma variável que contém “C:\Test\\*.txt” fornece um caminho que dá suporte à exclusão ou envio de todos os arquivos com uma extensão .txt no diretório Test.  
  
 Para enviar vários arquivos e acessar diversos arquivos locais e diretórios, você também pode executar diversas vezes a tarefa FTP incluindo a tarefa em um Loop Foreach. O Loop Foreach pode enumerar arquivos em um diretório usando o enumerador For Each File. Para obter mais informações, consulte [Foreach Loop Container](../../integration-services/control-flow/foreach-loop-container.md).  
  
 A tarefa de FTP dá suporte para os caracteres curinga *?* e *\** nos caminhos. Isso permite que a tarefa acesse vários arquivos. Porém, você só pode usar caracteres curinga na parte do caminho que especifica o nome de arquivo. Por exemplo, C:\MyDirectory\\*.txt é um caminho válido, mas C:\\\*\MyText.txt não é.  
  
 Os operações de FTP podem ser configuradas para interromper a tarefa Sistema de Arquivos quando a operação falha ou para transferir arquivos no modo ASCII. As operações que enviam e recebem cópias de arquivos podem ser configuradas para substituir arquivos de destino e diretórios.  
  
## Operações de FTP predefinidas  
 A tarefa FTP inclui um conjunto predefinido de operações. A tabela a seguir descreve essas operações.  
  
|Operação|Description|  
|---------------|-----------------|  
|Enviar arquivos|Envia um arquivo do computador local para o servidor FTP.|  
|Receber arquivos|Salva um arquivo do servidor FTP no computador local.|  
|Criar diretório local|Cria uma pasta no computador local.|  
|Criar diretório remoto|Cria uma pasta no servidor FTP.|  
|Remover diretório local|Exclui uma pasta no computador local.|  
|Remover diretório remoto|Exclui uma pasta no servidor FTP.|  
|Excluir arquivos locais|Exclui um arquivo no computador local.|  
|Excluir arquivos remotos|Exclui um arquivo no servidor FTP.|  
  
## Entradas de log personalizadas disponíveis na tarefa FTP  
 A tabela a seguir relaciona as entradas de log personalizadas da tarefa FTP. Para obter mais informações, consulte [Log do SSIS &#40;Integration Services&#41;](../../integration-services/performance/integration-services-ssis-logging.md) e [Mensagens personalizadas para log](../../integration-services/performance/custom-messages-for-logging.md).  
  
|Entrada de log|Description|  
|---------------|-----------------|  
|**FTPConnectingToServer**|Indica que a tarefa iniciou uma conexão com o servidor FTP.|  
|**FTPOperation**|Informa o início e o tipo de operação de FTP que a tarefa executa.|  
  
## Tarefas relacionadas  
 Você pode definir propriedades pelo Designer do [!INCLUDE[ssIS](../../includes/ssis-md.md)] ou programaticamente.  
  
 Para obter informações sobre como definir essas propriedades no Designer do [!INCLUDE[ssIS](../../includes/ssis-md.md)], consulte [Definir as propriedades de uma tarefa ou um contêiner](../Topic/Set%20the%20Properties%20of%20a%20Task%20or%20Container.md).  
  
 Para obter mais informações sobre como definir essas propriedades de forma programática, consulte <xref:Microsoft.SqlServer.Dts.Tasks.FtpTask.FtpTask>.  
  
## Consulte também  
 [Editor da Tarefa FTP &#40;página Geral&#41;](../../integration-services/control-flow/ftp-task-editor-general-page.md)   
 [Editor da Tarefa FTP &#40;página Transferência de Arquivos&#41;](../../integration-services/control-flow/ftp-task-editor-file-transfer-page.md)   
 [Tarefas do Integration Services](../../integration-services/control-flow/integration-services-tasks.md)   
 [Fluxo de Controle](../../integration-services/control-flow/control-flow.md)  
  
  