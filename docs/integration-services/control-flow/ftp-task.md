---
title: Tarefa FTP | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.ftptask.f1
- sql13.dts.designer.ftptask.general.f1
- sql13.dts.designer.ftptask.filetransfer.f1
helpviewer_keywords:
- FTP task [Integration Services]
ms.assetid: 41c3f2c4-ee04-460a-9822-bb9ae4036c2e
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: b183ff23efd18a19e08033e64691b723d4b4f323
ms.sourcegitcommit: 7ccb8f28eafd79a1bddd523f71fe8b61c7634349
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/20/2019
ms.locfileid: "58276025"
---
# <a name="ftp-task"></a>Tarefa FTP
  A tarefa FTP carrega e baixa arquivos de dados, bem como gerencia diretórios em servidores. Por exemplo, um pacote pode baixar arquivos de dados de um servidor remoto ou de um local de Internet como parte de um fluxo de trabalho de pacote do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . Você pode usar a tarefa FTP para os seguintes propósitos:  
  
-   Copiar diretórios e arquivos de dados de um diretório para outro, antes ou depois de mover dados, e aplicar transformações nos dados.  
  
-   Fazer logon em um local FTP de origem e copiar arquivos ou pacotes em um diretório de destino.  
  
-   Baixar arquivos de um local FTP e aplicar transformações em dados de coluna antes de carregar os dados em um banco de dados.  
  
 Em tempo de execução, a tarefa FTP é conectada a um servidor usando um gerenciador de conexões de FTP. O gerenciador de conexões de FTP é configurado separadamente da tarefa FTP e, em seguida, é referido na tarefa FTP. O gerenciador de conexões de FTP inclui as configurações do servidor, as credenciais para acessar o servidor FTP e as opções como o tempo limite e o número de tentativas para conexão com o servidor. Para obter mais informações, consulte [Gerenciador de Conexões de FTP](../../integration-services/connection-manager/ftp-connection-manager.md).  
  
> [!IMPORTANT]  
>  O gerenciador de conexões de FTP dá suporte apenas para autenticação anônima e autenticação básica. Ele não suporta a Autenticação do Windows.  
  
 Ao acessar um arquivo local ou um diretório local, a tarefa FTP usa um gerenciador de conexões de arquivos ou informações de caminho armazenadas em uma variável. Por outro lado, ao acessar um arquivo remoto ou um diretório remoto, a tarefa FTP usa um caminho especificado diretamente no servidor remoto, conforme especificado no gerenciador de conexões de FTP, ou as informações de caminho armazenadas em uma variável. Para obter mais informações, consulte [Gerenciador de Conexões de Arquivos](../../integration-services/connection-manager/file-connection-manager.md) e [Variáveis do Integration Services &#40;SSIS&#41;](../../integration-services/integration-services-ssis-variables.md).  
  
 Isso significa que a tarefa FTP pode receber vários arquivos e excluir diversos arquivos remotos, mas a tarefa só poderá enviar um arquivo e só poderá excluir um arquivo local se usar um gerenciador de conexões, porque um gerenciador de conexões de arquivos pode acessar só um arquivo. Para acessar vários arquivos locais, a tarefa FTP deve usar uma variável para fornecer as informações de caminho. Por exemplo, uma variável que contém "C:\Test\&#42;.txt" fornece um caminho que dá suporte à exclusão ou envio de todos os arquivos com uma extensão .txt no diretório Test.  
  
 Para enviar vários arquivos e acessar diversos arquivos locais e diretórios, você também pode executar diversas vezes a tarefa FTP incluindo a tarefa em um Loop Foreach. O Loop Foreach pode enumerar arquivos em um diretório usando o enumerador For Each File. Para obter mais informações, consulte [Foreach Loop Container](../../integration-services/control-flow/foreach-loop-container.md).  
  
 A tarefa de FTP dá suporte para os caracteres curinga *?* e *\** nos caminhos. Isso permite que a tarefa acesse vários arquivos. Porém, você só pode usar caracteres curinga na parte do caminho que especifica o nome de arquivo. Por exemplo, C:\MyDirectory\\*.txt é um caminho válido, mas C:\\\*\MyText.txt não é.  
  
 Os operações de FTP podem ser configuradas para interromper a tarefa Sistema de Arquivos quando a operação falha ou para transferir arquivos no modo ASCII. As operações que enviam e recebem cópias de arquivos podem ser configuradas para substituir arquivos de destino e diretórios.  
  
## <a name="predefined-ftp-operations"></a>Operações de FTP predefinidas  
 A tarefa FTP inclui um conjunto predefinido de operações. A tabela a seguir descreve essas operações.  
  
|Operação|Descrição|  
|---------------|-----------------|  
|Enviar arquivos|Envia um arquivo do computador local para o servidor FTP.|  
|Receber arquivos|Salva um arquivo do servidor FTP no computador local.|  
|Criar diretório local|Cria uma pasta no computador local.|  
|Criar diretório remoto|Cria uma pasta no servidor FTP.|  
|Remover diretório local|Exclui uma pasta no computador local.|  
|Remover diretório remoto|Exclui uma pasta no servidor FTP.|  
|Excluir arquivos locais|Exclui um arquivo no computador local.|  
|Excluir arquivos remotos|Exclui um arquivo no servidor FTP.|  
  
## <a name="custom-log-entries-available-on-the-ftp-task"></a>Entradas de log personalizadas disponíveis na tarefa FTP  
 A tabela a seguir relaciona as entradas de log personalizadas da tarefa FTP. Para obter mais informações, consulte [Log do SSIS &#40;Integration Services&#41;](../../integration-services/performance/integration-services-ssis-logging.md).  
  
|Entrada de log|Descrição|  
|---------------|-----------------|  
|**FTPConnectingToServer**|Indica que a tarefa iniciou uma conexão com o servidor FTP.|  
|**FTPOperation**|Informa o início e o tipo de operação de FTP que a tarefa executa.|  
  
## <a name="related-tasks"></a>Related Tasks  
 Você pode definir propriedades pelo Designer do [!INCLUDE[ssIS](../../includes/ssis-md.md)] ou programaticamente.  
  
 Para obter informações sobre como definir essas propriedades no Designer do [!INCLUDE[ssIS](../../includes/ssis-md.md)] , consulte [Definir as propriedades de uma tarefa ou um contêiner](https://msdn.microsoft.com/library/52d47ca4-fb8c-493d-8b2b-48bb269f859b).  
  
 Para obter mais informações sobre como definir essas propriedades de forma programática, consulte <xref:Microsoft.SqlServer.Dts.Tasks.FtpTask.FtpTask>.  
  
## <a name="ftp-task-editor-general-page"></a>Editor da Tarefa FTP (página Geral)
  Use a página **Geral** da caixa de diálogo **Editor da Tarefa FTP** para especificar o gerenciador de conexões que estabelece conexão com o servidor FTP com o qual a tarefa se comunica. Você também pode nomear e descrever a tarefa FTP.  
  
### <a name="options"></a>Opções  
 **FtpConnection**  
 Selecione um gerenciador de conexões FTP existente ou clique em \<**Nova conexão…**> para criar um gerenciador de conexões.  
  
> [!IMPORTANT]  
>  O gerenciador de conexões de FTP dá suporte apenas para autenticação anônima e autenticação básica. Ele não suporta a Autenticação do Windows.  
  
 **Tópicos relacionados**: [Gerenciador de Conexões de FTP](../../integration-services/connection-manager/ftp-connection-manager.md), [Editor do Gerenciador de Conexões de FTP](../../integration-services/connection-manager/ftp-connection-manager-editor.md)  
  
 **StopOnFailure**  
 Indique se a tarefa FTP deve ser encerrada se a operação FTP falhar.  
  
 **Nome**  
 Forneça um nome exclusivo para a tarefa FTP. Esse nome é usado como rótulo no ícone de tarefa.  
  
> [!NOTE]  
>  Os nomes das tarefas devem ser exclusivos em um pacote.  
  
 **Descrição**  
 Digite uma descrição para a tarefa FTP.  
  
## <a name="ftp-task-editor-file-transfer-page"></a>Editor da Tarefa FTP (página Transferência de Arquivos)
  Use a página **Transferência de Arquivos** da caixa de diálogo **Editor da Tarefa FTP** para configurar a operação FTP executada pela tarefa.  
  
### <a name="options"></a>Opções  
 **IsRemotePathVariable**  
 Indique se o caminho remoto deve ser armazenado em uma variável. As opções dessa propriedade são listadas na tabela a seguir.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**Verdadeiro**|O caminho de destino é armazenado em uma variável. Ao selecionar esse valor, a opção dinâmica **RemoteVariable**será exibida.|  
|**Falso**|O caminho de destino é especificado em um gerenciador de conexões de Arquivo. Ao selecionar esse valor, a opção dinâmica **RemotePath**será exibida.|  
  
 **OverwriteFileAtDestination**  
 Especifique se um arquivo no destino pode ser substituído.  
  
 **IsLocalPathVariable**  
 Indique se o caminho local deve ser armazenado em uma variável. As opções dessa propriedade são listadas na tabela a seguir.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**Verdadeiro**|O caminho de destino é armazenado em uma variável. Ao selecionar esse valor, a opção dinâmica **LocalVariable**será exibida.|  
|**Falso**|O caminho de destino é especificado em um gerenciador de conexões de Arquivo. Ao selecionar esse valor, a opção dinâmica **LocalPath**será exibida.|  
  
 **Operação**  
 Selecione a operação FTP a executar. As opções dessa propriedade são listadas na tabela a seguir.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**Enviar arquivos**|Enviar arquivos. Ao selecionar esse valor, as opções dinâmicas **LocalVariable**, **LocalPathRemoteVariable** e **RemotePath**serão exibidas.|  
|**Receber arquivos**|Receber arquivos. Ao selecionar esse valor, as opções dinâmicas **LocalVariable**, **LocalPathRemoteVariable** e **RemotePath**serão exibidas.|  
|**Criar diretório local**|Criar um diretório local. Ao selecionar esse valor, as opções dinâmicas **LocalVariable** e **LocalPath**serão exibidas.|  
|**Criar diretório remoto**|Criar um diretório remoto. Ao selecionar esse valor, as opções dinâmicas **RemoteVariable** e **RemotelPath**serão exibidas.|  
|**Remover diretório local**|Remover diretório local. Ao selecionar esse valor, as opções dinâmicas **LocalVariable** e **LocalPath**serão exibidas.|  
|**Remover diretório remoto**|Remover um diretório remoto. Ao selecionar esse valor, as opções dinâmicas **RemoteVariable** e **RemotePath**serão exibidas.|  
|**Excluir arquivos locais**|Excluir arquivos locais. Ao selecionar esse valor, as opções dinâmicas **LocalVariable** e **LocalPath**serão exibidas.|  
|**Excluir arquivos remotos**|Excluir arquivos remotos. Ao selecionar esse valor, as opções dinâmicas **RemoteVariable** e **RemotePath**serão exibidas.|  
  
 **IsTransferASCII**  
 Indique se os arquivos transferidos para e do servidor FTP remoto devem ser transferidos em modo ASCII.  
  
### <a name="isremotepathvariable-dynamic-options"></a>Opções dinâmicas de IsRemotePathVariable  
  
#### <a name="isremotepathvariable--true"></a>IsRemotePathVariable = True  
 **RemoteVariable**  
 Selecione uma variável definida pelo usuário existente ou clique em \<**Nova variável...**> para criar uma variável definida pelo usuário.  
  
 **Tópicos relacionados:** [Variáveis do Integration Services &#40;SSIS&#41;](../../integration-services/integration-services-ssis-variables.md), Adicionar variável  
  
#### <a name="isremotepathvariable--false"></a>IsRemotePathVariable = False  
 **RemotePath**  
 Selecione um gerenciador de conexões FTP existente ou clique em \<**Nova conexão…**> para criar um gerenciador de conexões.  
  
 **Tópicos relacionados:** [Gerenciador de Conexões de FTP](../../integration-services/connection-manager/ftp-connection-manager.md), [Editor do Gerenciador de Conexões de FTP](../../integration-services/connection-manager/ftp-connection-manager-editor.md)  
  
### <a name="islocalpathvariable-dynamic-options"></a>Opções dinâmicas de IsLocalPathVariable  
  
#### <a name="islocalpathvariable--true"></a>IsLocalPathVariable = True  
 **LocalVariable**  
 Selecione uma variável definida pelo usuário existente ou clique em \<**Nova variável...**> para criar uma variável.  
  
 **Tópicos relacionados:** [Variáveis do Integration Services &#40;SSIS&#41;](../../integration-services/integration-services-ssis-variables.md), Adicionar variável  
  
#### <a name="islocalpathvariable--false"></a>IsLocalPathVariable = False  
 **LocalPath**  
 Selecione um gerenciador de conexões de arquivos existente ou clique em \<**Nova conexão…**> para criar um gerenciador de conexões.  
  
 **Tópicos relacionados**: [Gerenciador de Conexões de Arquivos Simples](../../integration-services/connection-manager/flat-file-connection-manager.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Tarefas do Integration Services](../../integration-services/control-flow/integration-services-tasks.md)   
 [Fluxo de Controle](../../integration-services/control-flow/control-flow.md)  
  
  
