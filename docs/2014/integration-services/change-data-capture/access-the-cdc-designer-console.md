---
title: Acessar o CDC Designer Console | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- accMsDes
ms.assetid: b168c64e-c1b5-42d4-a92a-84de1dd0324e
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 1a1a46e47dc7c40bf3747c4be55290a02bf6d9d8
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52770848"
---
# <a name="access-the-cdc-designer-console"></a>Acessar o CDC Designer Console
  Você pode acessar o CDC Designer Console do computador onde instalou o console. Para obter mais informações sobre a instalação, consulte Instalação.  
  
 Quando você abre o CDC Designer Console, a caixa de diálogo Conecte-se ao SQL Server é aberta.  
  
 O logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que acessa o CDC Designer deve ter permissões UPDATE no banco de dados MSXDBCDC. Além disso, o logon também tem que ter a função de servidor fixa `dbcreator` para criar novas Instâncias Oracle CDC. É recomendado que o logon também tenha acesso SELECT aos bancos de dados CDC que estão sendo usados ou o usuário não poderá exibir o estado desses bancos de dados.  
  
 Insira as seguintes informações na caixa de diálogo Conecte-se ao SQL Server.  
  
### <a name="server-name"></a>Nome do servidor  
 Digite o nome do servidor em que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está localizado.  
  
### <a name="authentication"></a>Autenticação  
 Selecione uma destas opções:  
  
-   **Autenticação do Windows**  
  
-   **Autenticação do SQL Server**: Se você selecionar essa opção, você deve digitar o **Login** e **senha** para o usuário no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] você está se conectando.  
  
 O logon deve ter uma função de banco de dados que permite acesso ao banco de dados MSXCDCDB. É recomendado que o logon também tenha acesso a qualquer banco de dados adicional que está sendo usado ou o usuário não poderá exibir os dados nesses bancos de dados.  
  
### <a name="options"></a>Opções  
 Clique na seta para exibir opções disponíveis a serem configuradas. Você pode escolher deixar estas opções com o valor padrão. As opções disponíveis são:  
  
 **Tempo-limite da conexão**  
 Digite o tempo (em segundos) que o Serviço CDC para Oracle espera por uma conexão com o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] antes de exceder o tempo limite. O valor padrão é **15**.  
  
 **Tempo Limite de Execução**  
 Digite o tempo (em segundos) que o Serviço do Windows do Oracle CDC espera que um comando seja executado antes de exceder o tempo limite. O valor padrão é **30**.  
  
 **Criptografar conexão**  
 Selecione **criptografar Conexão** para a comunicação entre o serviço Oracle CDC e o destino [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instância usando uma conexão criptografada. **Advanced**: Clique em **Avançado** e digite as propriedades de conexão adicionais na caixa de diálogo Propriedades Avançadas de Conexão, se necessário.  
  
 **Avançado**  
 Clique em **Avançado** e digite as propriedades de conexão adicionais na caixa de diálogo Propriedades Avançadas de Conexão, se necessário.  
  
 Para obter informações sobre a caixa de diálogo Propriedades Avançadas de Conexão, consulte [Propriedades Avançadas de Conexão](advanced-connection-properties.md).  
  
## <a name="see-also"></a>Consulte também  
 [Permissões necessárias para conexão do SQL Server para o Designer CDC](sql-server-connection-required-permissions-for-the-cdc-designer.md)  
  
  
