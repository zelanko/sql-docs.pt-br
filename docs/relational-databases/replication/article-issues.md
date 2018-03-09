---
title: Problemas do artigo | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: replication
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: sql13.rep.newpubwizard.articleissues.f1
ms.assetid: bde57da2-dd47-412f-9df7-9224968b2448
caps.latest.revision: "23"
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 4935f6e607270401c095f78bd6142828e8581071
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/18/2018
---
# <a name="article-issues"></a>Problemas do Artigo
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] A página **Problemas do Artigo** lista condições que foram localizadas para artigos e qualquer alteração requerida como resultado dessa alteração. A tabela seguinte lista os possíveis problemas e as ações requeridas para garantir que a replicação e os aplicativos existentes funcionem corretamente.  
  
|Problema do artigo|Detalhes|Ação requerida|  
|-------------------|-------------|---------------------|  
|Colunas uniqueidentifier serão adicionadas a tabelas.|A replicação requer uma coluna de tipo de dados **uniqueidentifier** para todos os artigos em uma publicação de mesclagem ou uma publicação transacional que permita assinaturas de atualização.|A replicação adiciona automaticamente uma coluna de tipo de dados **uniqueidentifier** às tabelas publicadas que não têm uma quando o primeiro instantâneo é gerado. Você deve assegurar que as instruções INSERT e UPDATE que referenciam essas tabelas usam listas de colunas. Assegure também que haja espaço suficiente em disco para a coluna adicional.|  
|Colunas IDENTITY requerem a opção NOT FOR REPLICATION.|A replicação requer que todas as colunas IDENTITY usem a opção NOT FOR REPLICATION. Se uma coluna IDENTITY publicada não usar essa opção, comandos INSERT poderão não ser replicados corretamente.|Aplica-se a publicações criadas em Publicadores que executam o [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] e versões anteriores. Você deve especificar a propriedade NOT FOR REPLICATION para todas as colunas IDENTITY.|  
|Propriedade IDENTITY não transferida aos Assinantes.|Essa publicação não permite atualizações nos Assinantes. Quando as colunas IDENTITY são transferidas para o Assinante, a propriedade IDENTITY não é transferida. Por exemplo, uma coluna definida como INT IDENTITY no Publicador é definida como INT no Assinante.|Aplica-se a publicações criadas em Publicadores que executam o [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] e versões anteriores. Nenhuma ação é necessária.|  
|Tabelas referenciadas por exibições são requeridas.|O[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] requer que todas a tabelas referenciadas por exibições e exibições indexadas publicadas estejam disponíveis no Assinante. Se as tabelas referenciadas não forem publicadas como artigos nesta publicação, elas deverão ser criadas no Assinante manualmente.|Use o botão **Voltar** para navegar até página **Artigos** . Adicione qualquer objeto requerido.|  
|Objetos referenciados por procedimentos armazenados são requeridos.|O[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] requer que todos os objetos referenciados por procedimentos armazenados publicados, como tabelas e funções definidas pelo usuário, estejam disponíveis no Assinante. Se os objetos referenciados não forem publicados como artigos nesta publicação, eles deverão ser criados no Assinante manualmente.|Use o botão **Voltar** para navegar até página **Artigos** . Adicione qualquer objeto requerido.|  
  
## <a name="see-also"></a>Consulte Também  
 [Publicar dados e objetos de banco de dados](../../relational-databases/replication/publish/publish-data-and-database-objects.md)   
 [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md)  
  
  
