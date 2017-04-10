---
title: "Permiss&#245;es necess&#225;rias para conex&#227;o do SQL Server para o Servi&#231;o CDC | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: d9e968f9-180c-4fa0-a849-98f2b1942330
caps.latest.revision: 8
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 8
---
# Permiss&#245;es necess&#225;rias para conex&#227;o do SQL Server para o Servi&#231;o CDC
  O Console de Configuração do Serviço CDC exige informações de conexão para que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] execute suas tarefas. Este tópico descreve as informações que podem ser fornecidas na caixa de diálogo Conecte-se ao SQL Server para definir a conexão para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 A caixa de diálogo Conecte-se ao SQL Server abre quando necessário, como quando as informações de conexão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não estão disponíveis ou quando as informações existem, mas a conexão não tem as permissões necessárias.  
  
 A tabela a seguir descreve as várias tarefas em que uma conexão para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é necessária e as permissões necessárias de logon/usuário do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
|Tarefa|Permissões mínimas|  
|----------|-------------------------|  
|Preparar a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .|`dbcreator` função de servidor fixa|  
|Crie um logon Oracle CDC Service-SQL Server para ser usado pelo serviço Oracle CDC.|`public` função de servidor fixa|  
|Crie um logon do Serviço Oracle CDC para usar para registrar o novo serviço no MSXDBCDC.|`db_datareader` e `db_datawriter` no MSXDBCDC|  
|Editar um logon do Serviço Oracle CDC para atualizar o registro do serviço no MSXDBCDC.|`db_datareader` e `db_datawriter` no MSXDBCDC|  
|Excluir um logon do Serviço Oracle CDC para atualizar o registro do serviço no MSXDBCDC.|`db_datareader` e `db_datawriter` no MSXDBCDC|  
  
## Consulte também  
 [Conexão com o SQL Server](../../integration-services/change-data-capture/connection-to-sql-server.md)   
 [Conexão para o SQL Server para exclusão](../../integration-services/change-data-capture/connection-to-sql-server-for-delete.md)  
  
  