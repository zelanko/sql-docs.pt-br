---
description: Tarefa Transferir Logons
title: Tarefa Transferir Logons | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.transferloginstask.f1
- sql13.dts.designer.transferloginstask.general.f1
- sql13.dts.designer.transferloginstask.logins.f1
helpviewer_keywords:
- Transfer Logins task [Integration Services]
ms.assetid: 1df60fd6-c019-405d-8155-c330dbac2cc1
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 7ff8e4b35d30e9b2504dd128ca9694007647f5eb
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88477909"
---
# <a name="transfer-logins-task"></a>Tarefa Transferir Logons

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  A tarefa Transferir Logons transfere um ou mais logons entre instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="transfer-logins-between-instances-of-sql-server"></a>Transfer logons entre instâncias do SQL Server  
 A tarefa Transferir Logons dá suporte a uma origem e a um destino do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="events"></a>Eventos  
 A tarefa gera um evento de informação com o número de logons transferidos e um evento de aviso quando um logon é substituído.  
  
 A tarefa Transferir Logons não informa o progresso incremental da transferência de logons; informa só 0% e 100% concluídos.  
  
## <a name="execution-value"></a>Valor de execução  
 O valor de execução, definido na propriedade da tarefa **ExecutionValue** retorna o número de logons que são transferidos. Ao atribuir uma variável definida pelo usuário à propriedade **ExecValueVariable** da tarefa Transferir Logons, informações sobre a transferência de logons podem se tornar disponíveis a outros objetos no pacote. Para obter mais informações, consulte [Variáveis do Integration Services &#40;SSIS&#41;](../../integration-services/integration-services-ssis-variables.md) e [Usar variáveis em pacotes](https://msdn.microsoft.com/library/7742e92d-46c5-4cc4-b9a3-45b688ddb787).  
  
## <a name="log-entries"></a>Entradas de log  
 A tarefa Transferir Logons inclui as seguintes entradas de log personalizadas:  
  
-   TransferLoginsTaskStarTransferringObjects    Essa entrada de log informa que a transferência foi iniciada. A entrada do log contém a hora de início.  
  
-   TransferLoginsTaskFinishedTransferringObjects   Essa entrada de log informa que a transferência foi concluída. A entrada do log contém a hora de término.  
  
 Além disso, uma entrada de log para o evento **OnInformation** informa o número de logons que foram transferidos e uma entrada de log para o evento **OnWarning** é gravada para cada logon no destino que for substituído.  
  
## <a name="security-and-permissions"></a>Segurança e permissões  
 Para procurar logons no servidor de origem e criar logons no servidor de destino, o usuário deve ser um membro da função de sysadmin em ambos os servidores.  
  
## <a name="configuration-of-the-transfer-logins-task"></a>Configuração da tarefa Transferir Logons  
 A tarefa Transferira Logons pode ser configurada para transferir todos os logons, só os logons especificados ou todos os logons que só têm acesso a bancos de dados especificados. O logon do sa não pode ser transferido. O logon sa pode ser renomeado; porém, o logon sa renomeado não pode ser transferido.  
  
 Você também pode indicar se a tarefa deve copiar os SIDs (identificadores de segurança) associados aos logons. Se a tarefa Transferir Logons for usada junto com a tarefa Transferir Banco de Dados, os SIDs deverão ser copiados para o destino; caso contrário, os logons transferidos não serão reconhecidos pelo banco de dados de destino.  
  
 No destino, os logons transferidos são desabilitados e senhas aleatórias são atribuídas a eles. Um membro da função de sysadmin no servidor de destino deve alterar as senhas e habilitar os logons antes de os logons poderem ser usados.  
  
 Os logons a serem transferidos já podem existir no destino. A tarefa Transferir Logons pode ser configurada para manipular os logons existentes dos modos a seguir:  
  
-   Substituir os logons existentes.  
  
-   Interromper a tarefa quando houver logons duplicados.  
  
-   Ignorar logons duplicados.  
  
 No tempo de execução, a tarefa Transferir Logons conecta-se aos servidores de origem e de destino usando dois gerenciadores de conexões SMO. Os gerenciadores de conexões SMO são configurados separadamente da tarefa Transferir Logons e depois são referenciados na tarefa Transferir Logons. Os gerenciadores de conexões SMO especificam o servidor e o modo de autenticação a serem usados ao acessar o servidor. Para obter mais informações, consulte [SMO Connection Manager](../../integration-services/connection-manager/smo-connection-manager.md).  
  
 Você pode definir propriedades pelo Designer do [!INCLUDE[ssIS](../../includes/ssis-md.md)] ou programaticamente.  
  
 Para obter mais informações sobre as propriedades que podem ser definidas no [!INCLUDE[ssIS](../../includes/ssis-md.md)] Designer, clique no tópico a seguir:  
  
-   [Página Expressões](../../integration-services/expressions/expressions-page.md)  
  
 Para obter mais informações sobre como definir essas propriedades no [!INCLUDE[ssIS](../../includes/ssis-md.md)] Designer, clique no tópico a seguir:  
  
-   [Definir as propriedades de uma tarefa ou contêiner](https://msdn.microsoft.com/library/52d47ca4-fb8c-493d-8b2b-48bb269f859b)  
  
## <a name="programmatic-configuration-of-the-transfer-logins-task"></a>Configuração programática da tarefa Transferir Logons  
 Para obter mais informações sobre como definir essas propriedades programaticamente, clique no tópico a seguir:  
  
-   <xref:Microsoft.SqlServer.Dts.Tasks.TransferLoginsTask.TransferLoginsTask>  
  
## <a name="transfer-logins-task-editor-general-page"></a>Editor da Tarefa Transferir Logons (página Geral)
  Use a página **Geral** da caixa de diálogo do **Editor da Tarefa Transferir Logons** para nomear e descrever a tarefa Transferir Logons.  
  
### <a name="options"></a>Opções  
 **Nome**  
 Digite um nome exclusivo para a tarefa Transferir Logons. Esse nome é usado como rótulo no ícone de tarefa.  
  
> [!NOTE]  
>  Os nomes das tarefas devem ser exclusivos em um pacote.  
  
 **Descrição**  
 Digite uma descrição para a tarefa Transferir Logons.  
  
## <a name="transfer-logins-task-editor-logins-page"></a>Editor da Tarefa Transferir Logons (página Logons)
  Use a página **Logons** da caixa de diálogo **Editor da Tarefa de Transferir Logons** para especificar as propriedades para copiar um ou mais logons [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de uma instância de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para outra.  
  
> [!IMPORTANT]  
>  Quando a tarefa de Transferir Logons é executada, os logons são criados no servidor de destino com senhas aleatórias e as senhas são desabilitadas. Para usar esses logons, um membro da função de servidor fixa **sysadmin** deve alterar as senhas e habilitá-las. O logon do **sa** não pode ser transferido.  
  
### <a name="options"></a>Opções  
 **SourceConnection**  
 Selecione um gerenciador de conexões SMO na lista ou clique em **\<New connection...>** para criar uma conexão com o servidor de origem.  
  
 **DestinationConnection**  
 Selecione um gerenciador de conexões SMO na lista ou clique em **\<New connection...>** para criar uma conexão com o servidor de destino.  
  
 **LoginsToTransfer**  
 Selecione os logons [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para copiar da fonte para o servidor de destino. As opções desta propriedade estão listadas na seguinte tabela:  
  
|Valor|DESCRIÇÃO|  
|-----------|-----------------|  
|**AllLogins**|Todos os logons [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no servidor de origem serão copiados para o servidor de destino.|  
|**SelectedLogins**|Apenas os logons especificados com **LoginsList** serão copiados para o servidor de destino.|  
|**AllLoginsFromSelectedDatabases**|Todos os logons do banco de dados especificados com **DatabasesList** serão copiados para o servidor de destino.|  
  
 **LoginsList**  
 Selecione os logons no servidor de origem serão copiados para o servidor de destino. Esta opção somente está disponível quando **SelectedLogins** é selecionado para **LoginsToTransfer**.  
  
 **DatabasesList**  
 Selecione os logons no servidor de origem que serão copiados para o servidor de destino. Esta opção somente está disponível quando **AllLoginsFromSelectedDatabases** é selecionado para **LoginsToTransfer**.  
  
 **IfObjectExists**  
 Selecione como a tarefa deve tratar logons que tenham o mesmo nome já existente no servidor de destino.  
  
 As opções desta propriedade estão listadas na seguinte tabela:  
  
|Valor|DESCRIÇÃO|  
|-----------|-----------------|  
|**FailTask**|A tarefa irá falhar se já existirem logons com o mesmo nome no servidor de destino.|  
|**Overwrite**|A tarefa irá substituir logons de mesmo nome no servidor de destino.|  
|**Ignorar**|A tarefa irá ignorar os logons de mesmo nome que existem no servidor de destino.|  
  
 **CopySids**  
 Selecione se os identificadores de segurança associados aos logons devem ser copiados para o servidor de destino. Será necessário definir**CopySids** para **True** se a tarefa Transferir Logons for usada junto com a tarefa Transferir Banco de Dados. Caso contrário, os logons copiados não serão reconhecidos pelo banco de dados transferido.  
  
