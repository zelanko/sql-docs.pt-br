---
title: "Propriedades da publicação, partições de dados | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: replication
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: sql13.rep.newpubwizard.pubproperties.datapartitions.f1
ms.assetid: 5869edb7-d05f-495b-b828-b7fd5e828d20
caps.latest.revision: "20"
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 1e62fa467c0b757a74ca72bc4d9d7679944a91ca
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/18/2018
---
# <a name="publication-properties-data-partitions"></a>Propriedades de Publicação, Partições de Dados
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] A página **Partições de Dados** da caixa de diálogo **Propriedades de Publicação** permite definir partições de dados para publicações de mesclagem que usam filtragem com parâmetros. Depois de definir as partições, você pode gerar instantâneos para essas partições, fornecendo conjuntos de dados iniciais diferentes para Assinantes diferentes, com base nas propriedades de conexão (logon e/ou nome de computador) dos Assinantes. Você pode também selecionar para permitir aos Assinantes solicitarem a entrega e a geração de instantâneo, se não tiverem um instantâneo disponível para a partição, na primeira vez em que sincronizarem. Para obter mais informações, consulte [Criar um instantâneo para uma publicação de mesclagem com filtros com parâmetros](../../relational-databases/replication/create-a-snapshot-for-a-merge-publication-with-parameterized-filters.md).  
  
## <a name="options"></a>Opções  
 **Adicionar**  
 Clique em **Adicionar** para definir uma partição. Na caixa de diálogo **Adicionar Partição de Dados** especifique os valores para **HOST_NAME()** e/ou **SUSER_SNAME()**e defina um agendamento de atualização de instantâneos.  
  
 **Editar**  
 Selecione uma partição existente na grade e clique em **Editar** para editar a partição.  
  
 **Delete (excluir)**  
 Selecione uma partição existente na grade e clique em **Excluir** para excluir a partição.  
  
 **Gerar os instantâneos selecionados agora**  
 Selecione uma ou mais partições na grade e clique em **Gerar os instantâneos selecionados agora** para gerar os instantâneos para essas partições.  
  
 **Limpar os instantâneos existentes**  
 Selecione uma ou mais partições na grade e clique em **Limpar os instantâneos existentes** para limpar os instantâneos para essas partições.  
  
 **Definir automaticamente uma partição e gerar um instantâneo, se necessário, quando um novo Assinante tentar sincronizar**  
 Selecione essa opção se quiser permitir que os Assinantes solicitem geração e aplicação de  instantâneo. Os Assinantes podem exigir essa opção, se não tiverem um instantâneo disponível para a partição, na primeira vez em que sincronizarem.  
  
## <a name="see-also"></a>Consulte Também  
 [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md)   
 [Exibir e modificar as propriedades da publicação](../../relational-databases/replication/publish/view-and-modify-publication-properties.md)   
 [Parameterized Row Filters](../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md)   
 [Publicar dados e objetos de banco de dados](../../relational-databases/replication/publish/publish-data-and-database-objects.md)   
 [Snapshots for Merge Publications with Parameterized Filters](../../relational-databases/replication/snapshots-for-merge-publications-with-parameterized-filters.md)  
  
  
