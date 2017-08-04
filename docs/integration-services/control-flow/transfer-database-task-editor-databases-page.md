---
title: "Transferência de Editor de tarefa de banco de dados (página bancos de dados) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.transferdatabasetask.database.f1
helpviewer_keywords:
- Transfer Database Task Editor
ms.assetid: ccdb74d0-4bea-420c-a726-2e0eb8957e0a
caps.latest.revision: 26
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: b104103ab5fdde0084cfcadcc82897d71d9a5c11
ms.contentlocale: pt-br
ms.lasthandoff: 08/03/2017

---
# <a name="transfer-database-task-editor-databases-page"></a>Editor da Tarefa Transferir Banco de Dados (página Bancos de Dados)
  Use a página **Bancos de Dados** da caixa de diálogo **Editor da Tarefa Transferir Banco de Dados** para especificar as propriedades para os bancos de dado de origem e de destino envolvidos na tarefa Transferir Banco de Dados. A tarefa Transferir Banco de Dados copia ou move um bancos de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] entre duas instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Essa tarefa também pode ser usada para copiar um banco de dados dentro do mesmo servidor. Para obter mais informações sobre essa tarefa, consulte [Tarefa Transferir Banco de Dados](../../integration-services/control-flow/transfer-database-task.md).  
  
## <a name="options"></a>Opções  
 **SourceConnection**  
 Selecione um Gerenciador de conexão do SMO na lista ou clique em  **\<nova conexão... >** para criar uma nova conexão para o servidor de origem.  
  
 **DestinationConnection**  
 Selecione um Gerenciador de conexão do SMO na lista ou clique em  **\<nova conexão... >** para criar uma nova conexão para o servidor de destino.  
  
 **DestinationDatabaseName**  
 Especifique o nome do banco de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no servidor de destino.  
  
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
  
|Value|Description|  
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
  
|Value|Description|  
|-----------|-----------------|  
|**Verdadeiro**|Anexa novamente o banco de dados de origem.|  
|**Falso**|Não anexa novamente o banco de dados de origem.|  
  
## <a name="see-also"></a>Consulte também  
 [Referência de mensagens e erros do Integration Services](../../integration-services/integration-services-error-and-message-reference.md)   
 [Tarefas do Integration Services](../../integration-services/control-flow/integration-services-tasks.md)   
 [Editor da tarefa transferir banco de dados &#40; Página geral &#41;](../../integration-services/control-flow/transfer-database-task-editor-general-page.md)   
 [Página expressões](../../integration-services/expressions/expressions-page.md)   
 [Gerenciador de Conexão do SMO](../../integration-services/connection-manager/smo-connection-manager.md)  
  
  
