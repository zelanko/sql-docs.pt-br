---
description: Configurar segurança de caixa de diálogo para notificações de evento
title: Configurar segurança de caixa de diálogo para notificações de evento | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- event notifications [SQL Server], security
ms.assetid: 12afbc84-2d2a-4452-935e-e1c70e8c53c1
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 85fbbe596954083015a0533995784f31609d1b90
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/25/2020
ms.locfileid: "96130201"
---
# <a name="configure-dialog-security-for-event-notifications"></a>Configurar segurança de caixa de diálogo para notificações de evento
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  [!INCLUDE[ssSB](../../includes/sssb-md.md)] deve ser configurada para notificações de eventos que enviam mensagens a um agente de serviços em um servidor remoto. A segurança de diálogo deve ser configurada manualmente, de acordo com o modelo de segurança total de diálogo do [!INCLUDE[ssSB](../../includes/sssb-md.md)] . O modelo de segurança total habilita criptografia e decodificação de mensagens enviadas para e de servidores remotos. Embora as notificações de eventos sejam enviadas em uma única direção, outras mensagens, como erros, também são retornadas para a direção oposta.  
  
## <a name="configuring-dialog-security-for-event-notifications"></a>Configurando segurança de diálogo para notificações de eventos  
 O processo necessário para implementar segurança de diálogo para notificação de eventos é descrito nas etapas a seguir. Elas compreendem ações a serem efetuadas tanto no servidor de origem, quanto no servidor de destino. O servidor de origem é o servidor no qual a notificação de eventos está sendo criada. O servidor de destino é o servidor que recebe a mensagem de notificação de eventos. É necessário completar as ações de cada etapa em ambos os servidores, de origem e de destino, para poder passar à etapa seguinte.  
  
> [!IMPORTANT]  
>  Todos os certificados devem ser criados com datas válidas de início e de validade.  
  
 **Etapa 1: Estabeleça um número da porta de TCP e o nome do serviço de destino.**  
  
 Estabeleça a porta de TCP pela qual o servidor de origem e o servidor de destino receberão mensagens. Você também deve determinar o nome do serviço de destino.  
  
 **Etapa 2: Configure criptografia e compartilhamento de certificados para autenticação em nível de banco de dados.**  
  
 Efetue as ações abaixo nos servidores de origem e de destino.  
  
|Servidor de origem|Servidor de destino|  
|-------------------|-------------------|  
|Escolha ou crie um banco de dados para guardar a notificação de eventos e a chave mestra.|Escolha ou crie um banco de dados para guardar a chave mestra.|  
|Se não existir uma chave mestra para o banco de dados de origem, [crie uma chave mestra](../../t-sql/statements/create-master-key-transact-sql.md). É necessária uma chave mestra em ambos os bancos de dados (origem e destino), para ajudar a proteger seus respectivos certificados.|Se não existir uma chave mestra para o banco de dados de destino, crie uma chave mestra.|  
|[Crie um logon](../../t-sql/statements/create-login-transact-sql.md) e um [usuário](../../t-sql/statements/create-user-transact-sql.md) correspondente para o banco de dados de origem.|Crie um logon e um usuário correspondente para o banco de dados de destino.|  
|[Crie um certificado](../../t-sql/statements/create-certificate-transact-sql.md) de propriedade do usuário do banco de dados de origem.|Crie um certificado de propriedade do usuário do banco de dados de destino.|  
|[Faça um backup do certificado](../../t-sql/statements/backup-certificate-transact-sql.md) em um arquivo que possa ser acessado pelo servidor de destino.|Faça um backup do certificado em um arquivo que possa ser acessado pelo servidor de origem.|  
|[Crie um usuário](../../t-sql/statements/create-user-transact-sql.md), especificando o usuário do banco de dados de destino e WITHOUT LOGIN. Este usuário será proprietário do certificado de banco de dados de destino a ser criado a partir do arquivo de backup. O usuário não precisa ser mapeado para um logon, pois seu único propósito é possuir o certificado de banco de dados de destino criado na etapa 3 abaixo.|Crie um usuário, especificando o usuário do banco de dados de origem e WITHOUT LOGIN. Este usuário será proprietário do certificado de banco de dados de origem a ser criado a partir do arquivo de backup. O usuário não precisa ser mapeado para um logon, pois seu único propósito é possuir o certificado de banco de dados de origem criado na etapa 3 abaixo.|  
  
 **Etapa 3: Compartilhe os certificados e conceda permissões para autenticação em nível de banco de dados.**  
  
 Efetue as ações abaixo nos servidores de origem e de destino.  
  
|Servidor de origem|Servidor de destino|  
|-------------------|-------------------|  
|[Crie um certificado](../../t-sql/statements/create-certificate-transact-sql.md) a partir do arquivo de backup do certificado de destino, especificando o usuário do banco de dados de destino como o proprietário.|Crie um certificado a partir do arquivo de backup do certificado de origem, especificando o usuário do banco de dados de origem como o proprietário.|  
|[Conceda permissão](../../t-sql/statements/grant-transact-sql.md) para criar a notificação de eventos para o usuário do banco de dados de origem. Para obter mais informações sobre essa permissão, consulte [CREATE EVENT NOTIFICATION &#40;Transact-SQL&#41;](../../t-sql/statements/create-event-notification-transact-sql.md).|Conceda a permissão REFERENCES ao usuário do banco de dados de destino no contrato de notificações de eventos existentes do [!INCLUDE[ssSB](../../includes/sssb-md.md)] : `https://schemas.microsoft.com/SQL/Notifications/PostEventNotification`.|  
|[Crie uma associação de serviço remoto](../../t-sql/statements/create-remote-service-binding-transact-sql.md) ao serviço de destino e especifique as credenciais do usuário do banco de dados de destino. A associação do serviço remoto garante que a chave pública no certificado de propriedade do usuário do banco de dados de origem autentique as mensagens enviadas ao servidor de destino.|[Conceda](../../t-sql/statements/grant-transact-sql.md) permissões CREATE QUEUE, CREATE SERVICE e CREATE SCHEMA ao usuário do banco de dados de destino.|  
||Caso ainda não esteja conectado ao banco de dados como usuário do banco de dados de destino, faça-o agora.|  
||[Crie uma fila](../../t-sql/statements/create-queue-transact-sql.md) para receber as mensagens de notificação de eventos e [crie um serviço](../../t-sql/statements/create-service-transact-sql.md) para entregar as mensagens.|  
||[Conceda permissão SEND](../../t-sql/statements/grant-transact-sql.md) no serviço de destino ao usuário do banco de dados de origem.|  
|Forneça o identificador do agente de serviços do banco de dados de origem para o servidor de destino. Esse identificador pode ser obtido consultando-se a coluna **service_broker_guid** da exibição de catálogo [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) . Para uma notificação de eventos de nível de servidor, use o identificador do service broker do **msdb**.|Forneça o identificador do agente de serviços do banco de dados de destino para o servidor de origem.|  
  
 **Etapa 4: Crie rotas e configure autenticação em nível de servidor.**  
  
 Efetue as ações abaixo nos servidores de origem e de destino.  
  
|Servidor de origem|Servidor de destino|  
|-------------------|-------------------|  
|[Crie uma rota](../../t-sql/statements/create-route-transact-sql.md) para o serviço de destino e especifique o identificador do service broker do banco de dados de destino e o número da porta de TCP estabelecido.|Crie uma rota para o serviço de origem e especifique o identificador do agente de serviços do banco de dados de origem e o número de porta de TCP estabelecido. Para especificar o serviço de origem, use o seguinte serviço fornecido: `https://schemas.microsoft.com/SQL/Notifications/EventNotificationService`.|  
|Mude para o banco de dados **mestre** para configurar a autenticação no nível de servidor.|Mude para o banco de dados **mestre** para configurar a autenticação no nível de servidor.|  
|Se não existir uma chave mestra para o banco de dados de **mestre** , [crie uma chave mestra](../../t-sql/statements/create-master-key-transact-sql.md).|Se não existir uma chave mestra para o banco de dados de **mestre** , crie uma chave mestra.|  
|[Crie um certificado](../../t-sql/statements/create-certificate-transact-sql.md) que autentique o banco de dados.|Crie um certificado que autentique o banco de dados.|  
|[Faça um backup do certificado](../../t-sql/statements/backup-certificate-transact-sql.md) em um arquivo que possa ser acessado pelo servidor de destino.|Faça um backup do certificado em um arquivo que possa ser acessado pelo servidor de origem.|  
|[Crie um ponto de extremidade](../../t-sql/statements/create-endpoint-transact-sql.md)e especifique o número da porta de TCP estabelecido, FOR SERVICE_BROKER (AUTHENTICATION = CERTIFICATE *certificate_name*) e o nome do certificado de autenticação.|Crie um ponto de extremidade e especifique o número da porta de TCP estabelecido, FOR SERVICE_BROKER (AUTHENTICATION = CERTIFICATE *certificate_name*) e o nome do certificado de autenticação.|  
|[Crie um logon](../../t-sql/statements/create-login-transact-sql.md)e especifique o logon do servidor de destino.|Crie um logon e especifique o logon do servidor de origem.|  
|[Conceda permissão CONNECT](../../t-sql/statements/grant-transact-sql.md) no ponto de extremidade para o logon do autenticador de destino.|Conceda permissão CONNECT no ponto de extremidade para o logon do autenticador de origem.|  
|[Crie um usuário](../../t-sql/statements/create-user-transact-sql.md)e especifique o logon do autenticador de destino.|Crie um usuário e especifique o logon do autenticador de origem.|  
  
 **Etapa 5: Compartilhe certificados para autenticação em nível de servidor e crie a notificação de eventos.**  
  
 Efetue as ações abaixo nos servidores de origem e de destino.  
  
|Servidor de origem|Servidor de destino|  
|-------------------|-------------------|  
|[Crie um certificado](../../t-sql/statements/create-certificate-transact-sql.md) a partir do arquivo de backup do certificado de destino, especificando o autenticador de destino como o proprietário.|Crie um certificado a partir do arquivo de backup do certificado de origem, especificando o autenticador de origem como o proprietário.|  
|Alterne para o banco de dados de origem no qual criar a notificação de eventos e, caso ainda não esteja conectado como usuário do banco de dados de origem, faça-o agora.|Alterne para o banco de dados de destino a receber as mensagens de notificação de eventos.|  
|[Crie a notificação de eventos](../../t-sql/statements/create-event-notification-transact-sql.md)e especifique o agente de serviços e o identificador do banco de dados de destino.||  
  
## <a name="see-also"></a>Consulte Também  
 [GRANT &#40;Transact-SQL&#41;](../../t-sql/statements/grant-transact-sql.md)   
 [BACKUP CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/backup-certificate-transact-sql.md)   
 [sys.databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)   
 [Hierarquia de criptografia](../../relational-databases/security/encryption/encryption-hierarchy.md)   
 [Implementar notificações de evento](../../relational-databases/service-broker/implement-event-notifications.md)   
 [CREATE MASTER KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-master-key-transact-sql.md)   
 [CREATE LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/create-login-transact-sql.md)   
 [CREATE USER &#40;Transact-SQL&#41;](../../t-sql/statements/create-user-transact-sql.md)   
 [CREATE CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/create-certificate-transact-sql.md)   
 [CREATE REMOTE SERVICE BINDING &#40;Transact-SQL&#41;](../../t-sql/statements/create-remote-service-binding-transact-sql.md)   
 [GRANT &#40;Transact-SQL&#41;](../../t-sql/statements/grant-transact-sql.md)   
 [CREATE ROUTE &#40;Transact-SQL&#41;](../../t-sql/statements/create-route-transact-sql.md)   
 [CREATE QUEUE &#40;Transact-SQL&#41;](../../t-sql/statements/create-queue-transact-sql.md)   
 [CREATE SERVICE &#40;Transact-SQL&#41;](../../t-sql/statements/create-service-transact-sql.md)   
 [CREATE ENDPOINT &#40;Transact-SQL&#41;](../../t-sql/statements/create-endpoint-transact-sql.md)   
 [CREATE EVENT NOTIFICATION &#40;Transact-SQL&#41;](../../t-sql/statements/create-event-notification-transact-sql.md)  
  
  
