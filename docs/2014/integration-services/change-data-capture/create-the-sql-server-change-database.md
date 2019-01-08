---
title: Criar o banco de dados de alteração do SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- oraIns
ms.assetid: 4f79c24a-e99a-4a06-8637-51eeec406259
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 7e95a47f2a2fc7444822c19b67bf2d95626fa62c
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52770968"
---
# <a name="create-the-sql-server-change-database"></a>Criar o banco de dados de alteração do SQL Server
  Quando você inicia o assistente Nova Instância, a página Criar Banco de Dados CDC é aberta. Use a página Criar Banco de Dados CDC para fornecer informações sobre a nova instância CDC e criar um novo banco de dados de alteração.  
  
 Quando você cria um novo banco de dados CDC, ele está habilitado para SQL Server CDC e esta habilitação exige um logon que é um membro da função de servidor fixa `sysadmin` .  
  
 Quando um usuário que inicia o assistente Criar uma Instância Oracle CDC não é membro da função de servidor fixa `sysadmin` , a caixa de diálogo Conecte-se ao SQL Server abre e pede as credenciais para um membro da função sysadmin para realizar a tarefa de habilitar o banco de dados para SQL Server CDC. Quando o banco de dados CDC é criado, o logon `sysadmin` é descartado e o trabalho é retomado com o logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] original usado quando o Oracle Designer Console foi inserido.  
  
> [!IMPORTANT]  
>  Para tarefas diferentes de Habilitar o banco de dados para SQL Server CDC de, o logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usado para executar o Assistente de Nova Instância deverá ter a função de servidor fixa `dbcreator` e permissões UPDATE no banco de dados MSXDBCDC.  
  
 Para obter informações sobre como inserir os dados na caixa de diálogo Conecte-se ao SQL Server, consulte [SQL Server Connection for Instance Creation](sql-server-connection-for-instance-creation.md).  
  
## <a name="options"></a>Opções  
 **Instância Oracle CDC**  
 Digite as seguintes informações sobre a instância CDC que você está criando.  
  
-   **Nome**: Digite um nome para o novo serviço. Este também será o nome do novo banco de dados de alteração.  
  
-   **Descrição**: Digite uma descrição para a nova instância ajudar a identificá-lo. Isso é opcional.  
  
 **Banco de Dados de alteração do SQL Server**  
 Esta seção é usada para criar o banco de dados.  
  
1.  **Alterar banco de dados**: O nome do novo banco de dados de alteração. O nome do banco de dados é o mesmo que o nome que você deu à instância. Este campo somente leitura exibe o caminho completo para o banco de dados.  
  
2.  **Criar banco de dados**: Clique em **Create Database** para criar o banco de dados.  
  
     Para criar o banco de dados, o logon deve ter a função de servidor `sysasmin` . Consulte a observação de segurança acima para obter mais informações.  
  
     Depois que você criar o banco de dados, clique em **Avançar** para [Connect to an Oracle Source Database](connect-to-an-oracle-source-database.md).  
  
## <a name="see-also"></a>Consulte também  
 [Como criar a instância de banco de dados de alteração do SQL Server](how-to-create-the-sql-server-change-database-instance.md)   
 [O Serviço Oracle CDC](the-oracle-cdc-service.md)  
  
  
