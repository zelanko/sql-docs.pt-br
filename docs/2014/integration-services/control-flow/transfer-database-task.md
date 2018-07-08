---
title: Tarefa Transferir Banco de Dados | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.transferdatabasetask.f1
helpviewer_keywords:
- Transfer Database task [Integration Services]
ms.assetid: b9a2e460-cdbc-458f-8df8-06b8b2de3d67
caps.latest.revision: 26
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 931978bdad7e2e82d232af85ee253ca8cae7de91
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37239256"
---
# <a name="transfer-database-task"></a>Tarefa Transferir Banco de Dados
  A tarefa Transferir Banco de Dados transfere um banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] entre duas instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Ao contrário das outras tarefas que transferem apenas objetos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] por meio de cópia, a tarefa Transferir Banco de Dados pode copiar ou mover um banco de dados. Essa tarefa também pode ser usada para copiar um banco de dados dentro do mesmo servidor.  
  
## <a name="offline-and-online-modes"></a>Modos offline e online  
 O banco de dados pode ser transferido usando o modo online ou offline. Quando você usa o modo online, o banco de dados permanece anexado e é transferido por meio do SQL Management Object (SMO) para copiar os objetos do banco de dados. Quando você usa o modo offline, o banco de dados é desanexado, os arquivos do banco de dados são copiados ou movidos e o banco de dados é anexado ao destino após a conclusão bem-sucedida da transferência. Se o banco de dados for copiado, ele será novamente anexado de forma automática à fonte, se a cópia for bem-sucedida. No modo offline, o banco de dados é copiado mais rapidamente, mas o banco de dados fica indisponível aos usuários durante a transferência.  
  
 O modo offline requer que você especifique os compartilhamentos de arquivos de rede nos servidores de origem e de destino que contêm os arquivos de banco de dados. Se a pasta for compartilhada e acessada pelo usuário, você poderá fazer referência ao compartilhamento de rede usando a sintaxe \\\nome_do_computador\Arquivos de Programas\minha_pasta\\. Caso contrário, você deverá usar a sintaxe \\\nome_do_computador\c$\Arquivos de Programas\minha_pasta\\. Para usar a última sintaxe, o usuário deve ter acesso à gravação para os compartilhamentos de rede de origem e destino.  
  
## <a name="transfer-of-databases-between-versions-of-sql-server"></a>Transferência de banco de dados entre versões do SQL Server  
 A tarefa Transferir Banco de Dados pode transferir um banco de dados entre instâncias de versões diferentes do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="events"></a>Eventos  
 A tarefa Transferir Banco de Dados não informa o progresso incremental da transferência de mensagem de erro; informa somente conclusão 0% e 100 %.  
  
## <a name="execution-value"></a>Valor de execução  
 O valor da execução, definido na propriedade `ExecutionValue` da tarefa, retorna o valor 1, porque em contraste com outras tarefas de transferência, a tarefa Transferir Banco de Dados pode transferir somente um banco de dados.  
  
 Ao atribuir uma variável definida pelo usuário para o `ExecValueVariable` propriedade da tarefa transferir banco de dados, as informações sobre a transferência de mensagem de erro pode se tornar disponível a outros objetos no pacote. Para obter mais informações, consulte [Variáveis do Integration Services &#40;SSIS&#41;](../integration-services-ssis-variables.md) e [Usar variáveis em pacotes](../use-variables-in-packages.md).  
  
## <a name="log-entries"></a>Entradas de log  
 A tarefa Transferir Banco de Dados inclui as seguintes entradas de log personalizadas:  
  
-   SourceSQLServer    Esta entrada de log lista o nome do servidor de origem.  
  
-   DestSQLServer    Esta entrada de log lista o nome do servidor de destino.  
  
-   SourceDB    Esta entrada de log lista o nome do banco de dados que é transferido.  
  
 Além disso, uma entrada de log para o `OnInformation` evento será gravado quando o banco de dados de destino é substituído.  
  
## <a name="security-and-permissions"></a>Segurança e permissões  
 Para transferir um banco de dados usando o  modo offline, o usuário que executa o pacote deve ser um membro da função servidor sysadmin.  
  
 Para transferir um banco de dados usando o modo online, o usuário que executa o pacote deve ser um membro da função servidor sysadmin ou proprietário do banco de dados (dbo) do banco de dados selecionado.  
  
## <a name="configuration-of-the-transfer-database-task"></a>Configuração da tarefa Transferir Banco de Dados  
 Você pode especificar se a tarefa tentará se anexar novamente ao banco de dados de origem, se a transferência do banco de dados falhar.  
  
 A tarefa Transferir Banco de Dados também pode ser configurada para permitir a sobregravação de um banco de dados de destino que tenha o mesmo nome, substituindo o banco de dados de destino.  
  
 O banco de dados de origem também pode ser renomeado como parte do processo de transferência. Se desejar transferir um banco de dados para uma instância de destino do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que já contenha um banco de dados com o mesmo nome, a renomeação do banco de dados de origem permitirá a transferência do banco de dados. Entretanto, os nomes dos arquivos do banco de dados também devem ser diferentes; se já existirem arquivos com os mesmos nomes no destino, a tarefa falhará.  
  
 Quando copiar um banco de dados, ele não poderá ser menor que o banco de dados **modelo** do servidor de destino. Você pode aumentar o tamanho do banco de dados para fazer a cópia ou reduzir o tamanho do **modelo**.  
  
 No tempo de execução, a tarefa Transferir Banco de Dados conecta-se aos servidores de origem e de destino usando um ou dois gerenciadores de conexões SMO. Quando você cria uma cópia de um banco de dados no mesmo servidor, somente um gerenciador de conexões SMO é exigido. Os gerenciadores de conexões SMO são configurados separadamente da tarefa Transferir Banco de Dados e, em seguida,  referenciadas na tarefa Transferir Banco de Dados. Os gerenciadores de conexões SMO especificam o servidor e o modo de autenticação a serem usados quando a tarefa acessar o servidor. Para obter mais informações, consulte [SMO Connection Manager](../connection-manager/smo-connection-manager.md).  
  
 Você pode definir propriedades pelo Designer do [!INCLUDE[ssIS](../../includes/ssis-md.md)] ou programaticamente.  
  
 Para obter mais informações sobre as propriedades que podem ser definidas no [!INCLUDE[ssIS](../../includes/ssis-md.md)] Designer, clique em um dos seguintes tópicos:  
  
-   [Editor da tarefa de banco de dados transferir &#40;página geral&#41;](../general-page-of-integration-services-designers-options.md)  
  
-   [Editor da tarefa de banco de dados transferir &#40;página de bancos de dados&#41;](../transfer-database-task-editor-databases-page.md)  
  
-   [Página Expressões](../expressions/expressions-page.md)  
  
 Para obter mais informações sobre como definir essas propriedades no [!INCLUDE[ssIS](../../includes/ssis-md.md)] Designer, clique no tópico a seguir:  
  
-   [Definir as propriedades de uma tarefa ou contêiner](../set-the-properties-of-a-task-or-container.md)  
  
## <a name="programmatic-configuration-of-the-transfer-database-task"></a>Configuração programática da tarefa Transferir Banco de Dados  
 Para obter mais informações sobre como definir essas propriedades programaticamente, clique no tópico a seguir:  
  
-   <xref:Microsoft.SqlServer.Dts.Tasks.TransferDatabaseTask.TransferDatabaseTask>  
  
  
