---
title: "Segurança do agente de distribuição | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.rep.security.DA.f1
helpviewer_keywords:
- Distribution Agent Security dialog box
ms.assetid: de40cc21-2e58-4464-9be7-b5b90c925e9b
caps.latest.revision: 25
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 44bbfd608ad2511c95a872f07eac657ae7616e6d
ms.contentlocale: pt-br
ms.lasthandoff: 06/22/2017

---
# <a name="distribution-agent-security"></a>Segurança do Distribution Agent
  A caixa de diálogo **Segurança do Distribution Agent** permite especificar a conta do Windows na qual o Distribution Agent é executado. O Distribution Agent é executado no Distribuidor para assinaturas push e no Assinante para assinaturas pull. A conta do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows é também referida como *conta do processo*, porque o processo do agente é executado nessa conta. Opções adicionais disponíveis na caixa de diálogo dependem de como você a acessa:  
  
-   Se a caixa de diálogo for acessada do Assistente para Nova Assinatura, também permitirá que você especifique o contexto no qual o Distribution Agent fará conexões com o Assinante (para assinaturas push) ou com o Publicador e o Distribuidor (para assinaturas pull). A conexão pode ser feita representando a conta do Windows ou no contexto de uma conta do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] especificada por você.  
  
-   Se a caixa de diálogo for acessada da caixa de diálogo **Propriedades da Assinatura** , especifique o contexto no qual o Distribution Agent faz conexões, clicando no botão de propriedades (**...**) na linha **Conexão do Assinante** ou **Conexão do Publicador** daquela caixa de diálogo. Para obter mais informações sobre como acessar a caixa de diálogo **Propriedades da Assinatura**, consulte [Exibir e modificar as propriedades da assinatura push](../../relational-databases/replication/view-and-modify-push-subscription-properties.md) e [Exibir e modificar as propriedades da assinatura pull](../../relational-databases/replication/view-and-modify-pull-subscription-properties.md).  
  
 Todas as contas devem ser válidas, com a senha correta especificada para cada conta. Contas e senhas não são validadas até que um agente seja executado.  
  
## <a name="options"></a>Opções  
 **Process Account**  
 Insira uma conta do Windows na qual o Distribution Agent seja executado:  
  
-   Para assinaturas push, a conta deve:  
  
    -   Ser, no mínimo, um membro da função de banco de dados fixa **db_owner** no banco de dados de distribuição.  
  
    -   Ser um membro da PAL (lista de acesso à publicação).  
  
    -   Ter permissões de leitura no compartilhamento de instantâneo.  
  
    -   Ter permissões de leitura no diretório de instalação do provedor OLE DB para o Assinante se a assinatura for para um Assinante não[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   Para assinaturas pull, a conta deve ser, no mínimo, um membro da função de banco de dados fixa **db_owner** no banco de dados de assinatura.  
  
 Serão requeridas permissões adicionais se a conta do processo for representada quando as conexões forem feitas. Consulte as seções **Conectar ao Distribuidor** e **Conectar ao Assinante** abaixo.  
  
 **Conta do processo** não pode ser especificada para assinaturas pull para o [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)], porque o Distribution Agent não é executado em instâncias do [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)].  
  
 **Senha** e **Confirmar Senha**  
 Insira a senha para a conta do Windows.  
  
 **Conectar ao Distribuidor**  
 Para assinaturas push, conexões com o Distribuidor são sempre feitas representando a conta especificada na caixa de texto **Conta do processo** .  
  
 Para assinaturas pull, selecione se o Distribution Agent deve fazer conexões com o Publicador e o Distribuidor representando a conta especificada na caixa de texto **Conta do processo** ou usando uma conta [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Se você optar por usar uma conta do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , insira um logon e uma senha [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
> [!NOTE]  
>  É recomendável a seleção para representar a conta do Windows em vez de usar uma conta do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 A conta do Windows ou do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usada para a conexão deve:  
  
-   Ser um membro da PAL.  
  
-   Ter permissões de leitura no compartilhamento de instantâneo.  
  
 **Conectar ao Assinante**  
 Para assinaturas pull, as conexões com o Assinante são sempre feitas representando a conta especificada na caixa de texto **Conta do processo** .  
  
 Para assinaturas push, as opções são diferentes para Assinantes [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e não[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] :  
  
-   Para Assinantes [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] : selecione se o Distribution Agent deve fazer conexões com o Assinante representando a conta especificada na caixa de texto **Conta do processo** ou usando uma conta [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Se você optar por usar uma conta do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , insira um logon e uma senha [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
    > [!NOTE]  
    >  É recomendável a seleção para representar a conta do Windows em vez de usar uma conta do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
     A conta do Windows ou do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usada para conexão com o Assinante deve ser, no mínimo, um membro da função de banco de dados fixa **db_owner** no banco de dados de assinatura.  
  
-   Para Assinantes não[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , especifique o logon do banco de dados no Assinante que deve ser usado quando o Distribution Agent conectar ao Assinante. O logon deve ter permissões adequadas para criar objetos no banco de dados de assinatura. Para mais informações sobre configuração de assinantes não [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], consulte [Criar uma assinatura para um assinante não SQL Server](../../relational-databases/replication/create-a-subscription-for-a-non-sql-server-subscriber.md).  
  
 **Opções de conexão adicionais**  
 Somente Assinantes não[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Especifique qualquer opção de conexão adicional para o Assinante na forma de uma sequência de conexão (Oracle não requer opções adicionais). Cada opção deverá estar separada por um ponto-e-vírgula. A seguir, um exemplo de uma sequência de conexão IBM DB2 (as quebras de linha são para facilitar a leitura):  
  
```  
Provider=DB2OLEDB;Initial Catalog=MY_SUBSCRIBER_DB;Network Transport Library=TCP;Host CCSID=1252;  
PC Code Page=1252;Network Address=MY_SUBSCRIBER;Network Port=50000;Package Collection=MY_PKGCOL;  
Default Schema=MY_SCHEMA;Process Binary as Character=False;Units of Work=RUW;DBMS Platform=DB2/NT;  
Persist Security Info=False;Connection Pooling=True;  
```  
  
 A maioria das opções na cadeia de caracteres é específica do servidor DB2 que você está configurando, mas a opção **Processar Binário como Caractere** sempre deve ser definida como **False**. Um valor é necessário para a opção **Catálogo Inicial** para identificar o banco de dados de assinatura. Para obter mais informações, consulte [IBM DB2 Subscribers](../../relational-databases/replication/non-sql/ibm-db2-subscribers.md).  
  
## <a name="see-also"></a>Consulte também  
 [Gerenciar logons e senhas na replicação](../../relational-databases/replication/security/manage-logins-and-passwords-in-replication.md)   
 [Modelo de segurança do agente de replicação](../../relational-databases/replication/security/replication-agent-security-model.md)   
 [Visão geral dos agentes de replicação](../../relational-databases/replication/agents/replication-agents-overview.md)   
 [Melhores práticas de segurança da replicação](../../relational-databases/replication/security/replication-security-best-practices.md)   
 [Assinar Publicações](../../relational-databases/replication/subscribe-to-publications.md)  
  
  
