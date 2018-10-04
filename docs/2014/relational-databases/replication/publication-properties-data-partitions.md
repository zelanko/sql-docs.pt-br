---
title: Propriedades da publicação, partições de dados | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.newpubwizard.pubproperties.datapartitions.f1
ms.assetid: 5869edb7-d05f-495b-b828-b7fd5e828d20
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: df90abfc372d583269152a7cbfe8ab0d5bebf34d
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48211256"
---
# <a name="publication-properties-data-partitions"></a>Propriedades de Publicação, Partições de Dados
  A página **Partições de Dados** da caixa de diálogo **Propriedades de Publicação** permite definir partições de dados para publicações de mesclagem que usam filtragem com parâmetros. Depois de definir as partições, você pode gerar instantâneos para essas partições, fornecendo conjuntos de dados iniciais diferentes para Assinantes diferentes, com base nas propriedades de conexão (logon e/ou nome de computador) dos Assinantes. Você pode também selecionar para permitir aos Assinantes solicitarem a entrega e a geração de instantâneo, se não tiverem um instantâneo disponível para a partição, na primeira vez em que sincronizarem. Para obter mais informações, consulte [Criar um instantâneo para uma publicação de mesclagem com filtros com parâmetros](create-a-snapshot-for-a-merge-publication-with-parameterized-filters.md).  
  
## <a name="options"></a>Opções  
 **Adicionar**  
 Clique em **Adicionar** para definir uma partição. Na caixa de diálogo **Adicionar Partição de Dados** especifique os valores para **HOST_NAME()** e/ou **SUSER_SNAME()** e defina um agendamento de atualização de instantâneos.  
  
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
  
## <a name="see-also"></a>Consulte também  
 [Create a Publication](publish/create-a-publication.md)   
 [Exibir e modificar as propriedades da publicação](publish/view-and-modify-publication-properties.md)   
 [Parameterized Row Filters](merge/parameterized-filters-parameterized-row-filters.md)   
 [Publicar dados e objetos de banco de dados](publish/publish-data-and-database-objects.md)   
 [Snapshots for Merge Publications with Parameterized Filters](snapshots-for-merge-publications-with-parameterized-filters.md)  
  
  
