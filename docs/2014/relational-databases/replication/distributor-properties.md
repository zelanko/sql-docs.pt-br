---
title: Propriedades do distribuidor | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.configdistwizard.distdbproperties.f1
- sql12.rep.configdistwizard.distproperties.general.f1
- sql12.rep.configdistwizard.distproperties.publishers.f1
- sql12.rep.configdistwizard.distproperties.publishers.f1
ms.assetid: f643c7c3-f238-4835-b81e-2c2b3b53b23f
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: ae7c7197fffcad7f64a82cf7c060e2e35e9bf460
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62721400"
---
# <a name="sql-server-replication-distributor-properties"></a>Propriedades do distribuidor Replicação do SQL Server
Este tópico discute as propriedades encontradas nas páginas **geral**, **editores**e banco de **dados de distribuição** na janela **Propriedades do distribuidor** . 

## <a name="general"></a>Geral
  A página **Geral** da caixa de diálogo **Propriedades do Distribuidor** permite adicionar e excluir bancos de dados de distribuição e definir propriedades do banco de dados de distribuição.  
  
 O banco de dados de distribuição armazena metadados e dados de histórico para todos os tipos de replicação e transações para replicação transacional. Em muitos casos, um único banco de dados de distribuição é suficiente. Porém, se vários Publicadores usarem um único Distribuidor, considere criar um banco de dados de distribuição para cada Publicador. Fazer isso assegura que os dados que fluem por cada banco de dados de distribuição são distintos.  
  
### <a name="options"></a>Opções  
 **Bancos de dados**  
 A grade de propriedades dos **Bancos de Dados** mostra as nome e as propriedades de retenção dos bancos de dados de distribuição no Distribuidor. **Retenção de Transação** é o período de tempo em que as transações são armazenadas para replicação transacional (a retenção da transação também é conhecida como retenção de distribuição). **Retenção de Histórico** é o período de tempo em que os metadados de histórico são armazenados para todos os tipos de replicação. Para mais informações sobre retenção de distribuição, consulte [Desativação e expiração da assinatura](subscription-expiration-and-deactivation.md).  
  
 Clique no botão de propriedades ( **...** ) na grade de propriedades de **Bancos de dados** para iniciar a caixa de diálogo **Propriedades do Banco de Dados de Distribuição** .  
  
 **Novo**  
 Clique para criar um novo banco de dados de distribuição.  
  
 **Delete (excluir)**  
 Selecione um banco de dados de distribuição existente na grade de propriedade de **Bancos de Dados** e clique em **Excluir** para excluir o banco de dados. O banco de dados de distribuição não poderá ser excluído se houver apenas esse banco de dados; cada distribuidor deve ter pelo menos um banco de dados de distribuição. Para excluir todos os bancos de dados de distribuição, você deve desabilitar a distribuição no computador. Para obter mais informações, consulte [Desabilitar a publicação e a distribuição](disable-publishing-and-distribution.md).  
  
 **Padrões de Perfil**  
 Clique para acessar perfis de agente de replicação na caixa de diálogo **Perfis de Agente** . Para obter mais informações sobre perfis, consulte [Replication Agent Profiles](agents/replication-agent-profiles.md).  

## <a name="publishers"></a>Publicadores

  A página **Publicadores** da caixa de diálogo **Propriedades do Distribuidor** permite habilitar Publicadores a usarem esse Distribuidor. Você também pode definir propriedades associadas a esses Publicadores. Esteja ciente de que habilitar um Publicador a usar esse servidor como seu Distribuidor remoto não faz daquele servidor um Publicador. Você deve se conectar ao Publicador, configurá-lo para publicação e escolher esse servidor como o Distribuidor. Você pode configurar o Publicador e escolher um Distribuidor pelo Assistente para Nova Publicação.  
  
### <a name="options"></a>Opções  
 **Publicadores**  
 Selecione os servidores que têm permissão para usar esse Distribuidor. Clique no botão **(...)** próximo ao Publicador para exibir e definir propriedades adicionais.  
  
 **Adicionar**  
 Se o servidor que você deseja permitir não estiver listado, clique em **Adicionar** para adicionar um Publicador do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou um Publicador Oracle à lista de Publicadores disponíveis. Se o servidor que você adicionar for o primeiro a usar esse Distribuidor como remoto, você será solicitado a fornecer uma senha de vínculo administrativo.  
  
 **Senha de vínculo administrativo**  
 Use para especificar ou atualizar a senha para a conexão que a replicação faz entre o Publicador e o Distribuidor remoto, usando o logon: **distributor_admin** .  
  
-   Se o  Distribuidor servir somente como Distribuidor local, essa senha será gerada aleatoriamente e configurada automaticamente.  
-   Se o Distribuidor já tiver um Publicador remoto, uma senha terá sido fornecida inicialmente nessa página ou na página **Senha do Distribuidor** do Assistente para Configurar Distribuição.    
-   Se você ativar o primeiro Publicador remoto para esse Distribuidor, você será solicitado a inserir uma senha.  
  
 Para mais informações sobre segurança de distribuidores, consulte [Proteger o distribuidor](security/secure-the-distributor.md).  

## <a name="distribution-database"></a>Banco de dados de distribuição
 A caixa de diálogo **Propriedades do Banco de Dados de Distribuição** permite a exibição de várias propriedades e a definição do período de retenção da transação e do período de retenção do histórico para o banco de dados.  
  
### <a name="options"></a>Opções  
 **Nome**  
 O nome do banco de dados de distribuição, que assume o padrão “distribuição” (somente leitura).  
  
 **Locais de arquivo**  
 O local do arquivo de banco de dados e do arquivo de log (somente leitura).  
  
 **Período de retenção de transação**  
 Também conhecido como o período de retenção de distribuição. O tempo de armazenamento das transações para replicação transacional. Para obter mais informações, consulte [Subscription Expiration and Deactivation](subscription-expiration-and-deactivation.md).  
  
 **Período de retenção de histórico**  
 O período de armazenamento dos metadados de histórico para todos os tipos de replicação.  
  
 **Segurança do Queue Reader Agent**  
 O Queue Reader Agent é usado pela replicação transacional com assinaturas de atualização enfileiradas. Um Agente de Leitor de Fila será criado automaticamente se você selecionar **Publicação transacional com assinaturas de atualização** na página **Tipo de Publicação** do Assistente para Nova Publicação. Clique em **Configurações de Segurança…** para alterar a conta na qual o agente é executado e efetua conexões com o Distribuidor.  
  
 Um Queue Reader Agent também pode ser criado selecionando **Criar Queue Reader Agent** nessa página (essa opção estará desabilitada se o agente já tiver sido criado).  
  
 Informações de conexão adicionais para o Queue Reader Agent são especificadas em dois lugares:    
-   O agente se conecta ao Publicador usando as credenciais especificadas na caixa de diálogo **Propriedades do Publicador** , disponível na página **Publicadores** da caixa de diálogo **Propriedades do Distribuidor** .    
-   O agente se conecta ao Assinante usando as credenciais especificadas para o Agente de Distribuição no Assistente para Nova Assinatura.  
  
 Para obter mais informações, \\consulte [Replication Agent Security Model](security/replication-agent-security-model.md). 

  
## <a name="see-also"></a>Consulte Também  
 [Configurar Distribuição](configure-distribution.md)   
 [Exibir e modificar propriedades de Publicador e Distribuidor](view-and-modify-distributor-and-publisher-properties.md)   

  
  
