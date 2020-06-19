---
title: Permissões necessárias para conexão do SQL Server para o Serviço CDC | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: d9e968f9-180c-4fa0-a849-98f2b1942330
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 02dafca49993154f15845c79d475eef3081ccd63
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84922321"
---
# <a name="sql-server-connection-required-permissions-for-the-cdc-service"></a>Permissões necessárias para conexão do SQL Server para o Serviço CDC
  O Console de Configuração do Serviço CDC exige informações de conexão para que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] execute suas tarefas. Este tópico descreve as informações que podem ser fornecidas na caixa de diálogo Conecte-se ao SQL Server para definir a conexão para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 A caixa de diálogo Conecte-se ao SQL Server abre quando necessário, como quando as informações de conexão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não estão disponíveis ou quando as informações existem, mas a conexão não tem as permissões necessárias.  
  
 A tabela a seguir descreve as várias tarefas em que uma conexão para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é necessária e as permissões necessárias de logon/usuário do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
|Tarefa|Permissões mínimas|  
|----------|-------------------------|  
|Preparar a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .|`dbcreator` função de servidor fixa|  
|Crie um logon Oracle CDC Service-SQL Server para ser usado pelo serviço Oracle CDC.|`public` função de servidor fixa|  
|Crie um logon do Serviço Oracle CDC para usar para registrar o novo serviço no MSXDBCDC.|`db_datareader` e `db_datawriter` no MSXDBCDC|  
|Editar um logon do Serviço Oracle CDC para atualizar o registro do serviço no MSXDBCDC.|`db_datareader` e `db_datawriter` no MSXDBCDC|  
|Excluir um logon do Serviço Oracle CDC para atualizar o registro do serviço no MSXDBCDC.|`db_datareader` e `db_datawriter` no MSXDBCDC|  
  
## <a name="see-also"></a>Consulte Também  
 [Conexão com o SQL Server](connection-to-sql-server.md)   
 [Conexão com o SQL Server para exclusão](connection-to-sql-server-for-delete.md)  
  
  
