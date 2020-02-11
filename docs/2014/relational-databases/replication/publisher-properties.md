---
title: Propriedades do Publicador Replicação do SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.configdistwizard.distpubproperties.f1
- sql12.rep.configdistwizard.pubproperties.general.f1
- sql12.rep.configdistwizard.pubproperties.pubdb.f1
- sql12.rep.configdistwizard.pubproperties.subscribers.f1
ms.assetid: 98df1aea-0406-40bf-a917-4bd80464125c
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 2ea467b00223e31ec7672d4d54a49150cf05368c
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "63261983"
---
# <a name="sql-server-replication-publisher-properties"></a>Propriedades do Publicador Replicação do SQL Server
  Esta seção contém informações sobre as propriedades do Publicador disponíveis no distribuidor e no Publicador. 

## <a name="general"></a>Geral  
  A página **Geral** da caixa de diálogo **Propriedades do Publicador** exibe informações somente leitura no Distribuidor e no banco de dados de distribuição que o Publicador usa. Para alterar o Distribuidor ou o banco de dados de um Publicador:  
  
1.  Desabilite a publicação no Publicador. Para obter mais informações, consulte [Desabilitar a publicação e a distribuição](disable-publishing-and-distribution.md).    
2.  Reconfigure a publicação e a distribuição Para obter mais informações, consulte [Configure Publishing and Distribution](configure-publishing-and-distribution.md).  

## <a name="distributor"></a>Distribuidor
  A caixa de diálogo **Propriedades do Publicador** permite exibir e modificar propriedades associadas com a relação entre o Publicador e seu Distribuidor.  
  
### <a name="options"></a>Opções  
 **Conexão do Agente com o Publicador**  
 Especifique o contexto no qual os agentes seguintes fazem conexões do Distribuidor com o Publicador:  
  
-   O Agente de Leitor de Fila para publicações transacionais, que permite assinaturas de atualização enfileiradas.  
  
-   O Agente de Instantâneo e Agente de Leitor de Log para publicações Oracle.  
  
 Selecione **Representar conta de processo do agente** para efetuar conexões com o Publicador usando o contexto de conta do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows na qual esses agentes executam ou especifique **Autenticação do SQL Server**e insira um valor para **Logon** e **Senha**. É recomendado que você selecione **Representar conta de processo do agente**. Para obter mais informações sobre a segurança do agente, consulte [Modelo de segurança do agente de replicação](security/replication-agent-security-model.md).  
  
 As contas do Windows nas quais esses agentes executam são especificadas no Assistente para Nova Publicação. Essas contas podem ser alteradas:  
  
-   Na caixa de diálogo **Propriedades do Distribuidor** para o Agente de Leitor de Fila.  
  
-   Na caixa de diálogo **Propriedades de Publicação** para o Agente de Instantâneo e Agente de Leitor de Log.  
  
 **Diversos**  
 As propriedades **Tipo de Publicador** e **Nome do Banco de dados de Distribuição** são somente leitura. A propriedade **Pasta Padrão de Instantâneo** pode ser alterada. Para obter mais informações sobre a pasta de instantâneos, consulte [Proteger a pasta de instantâneos](security/secure-the-snapshot-folder.md).  
  

## <a name="publication-databases"></a>Bancos de Dados de Publicação
  A página **Bancos de dados de Publicação** da caixa de diálogo **Propriedades do Publicador** permite que um usuário da função de servidor fixa **sysadmin** habilite bancos de dados para replicação. Habilitar um banco de dados não publica esse banco de dados, mas permite que qualquer usuário na função de banco de dados fixa **db_owner** daquele banco de dados crie uma ou mais publicações no banco de dados.  
  
### <a name="options"></a>Opções  
 **Transacional.**  
 Marque essa caixa de seleção para permitir que usuários na função de banco de dados fixa **db_owner** criem publicações de instantâneo ou transacionais no banco de dados. 
  
 **Mesclagem**  
 Marque essa caixa de seleção para permitir que usuários na função de banco de dados fixa **db_owner** criem publicações de mesclagem no banco de dados.  

## <a name="subscribers"></a>Publicadores

  A página **Assinantes** da caixa de diálogo **Propriedades do Editor** é usada por Editores que executam versões do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] anteriores à [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]. A página permite habilitar Publicadores a receber dados de publicações neste Publicador. Permitir que um Assinante receba dados deste Publicador não cria assinaturas para publicações neste Publicador. Para criar uma assinatura, você deve usar o Assistente para Nova Assinatura.  
  
### <a name="options"></a>Opções  
 **Publicadores**  
 A grade de propriedade **Assinantes** mostra Assinantes habilitados a receber dados de publicações neste Publicador. Clique no botão de propriedades **(...)** próximo ao Assinante para exibir e definir propriedades adicionais.  
  
 **Adicionar**  
 Clique em **Adicionar** para adicionar um Assinante e depois clique em **Adicionar Assinante SQL Server** ou **Adicionar Assinante não SQL Server**.  

## <a name="see-also"></a>Consulte Também  
 [Exibir e modificar propriedades de Publicador e Distribuidor](view-and-modify-distributor-and-publisher-properties.md)   

  
  
