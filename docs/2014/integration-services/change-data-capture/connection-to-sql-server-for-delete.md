---
title: Conexão ao SQL Server para exclusão | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 030b10c2-6b88-4c2c-bf67-22994be25a60
caps.latest.revision: 6
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: c2cf5dbb7d48050475dd839d0fd87fbce309a1f1
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36118929"
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
  
-   **Autenticação do SQL Server**: se você selecionar esta opção, deverá digitar o **Logon** e **Senha** para o usuário no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ao qual você está se conectando.  
  
 **Opções**  
 Clique na seta para exibir opções disponíveis a serem configuradas. Você pode escolher deixar estas opções com o valor padrão. As opções disponíveis são:  
  
-   **Tempo Limite de Conexão**: digite o tempo (em segundos) que o programa aguarda até que uma conexão com o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] seja estabelecida antes de gerar um erro de tempo limite. O valor padrão é **15**.  
  
-   **Tempo Limite de Execução**: digite o tempo (em segundos) que o programa aguarda até que uma execução de comando do SQL seja concluída antes de gerar um erro de tempo limite. O valor padrão é **30**.  
  
-   **Criptografar Conexão**: selecione **Criptografar Conexão** para verificar se a conexão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que está sendo estabelecida está criptografada para garantir a privacidade.  
  
-   **Avançado**: clique em **Avançado** e digite as propriedades de conexão adicionais na caixa de diálogo Propriedades Avançadas da Conexão, se necessário.  
  
## <a name="see-also"></a>Consulte também  
 [Permissões necessárias para conexão do SQL Server para o Serviço CDC](sql-server-connection-required-permissions-for-the-cdc-service.md)  
  
  