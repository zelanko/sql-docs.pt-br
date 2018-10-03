---
title: Conexão do SQL Server para a criação de instância | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 81d0e7e2-d8f0-4bd9-9565-218ce996f28e
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 2e0f879d566608f38a99d9fb4a316b0284213403
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47816825"
---
# <a name="sql-server-connection-for-instance-creation"></a>Conexão de SQL Server para a criação de instância
  Uma das primeiras etapas ao criar uma Instância Oracle CDC é a criação de um banco de dados CDC na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de destino. Este banco de dados CDC está habilitado para SQL Server CDC e esta habilitação exige um logon que é um membro da função de servidor fixa `sysadmin` .  
  
 Quando um usuário que inicia o assistente **Criar uma Instância Oracle CDC** não é membro da função de servidor fixa `sysadmin` , a caixa de diálogo **Conecte-se ao SQL Server** abre e pede as credenciais para um membro da função `sysadmin` para realizar a tarefa de habilitar o banco de dados para SQL Server CDC. Quando o banco de dados CDC é criado, o logon `sysadmin` é descartado e o trabalho é retomado com o logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] original usado quando o Oracle Designer Console foi inserido.  
  
## <a name="task-list"></a>Lista de Tarefas  
 Insira as seguintes informações na caixa de diálogo **Conecte-se ao SQL Server** .  
  
 **Nome do servidor**  
 Digite o nome do servidor em que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está localizado.  
  
 **Autenticação**  
 Selecione uma destas opções:  
  
-   **Autenticação do Windows**  
  
-   **Autenticação do SQL Server**: se você selecionar esta opção, deverá digitar o **Logon** e **Senha** para o usuário no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ao qual você está se conectando.  
  
 O logon deve ter uma função de banco de dados que permite acesso ao banco de dados MSXCDCDB. É recomendado que o logon também tenha acesso a qualquer banco de dados adicional que está sendo usado ou o usuário não poderá exibir os dados nesses bancos de dados.  
  
 **Opções**  
 Clique na seta para exibir opções disponíveis a serem configuradas. Você pode escolher deixar estas opções com o valor padrão. As opções disponíveis são:  
  
-   **Tempo limite de conexão**: digite o tempo (em segundos) que o Serviço CDC para Oracle aguarda uma conexão com o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] antes de exceder o tempo limite. O valor padrão é **15**.  
  
-   **Tempo limite de execução**: digite o tempo (em segundos) que o Serviço Windows do Oracle CDC aguarda até que um comando seja executado antes de exceder o tempo limite. O valor padrão é **30**.  
  
-   **Criptografar Conexão**: selecione **Criptografar Conexão** para a comunicação entre o Serviço Oracle CDC e a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de destino usando uma conexão criptografada.  
  
-   **Avançado**: clique em **Avançado** e digite as propriedades de conexão adicionais na caixa de diálogo Propriedades Avançadas da Conexão, se necessário.  
  
     Para obter informações sobre a caixa de diálogo Propriedades Avançadas de Conexão, consulte [Propriedades Avançadas de Conexão](../../integration-services/change-data-capture/advanced-connection-properties.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Criar o banco de dados de alteração do SQL Server](../../integration-services/change-data-capture/create-the-sql-server-change-database.md)   
 [Permissões necessárias para conexão do SQL Server para o CDC Designer](../../integration-services/change-data-capture/sql-server-connection-required-permissions-for-the-cdc-designer.md)  
  
  
