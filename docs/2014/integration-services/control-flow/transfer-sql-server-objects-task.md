---
title: Tarefa Transferir Objetos SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.transfersqlserverobjectstask.f1
helpviewer_keywords:
- Transfer SQL Server Objects task [Integration Services]
ms.assetid: fe86d6e5-e415-406c-88f3-dc3ef71bd5f0
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 11e995020bd4e212304f6071e3e60195a962a7ca
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84917870"
---
# <a name="transfer-sql-server-objects-task"></a>Tarefa Transferir Objetos do SQL Server
  A tarefa Transferir Objetos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] transfere um ou mais tipos de objetos para um banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] entre instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Por exemplo, a tarefa pode copiar tabelas e procedimentos armazenados. Dependendo da versão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usado como fonte, tipos diferentes de objetos estarão disponíveis para cópia. Por exemplo, só um banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] inclui esquemas e agregações definidos pelo usuário.  
  
## <a name="objects-to-transfer"></a>Objetos a serem transferidos  
 Funções de servidor, funções e usuários do banco de dados especificado poderão ser copiados, bem como as permissões para os objetos transferidos. Copiando os usuários, as funções e as permissões associados juntamente com os objetos, os objetos transferidos ficarão imediatamente operáveis no servidor de destino.  
  
 A tabela a seguir lista os tipos de objetos que podem ser copiados.  
  
|Objeto|  
|------------|  
|Tabelas|  
|Exibições|  
|Procedimentos armazenados|  
|Funções definidas pelo usuário|  
|Padrões|  
|Tipos de dados definidos pelo usuário|  
|Funções de partição|  
|Esquemas de partição|  
|Esquemas|  
|Assemblies|  
|Agregações definidas pelo usuário|  
|Tipos definidos pelo usuário|  
|Coleção de esquema XML|  
  
 Os UDTs (Tipos Definidos pelo Usuário) criados em uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] têm dependências em assemblies CLR (Common Language Runtime). Se você usar a tarefa Transferir Objetos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para transferir UDTs, terá de configurar a tarefa para transferir objetos dependentes. Para transferir objetos dependentes, defina a propriedade `IncludeDependentObjects` como `True`.  
  
### <a name="table-options"></a>Opções de tabela  
 Ao copiar tabelas, você poderá indicar os tipos de itens relacionados a tabelas a serem incluídos no processo de cópia. Os seguintes tipos de itens poderão ser copiados com a tabela relacionada:  
  
-   Índices  
  
-   Gatilhos  
  
-   Índices de texto completo  
  
-   Chaves primárias  
  
-   Chaves estrangeiras  
  
 Você também poderá indicar que o script gerado pela tarefa tenha o formato Unicode.  
  
## <a name="destination-options"></a>Opções de destino  
 Você pode configurar a tarefa Transferir Objetos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para incluir nomes de esquema, dados, propriedades estendidas de objetos transferidos e objetos dependentes na transferência. Se forem copiados dados, ela poderá substituir ou anexar dados existentes.  
  
 Algumas opções só se aplicam ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Por exemplo, somente o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dá suporte a esquemas.  
  
## <a name="security-options"></a>Opções de segurança  
 A tarefa Transferir Objetos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pode incluir usuários em nível de banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e funções da fonte, logons [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e permissões para objetos transferidos. Por exemplo, a transferência pode incluir as permissões nas tabelas transferidas.  
  
## <a name="transfer-objects-between-instances-of-sql-server"></a>Transferir objetos entre instâncias do SQL Server  
 A tarefa Transferir Objetos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dá suporte a uma origem e a um destino do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="events"></a>Eventos  
 A tarefa ativa um evento de informações que informa o objeto transferido e um evento de aviso quando um objeto é substituído. Um evento de informações também é ativado para ações como o truncamento de tabelas de banco de dados.  
  
 A tarefa Transferir Objetos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não informa progresso incremental da transferência do objeto; informa somente conclusão 0% e 100 % .  
  
## <a name="execution-value"></a>Valor de execução  
 O valor de execução armazenado na propriedade da tarefa `ExecutionValue` retorna o número de objetos transferidos. Ao atribuir uma variável definida pelo usuário à propriedade `ExecValueVariable` da tarefa Transferir Objetos do Servidor SQL, as informações sobre a transferência do objeto podem ser disponibilizadas para outros objetos do pacote. Para obter mais informações, consulte [Variáveis do Integration Services &#40;SSIS&#41;](../integration-services-ssis-variables.md) e [Usar variáveis em pacotes](../use-variables-in-packages.md).  
  
## <a name="log-entries"></a>Entradas de log  
 A tarefa Transferir Objetos do SQL inclui as seguintes entradas de log personalizadas:  
  
-   TransferSqlServerObjectsTaskStartTransferringObjects   Essa entrada de log informa que a transferência foi iniciada. A entrada do log contém a hora de início.  
  
-   TransferSqlServerObjectsTaskFinishedTransferringObjects    Essa entrada de log informa que a transferência foi concluída. A entrada do log contém a hora de término.  
  
 Além disso, uma entrada de log para um evento `OnInformation` informa o número de objetos dos tipos de objeto selecionados para transferência, o número de objetos transferidos e ações como truncamento de tabelas quando são transferidos dados com tabelas. Uma entrada de log para o evento `OnWarning` é gravada para cada objeto de destino que é substituído  
  
## <a name="security-and-permissions"></a>Segurança e permissões  
 O usuário deve ter permissão para procurar objetos no servidor de origem e deve ter permissão para cancelar e criar objetos no servidor de destino; além disso, o usuário deve ter acesso ao banco de dados especificado e aos objetos do banco de dados.  
  
## <a name="configuration-of-the-transfer-sql-server-objects-task"></a>Configuração da tarefa Transferir Objetos do SQL Server  
 A tarefa Transferir Objetos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pode ser configurada para transferir todos os objetos, todos os objetos de um tipo ou somente objetos especificados de um tipo. Por exemplo, você pode escolher copiar somente tabelas selecionadas no banco de dados AdventureWorks.  
  
 Se a tarefa Transferir Objetos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] transferir tabelas, você poderá especificar os tipos de objetos relacionados à tabela a serem copiados com as tabelas. Por exemplo, você poderá especificar que as chaves primárias sejam copiadas com as tabelas.  
  
 Para aprimorar a funcionalidade dos objetos transferidos, você pode configurar a tarefa Transferir Objetos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para incluir nomes de esquema, dados, propriedades estendidas de objetos transferidos e objetos dependentes na transferência. Ao copiar os dados, você poderá especificar se os dados existentes deverão ser substituídos ou anexados.  
  
 No tempo de execução, a tarefa Transferir Objetos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] faz a conexão com os servidores de origem e destino usando dois gerenciadores de conexões SMO. Os gerenciadores de conexões SMO são configurados separadamente da tarefa Transferir Objetos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e referenciadas na tarefa Transferir Objetos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Os gerenciadores de conexões SMO especificam o servidor e o modo de autenticação a serem usados ao acessar o servidor. Para obter mais informações, consulte [SMO Connection Manager](../connection-manager/smo-connection-manager.md).  
  
 Você pode definir propriedades pelo Designer do [!INCLUDE[ssIS](../../includes/ssis-md.md)] ou programaticamente.  
  
 Para obter mais informações sobre as propriedades que podem ser definidas no [!INCLUDE[ssIS](../../includes/ssis-md.md)] Designer, clique em um dos seguintes tópicos:  
  
-   [Editor da Tarefa Transferir Objetos SQL Server &#40;Página Geral&#41;](../general-page-of-integration-services-designers-options.md)  
  
-   [Editor da Tarefa Transferir Objetos do SQL Server &#40;Página Objetos&#41;](../transfer-sql-server-objects-task-editor-objects-page.md)  
  
-   [Página Expressões](../expressions/expressions-page.md)  
  
 Para obter mais informações sobre como definir essas propriedades no [!INCLUDE[ssIS](../../includes/ssis-md.md)] Designer, clique no tópico a seguir:  
  
-   [Definir as propriedades de uma tarefa ou de um contêiner](../set-the-properties-of-a-task-or-container.md)  
  
## <a name="programmatic-configuration-of-the-transfer-sql-server-objects-task"></a>Configuração programática da tarefa Transferir Objetos do SQL Server  
 Para obter mais informações sobre como definir essas propriedades programaticamente, clique no tópico a seguir:  
  
-   <xref:Microsoft.SqlServer.Dts.Tasks.TransferSqlServerObjectsTask.TransferSqlServerObjectsTask>  
  
  
