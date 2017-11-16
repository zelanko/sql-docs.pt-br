---
title: Problemas do artigo | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: sql13.rep.newpubwizard.articleissues.f1
ms.assetid: bde57da2-dd47-412f-9df7-9224968b2448
caps.latest.revision: "23"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 7840d17929da4b25bdab26ba98cba4fc92f1c60c
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2017
---
# <a name="article-issues"></a>Problemas do Artigo
  A página **Problemas do Artigo** lista condições que foram localizadas para artigos e qualquer alteração requerida como resultado dessa alteração. A tabela seguinte lista os possíveis problemas e as ações requeridas para garantir que a replicação e os aplicativos existentes funcionem corretamente.  
  
|Problema do artigo|Detalhes|Ação requerida|  
|-------------------|-------------|---------------------|  
|Colunas uniqueidentifier serão adicionadas a tabelas.|A replicação requer uma coluna de tipo de dados **uniqueidentifier** para todos os artigos em uma publicação de mesclagem ou uma publicação transacional que permita assinaturas de atualização.|A replicação adiciona automaticamente uma coluna de tipo de dados **uniqueidentifier** às tabelas publicadas que não têm uma quando o primeiro instantâneo é gerado. Você deve assegurar que as instruções INSERT e UPDATE que referenciam essas tabelas usam listas de colunas. Assegure também que haja espaço suficiente em disco para a coluna adicional.|  
|Colunas IDENTITY requerem a opção NOT FOR REPLICATION.|A replicação requer que todas as colunas IDENTITY usem a opção NOT FOR REPLICATION. Se uma coluna IDENTITY publicada não usar essa opção, comandos INSERT poderão não ser replicados corretamente.|Aplica-se a publicações criadas em Publicadores que executam o [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] e versões anteriores. Você deve especificar a propriedade NOT FOR REPLICATION para todas as colunas IDENTITY.|  
|Propriedade IDENTITY não transferida aos Assinantes.|Essa publicação não permite atualizações nos Assinantes. Quando as colunas IDENTITY são transferidas para o Assinante, a propriedade IDENTITY não é transferida. Por exemplo, uma coluna definida como INT IDENTITY no Publicador é definida como INT no Assinante.|Aplica-se a publicações criadas em Publicadores que executam o [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] e versões anteriores. Nenhuma ação é necessária.|  
|Tabelas referenciadas por exibições são requeridas.|O[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] requer que todas a tabelas referenciadas por exibições e exibições indexadas publicadas estejam disponíveis no Assinante. Se as tabelas referenciadas não forem publicadas como artigos nesta publicação, elas deverão ser criadas no Assinante manualmente.|Use o botão **Voltar** para navegar até página **Artigos** . Adicione qualquer objeto requerido.|  
|Objetos referenciados por procedimentos armazenados são requeridos.|O[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] requer que todos os objetos referenciados por procedimentos armazenados publicados, como tabelas e funções definidas pelo usuário, estejam disponíveis no Assinante. Se os objetos referenciados não forem publicados como artigos nesta publicação, eles deverão ser criados no Assinante manualmente.|Use o botão **Voltar** para navegar até página **Artigos** . Adicione qualquer objeto requerido.|  
  
## <a name="see-also"></a>Consulte também  
 [Publicar dados e objetos de banco de dados](../../relational-databases/replication/publish/publish-data-and-database-objects.md)   
 [Criar uma publicação](../../relational-databases/replication/publish/create-a-publication.md)  
  
  
