---
title: "Permissões necessárias para conexão do SQL Server para o CDC Designer | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: change-data-capture
ms.reviewer: 
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 80334de2-17c1-43c9-951e-21a9f864e9cb
caps.latest.revision: "9"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: c93992095ccc5c388b240273008f07d2237e44c9
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/20/2017
---
# <a name="sql-server-connection-required-permissions-for-the-cdc-designer"></a>Permissões necessárias para conexão do SQL Server para o Designer CDC
  O CDC Designer Console exige informações de conexão para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] executar suas tarefas. Este tópico descreve as informações que podem ser fornecidas na caixa de diálogo **Conecte-se ao SQL Server** para definir a conexão para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 A caixa de diálogo **Conecte-se ao SQL Server** abre quando necessário, como quando as informações de conexão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não estão disponíveis ou quando as informações existem, mas a conexão não tem as permissões necessárias.  
  
 A tabela a seguir descreve as várias tarefas em que uma conexão para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é necessária e as permissões necessárias de logon/usuário do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
|Tarefa|Permissões mínimas|  
|----------|-------------------------|  
|Exibir a lista de Serviços e Instâncias CDC usando a instância associada do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .|`db_datareader` em MSXDBCDC|  
|Iniciar/parar instâncias CDC|`db_datareader` e `db_datawriter` no MSXDBCDC|  
|Exibir o status da Instância CDC.|`db_owner` no banco de dados da Instância CDC|  
|Criar um novo banco de dados da Instância Oracle CDC.|`dbcreator` função de servidor fixa|  
|Criar uma nova instância Oracle CDC.|`db_datareader` em MSXDBCDC<br /><br /> `db_owner` no banco de dados CDC que foi criado.|  
|Obter scripts de implantação.|`db_datareader` e `db_datawriter` no MSXDBCDC<br /><br /> `db_owner` no banco de dados CDC relacionado|  
|Alterar configuração e adicionar/remover instâncias de captura.|`db_datareader` e `db_datawriter` no MSXDBCDC<br /><br /> `db_owner` no banco de dados CDC relacionado|  
  
## <a name="see-also"></a>Consulte também  
 [Acessar o CDC Designer Console](../../integration-services/change-data-capture/access-the-cdc-designer-console.md)   
 [Conexão do SQL Server para a criação de instância](../../integration-services/change-data-capture/sql-server-connection-for-instance-creation.md)  
  
  
