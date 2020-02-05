---
title: MSSQLSERVER_21879 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 21879 (Database Engine error)
ms.assetid: fcfab735-05ca-423a-89f1-fdee7e2ed8c0
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 7068229bcfcf63bb08fe46272cf308cee60be022
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/01/2020
ms.locfileid: "68056712"
---
# <a name="mssqlserver_21879"></a>MSSQLSERVER_21879
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do Produto|SQL Server|  
|ID do evento|21879|  
|Origem do Evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|SQLErrorNum21879|  
|Texto da mensagem|Não foi possível consultar o servidor redirecionado '% s' para o publicador original '% s' e o banco de dados publicador '% s' para determinar o nome do servidor remoto; Erro %d, Mensagem de erro '% s.'|  
  
## <a name="explanation"></a>Explicação  
**sp_validate_redirected_publisher** usa um servidor vinculado temporário criado para se conectar ao publicador redirecionado e descobrir o nome do servidor remoto. O erro 21879 é retornado quando a consulta de servidor vinculado falha. A chamada para solicitar o nome de servidor remoto é normalmente o primeiro uso do servidor vinculado temporário e, portanto, se houver problemas de conectividade, é provável que eles apareçam primeiro com essa chamada. Essa chamada remota apenas executa selecionar **@@servername** no servidor remoto.  
  
O servidor vinculado usado para consultar o publicador redirecionado usa o modo de segurança, o logon e a senha fornecidos quando **sp_adddistpublisher** foi chamado para o publicador original.  
  
-   Se a autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tiver sido usada (modo de segurança 0), o logon e a senha especificados serão usados para a conexão ao servidor remoto.  
  
-   Se a autenticação do Windows tiver sido usada (modo de segurança 1), uma conexão confiável será usada para conectar.  
  
    -   Se **sp_validate_redirected_publisher** for chamado explicitamente por um usuário, o logon do Windows usado pelo usuário será usado para a conexão.  
  
    -   Se o **sp_validate_redirected_** publisher for chamado por um agente de replicação em **sp_get_redirected_publisher**, o logon do Windows associado ao agente será usado.  
  
O erro 21879 pode indicar que **sp_validate_redirected_publisher** foi chamado usando um logon que não é conhecido no publicador de destino redirecionado.  
  
## <a name="user-action"></a>Ação do usuário  
Verifique se o logon de autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou o logon de autenticação do Windows é válido em todas as réplicas de grupo de disponibilidade e se tem autorização suficiente para acessar as tabelas de metadados de assinatura (syssubscriptions e sysmergesubscriptions) no banco de dados publicador.  
  
Existem considerações especiais quando o erro 21879 é retornado de uma chamada a **sp_get_redirected_publisher** iniciada por um agente de replicação executado em um nó diferente do distribuidor, como um agente de mesclagem executado em um assinante. Se a autenticação do Windows for usada para a conexão ao publicador redirecionado, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deverá ser configurado para a autenticação Kerberos, para que a conexão seja estabelecida com êxito. Quando a autenticação do Windows é usada e o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não é configurado para a autenticação Kerberos, o erro 18456 que indica que o logon 'NT AUTHORITY\ANONYMOUS LOGON' falhou é recebido por um agente de mesclagem executado em um assinante. Há três maneiras possíveis de lidar com este problema:  
  
-   Configure o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para autenticação Kerberos. Consulte **Autenticação Kerberos e SQL Server** nos Manuais Online do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   Use **sp_changedistpublisher** para alterar o modo de segurança associado ao publicador original em MSdistpublishers, bem como para especificar um logon e a senha a serem usados para a conexão.  
  
-   Especifique o parâmetro de linha de comando *BypassPublisherValidation* na linha de comando do agente de mesclagem para ignorar a validação quando **sp_get_redirected_publisher** for chamado no distribuidor.  
  
