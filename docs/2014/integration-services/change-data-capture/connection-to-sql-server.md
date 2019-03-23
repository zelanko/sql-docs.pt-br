---
title: Conexão ao SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 5bb582f9-68d3-4c1e-ab02-6fc16807f1a5
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 09d597cb7776362c44ca53e8d544f66608d8d37c
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/22/2019
ms.locfileid: "58377194"
---
# <a name="connection-to-sql-server"></a>Conexão com o SQL Server
  Quando um logon sem uma função de banco de dados que inclui permissão de gravação (por exemplo a função **db_owner**) ao banco de dados MSXDBCDC tenta criar uma instância Oracle CDC, a caixa de diálogo Conecte-se ao SQL Server é exibida.  
  
 Nesta caixa de diálogo, você deve inserir as credenciais para um logon que tem permissão de gravação ao banco de dados MSXDBCDC, como a função de banco de dados **db_owner** para criar a nova instância Oracle CDC.  
  
 Insira as seguintes informações na caixa de diálogo Conecte-se ao SQL Server.  
  
### <a name="server-name"></a>Nome do servidor  
 Digite o nome do servidor em que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está localizado.  
  
### <a name="authentication"></a>Autenticação  
 Selecione uma destas opções:  
  
-   Autenticação do Windows  
  
-   **Autenticação do SQL Server**: Se você selecionar essa opção, você deve digitar o **Login** e **senha** para o usuário no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] você está se conectando.  
  
### <a name="options"></a>Opções  
 Clique na seta para exibir opções disponíveis a serem configuradas. Você pode escolher deixar estas opções com o valor padrão. As opções disponíveis são:  
  
-   **Tempo limite de Conexão**: Digite o tempo (em segundos) o programa aguarda o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] conexão seja estabelecida antes de produzir um erro de tempo limite. O valor padrão é **15**.  
  
-   **Tempo limite de execução**: Digite o tempo (em segundos) que o programa aguarda a execução do comando SQL terminar antes produzir um erro de tempo limite. O valor padrão é **30**.  
  
-   **Criptografar Conexão**: Selecione **criptografar Conexão** para garantir que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] conexão que está sendo estabelecida está criptografada para garantir a privacidade.  
  
-   **Avançado**: Clique em **Avançado** e digite as propriedades de conexão adicionais na caixa de diálogo Propriedades Avançadas de Conexão, se necessário.  
  
## <a name="see-also"></a>Consulte também  
 [Permissões necessárias para conexão do SQL Server para o Serviço CDC](sql-server-connection-required-permissions-for-the-cdc-service.md)  
  
  
