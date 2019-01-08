---
title: Conexão ao SQL Server para exclusão | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 030b10c2-6b88-4c2c-bf67-22994be25a60
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 0b7c3b34f60f69a788c67022151dd90ddc9235e8
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52779948"
---
# <a name="connection-to-sql-server-for-delete"></a>Conexão para o SQL Server para exclusão
  Quando um logon sem uma função de banco de dados que inclui permissão de gravação (por exemplo a função **db_owner**) ao banco de dados MSXDBCDC tenta excluir uma instância Oracle CDC, a caixa de diálogo Conectar-se ao SQL Server é exibida.  
  
 Nesta caixa de diálogo, você deve inserir as credenciais de um logon que tem permissão de gravação ao banco de dados MSXDBCDC, como a função de banco de dados **db_owner** para excluir a instância Oracle CDC.  
  
 Insira as seguintes informações na caixa de diálogo Conecte-se ao SQL Server.  
  
 **Nome do servidor**  
 Digite o nome do servidor em que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está localizado.  
  
 **Autenticação**  
 Selecione uma destas opções:  
  
-   **Autenticação do Windows**  
  
-   **Autenticação do SQL Server**: Se você selecionar essa opção, você deve digitar o **Login** e **senha** para o usuário no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] você está se conectando.  
  
 **Opções**  
 Clique na seta para exibir opções disponíveis a serem configuradas. Você pode escolher deixar estas opções com o valor padrão. As opções disponíveis são:  
  
-   **Tempo limite de Conexão**: Digite o tempo (em segundos) o programa aguarda o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] conexão seja estabelecida antes de produzir um erro de tempo limite. O valor padrão é **15**.  
  
-   **Tempo limite de execução**: Digite o tempo (em segundos) que o programa aguarda a execução do comando SQL terminar antes produzir um erro de tempo limite. O valor padrão é **30**.  
  
-   **Criptografar Conexão**: Selecione **criptografar Conexão** para garantir que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] conexão que está sendo estabelecida está criptografada para garantir a privacidade.  
  
-   **Avançado**: Clique em **Avançado** e digite as propriedades de conexão adicionais na caixa de diálogo Propriedades Avançadas de Conexão, se necessário.  
  
## <a name="see-also"></a>Consulte também  
 [Permissões necessárias para conexão do SQL Server para o Serviço CDC](sql-server-connection-required-permissions-for-the-cdc-service.md)  
  
  
