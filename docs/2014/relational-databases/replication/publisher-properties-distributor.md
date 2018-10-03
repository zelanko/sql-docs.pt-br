---
title: Propriedades do Publicador – Distribuidor | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.configdistwizard.distpubproperties.f1
helpviewer_keywords:
- Publisher Properties dialog box
ms.assetid: ab6ada76-0f99-43fe-b524-baac7b1bc483
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: b0b1cddd1c5849f43aac7f41a2f4b679af21760b
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48057952"
---
# <a name="publisher-properties---distributor"></a>Propriedades do Publicador - Distribuidor
  A caixa de diálogo **Propriedades do Publicador** permite exibir e modificar propriedades associadas com a relação entre o Publicador e seu Distribuidor.  
  
## <a name="options"></a>Opções  
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
  
## <a name="see-also"></a>Consulte também  
 [Create a Publication](publish/create-a-publication.md)   
 [Exibir e modificar propriedades de Publicador e Distribuidor](view-and-modify-distributor-and-publisher-properties.md)   
 [Referência de propriedades &#40;Replicação&#41;](properties-reference-replication.md)  
  
  
