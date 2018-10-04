---
title: Transferir o Editor da tarefa de banco de dados (página bancos de dados) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.transferdatabasetask.database.f1
helpviewer_keywords:
- Transfer Database Task Editor
ms.assetid: ccdb74d0-4bea-420c-a726-2e0eb8957e0a
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 69a3c17a5b247c3c1ccefa5887404ad0865c673e
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48070628"
---
# <a name="transfer-database-task-editor-databases-page"></a>Editor da Tarefa Transferir Banco de Dados (página Bancos de Dados)
  Use a página **Bancos de Dados** da caixa de diálogo **Editor da Tarefa Transferir Banco de Dados** para especificar as propriedades para os bancos de dado de origem e de destino envolvidos na tarefa Transferir Banco de Dados. A tarefa Transferir Banco de Dados copia ou move um bancos de dados [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] entre duas instâncias do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Essa tarefa também pode ser usada para copiar um banco de dados dentro do mesmo servidor. Para obter mais informações sobre essa tarefa, consulte [Tarefa Transferir Banco de Dados](control-flow/transfer-database-task.md).  
  
## <a name="options"></a>Opções  
 **SourceConnection**  
 Selecione um gerenciador de conexões SMO na lista ou clique em **\<Nova conexão...>** para criar uma nova conexão com o servidor de origem.  
  
 **DestinationConnection**  
 Selecione um gerenciador de conexões SMO na lista ou clique em **\<Nova conexão...>** para criar uma nova conexão com o servidor de destino.  
  
 **DestinationDatabaseName**  
 Especifique o nome do banco de dados [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] no servidor de destino.  
  
 Para popular este campo automaticamente com o nome do banco de dados de origem, especifique o **SourceConnection** e **SourceDatabaseName** primeiro.  
  
 Para renomear o banco de dados no servidor de destino, digite o novo nome neste campo.  
  
 **DestinationDatabaseFiles**  
 Especifica os nomes e locais dos arquivos de banco de dados no servidor de destino.  
  
 Para popular este campo automaticamente com os nomes e locais de arquivo de banco de dados, especifique o **SourceConnection**, **SourceDatabaseName**e **SourceDatabaseFiles** primeiro.  
  
 Para renomear os arquivos de banco de dados ou especificar os novos locais no servidor de destino, popule esse campo com as informações de banco de dados de origem e clique no botão Procurar. Na caixa de diálogo **Arquivos de banco de dados de destino** , edite o **Arquivo de Destino**, a **Pasta de Destino**ou o **Compartilhamento de Arquivos na Rede**.  
  
> [!NOTE]  
>  Se você localizar os arquivos de banco de dados usando o botão Procurar, o local de arquivo será inserido usando a notação da unidade local: por exemplo, c:\\. É possível substituir isso pela a notação de compartilhamento na rede, inclusive o nome do computador e o nome de compartilhamento. Se o compartilhamento administrativo padrão for usado, será necessário usar a notação de $ e ter acesso administrativo ao compartilhamento.  
  
 **DestinationOverwrite**  
 Especifique se o é possível substituir o banco de dados no servidor de destino.  
  
 As opções desta propriedade estão listadas na seguinte tabela:  
  
|Valor|Description|  
|-----------|-----------------|  
|**Verdadeiro**|Substitui o banco de dados no servidor de destino.|  
|**Falso**|Não substitui o banco de dados no servidor de destino.|  
  
> [!CAUTION]  
>  Os dados no banco de dados do servidor de destino serão substituídos se você especificar **True** para **DestinationOverwrite**, o que pode resultar na perda de dados. Para evitar isso, faça backup do banco de dados do servidor de destino em outro local antes de executar a tarefa Transferir Banco de Dados.  
  
 **Ação**  
 Especifique se a tarefa vai **Copiar** ou **Mover** o banco de dados para o servidor de destino.  
  
 **Método**  
 Especifique se a tarefa será executada enquanto o banco de dados no servidor de origem estiver no modo online ou offline.  
  
 Para transferir um banco de dados usando o modo offline, é necessário que o usuário que executa o pacote seja um membro da função de servidor fixa **sysadmin** .  
  
 Para transferir um banco de dados usando o modo online, é necessário que o usuário que executa o pacote seja um membro da função de servidor fixa **sysadmin** ou o proprietário do banco de dados (**dbo**) do banco de dados selecionado.  
  
 **SourceDatabaseName**  
 Selecione o nome do banco de dados a ser copiado ou movido.  
  
 **SourceDatabaseFiles**  
 Clique no botão Procurar para selecionar os arquivos de banco de dados.  
  
 **ReattachSourceDatabase**  
 Especifique se a tarefa tentará anexar novamente o banco de dados de origem se ocorrer uma falha.  
  
 As opções desta propriedade estão listadas na seguinte tabela:  
  
|Valor|Description|  
|-----------|-----------------|  
|**Verdadeiro**|Anexa novamente o banco de dados de origem.|  
|**Falso**|Não anexa novamente o banco de dados de origem.|  
  
## <a name="see-also"></a>Consulte também  
 [Referência de mensagens e erros do Integration Services](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Tarefas do Integration Services](control-flow/integration-services-tasks.md)   
 [Editor da tarefa de banco de dados transferir &#40;página geral&#41;](general-page-of-integration-services-designers-options.md)   
 [Página expressões](expressions/expressions-page.md)   
 [Gerenciador de Conexões SMO](connection-manager/smo-connection-manager.md)  
  
  
