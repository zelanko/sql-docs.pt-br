---
title: "Validar informa&#231;&#245;es de parti&#231;&#227;o para um assinante de mesclagem | Microsoft Docs"
ms.custom: ""
ms.date: "03/04/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "mesclar validação de dados de replicação [replicação do SQL Server], partições"
  - "filtros com parâmetros [replicação do SQL Server], validando informações de partição"
  - "validando informações de partição"
ms.assetid: c059553e-df2c-4333-ba79-e8d6e2890c34
caps.latest.revision: 36
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 36
---
# Validar informa&#231;&#245;es de parti&#231;&#227;o para um assinante de mesclagem
  Quando você define um filtro de linha com parâmetros para uma publicação de mesclagem, usa uma função que faz referência à informação do Assinante, como o nome de logon do Assinante. Por padrão, a replicação valida a informação do Assinante baseada nessa função, antes de cada sincronização e sempre que um instantâneo é aplicado ao Assinante. O processo de validação assegura que os dados são particionados corretamente para cada Assinante. Comportamento de validação é controlado pelo **validate_subscriber_info** propriedade de publicação, que pode ser alterada usando [sp_changemergepublication & #40. O Transact-SQL e 41;](../../relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql.md) ou o **Opções de assinatura** página do **Propriedades de publicação** caixa de diálogo. Para obter mais informações sobre como alterar propriedades de publicação, consulte [View and Modify Publication Properties](../../relational-databases/replication/publish/view-and-modify-publication-properties.md).  
  
## Como a validação de partição funciona  
 Quando uma publicação é filtrada, por exemplo, usando a função **suser_sname ()**, o Merge Agent aplica o instantâneo inicial para cada assinante com base nos dados que é válidos para o **suser_sname ()** expressão.  
  
 Se a validação é ativada, quando o Assinante se conecta novamente ao Publicador para a sincronização seguinte, o Agente de Mesclagem valida a informação do Assinante e assegura que cada partição de assinante seja a mesma que a recebida no instantâneo inicial. Para cada mesclagem subsequente ou aplicativo de instantâneo, o Agente de Mesclagem valida a partição de cada Assinante.  
  
 Se o Agente de Mesclagem detecta que a função usada na expressão de filtragem retornou um valor diferente daquele do instantâneo inicial, o aplicativo de mesclagem ou de instantâneo falhará, e essa assinatura do Assinante poderá necessitar reinicialização. A reinicialização poderá ser necessária para evitar problemas, que podem surgir se as configurações de mesclagem de um Assinante são alteradas, mas poderá ser suficiente para alterar informações no Assinante, como o nome de logon, novamente ao valor usado no momento do instantâneo original.  
  
 Quando o Agente de Mesclagem valida uma partição, além de validar a partição comparando aos valores retornados por todas as funções usadas em expressões de filtragem, o agente também verifica se o instantâneo foi gerado antes das mudanças que o invalidem, como operações de limpeza de metadados ou mudanças de esquema. Se um instantâneo é muito antigo, o Agente de Mesclagem retornará um erro e você precisará gerar novamente um instantâneo particionado para esse Assinante, baseado em um instantâneo regular atual.  
  
## Consulte também  
 [Administração e 40; Replicação e 41;](../../relational-databases/replication/administration/administration-replication.md)   
 [Práticas recomendadas para administração de replicação](../../relational-databases/replication/administration/best-practices-for-replication-administration.md)   
 [Reinicializar as assinaturas](../../relational-databases/replication/reinitialize-subscriptions.md)   
 [Validar os dados replicados](../../relational-databases/replication/validate-replicated-data.md)  
  
  