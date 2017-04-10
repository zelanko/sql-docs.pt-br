---
title: "Li&#231;&#227;o 3: Validando a assinatura e medindo a lat&#234;ncia | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
applies_to: 
  - "SQL Server 2016"
helpviewer_keywords: 
  - "replicação [SQL Server], tutoriais"
ms.assetid: 147f7b93-1804-4e0b-9e17-57a51d035b2a
caps.latest.revision: 12
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 12
---
# Li&#231;&#227;o 3: Validando a assinatura e medindo a lat&#234;ncia
Nesta lição, você usará tokens de rastreadores para verificar se as alterações estão sendo replicadas para o Assinante e para determinar: a latência, o tempo decorrido entre o momento em que a alteração é feita no Publicador, e o momento em que ela aparece no Assinante. Esta lição exige que você tenha concluído a lição anterior, [Lição 2: Criando uma assinatura na publicação transacional](../../relational-databases/replication/lesson-2-creating-a-subscription-to-the-transactional-publication.md).  
  
### Para inserir um token de rastreamento e exibir informações sobre o token  
  
1.  Conecte-se ao Publicador no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], expanda o nó de servidor, clique com o botão direito do mouse na pasta **Replicação** e clique em **Iniciar o Replication Monitor**.  
  
    O Replication Monitor é iniciado.  
  
2.  Expanda um grupo Publicador no painel esquerdo; expanda a instância do Publicador e, depois, clique na publicação **AdvWorksProductTrans** .  
  
3.  Clique na guia **Tokens de Rastreamento** .  
  
4.  Clique em **Inserir Rastreador**.  
  
5.  Exiba o tempo decorrido para o token de rastreamento nas seguintes colunas: **Publicador para Distribuidor**, **Distribuidor para Assinante**, **Latência Total**. Um valor de **Pendente** indica que o token não alcançou um determinado ponto.  
  
## Próximas etapas  
Nessa lição, você usou tokens de rastreador com êxito, para validar que as alterações de dados sejam replicadas do Publicador para o Assinante. É igualmente possível inserir, atualizar ou excluir dados da tabela **Product** do Publicador e consultar a tabela **Product** do Assinante para exibir essas alterações após serem replicadas.  
  
Isso encerra o tutorial Replicando Dados entre Servidores Conectados Continuamente Para obter um tutorial semelhante, que utilize replicação de mesclagem, consulte [Tutorial: Replicating Data with Mobile Clients](../../relational-databases/replication/tutorial-replicating-data-with-mobile-clients.md).  
  
## Consulte também  
[Measure Latency and Validate Connections for Transactional Replication](../../relational-databases/replication/monitor/measure-latency-and-validate-connections-for-transactional-replication.md)  
  
  
  
