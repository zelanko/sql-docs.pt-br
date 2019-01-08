---
title: Publicando dados (suplemento MDS para Excel) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: ea84a9aa-aeec-411b-ab8d-bc1b14f864a3
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: 5ed014aaed74ea9da70485b73d089e8ddaae0f43
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52760258"
---
# <a name="publishing-data-mds-add-in-for-excel"></a>Publicando dados (suplemento MDS para Excel)
  No [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)], publique dados no repositório do MDS quando quiser compartilhá-lo com outros usuários. Assim que os dados são publicados, eles ficam disponíveis para outros usuários do suplemento para download.  
  
 Ao publicar dados, qualquer dado que você adicionou ou atualizou será publicado no repositório do MDS. Os dados que você excluiu não são publicados – é necessário excluir os dados separadamente. Para obter mais informações, consulte [Excluir uma linha &#40;Suplemento MDS para Excel&#41;](delete-a-row-mds-add-in-for-excel.md).  
  
> [!NOTE]  
>  A publicação não pode ser usada para criar uma nova entidade. Para obter mais informações sobre como criar entidades, consulte [Criar uma entidade &#40;Suplemento MDS para Excel&#41;](create-an-entity-mds-add-in-for-excel.md).  
  
## <a name="when-multiple-users-publish-at-the-same-time"></a>Quando vários usuários publicam ao mesmo tempo  
 Vários usuários podem publicar atualizações dos mesmos dados. Conforme cada usuário publica, a atualização é salva no banco de dados. Isso significa que um usuário que não estava trabalhando com os dados atualizados mais recentemente ainda pode alterar o valor quando ele publicá-los.  
  
 Somente as atualizações que você faz são publicadas no banco de dados. Os dados desatualizados na planilha não são publicados.  
  
## <a name="transactions-and-annotations"></a>Transações e anotações  
 Cada alteração publicada é salva como transação. Se quiser, você pode adicionar anotações (comentários) a uma transação, para explicar por que fez a alteração.  
  
-   Você não pode anotar exclusões, embora as exclusões sejam salvas como transações que podem ser revertidas por um administrador.  
  
-   Se você alterar o **código** valor para um membro, ele não será registrado como uma transação e todas as transações anteriores para o membro não estão disponíveis.  
  
-   Você pode ver as transações feitas em um membro por outros usuários. Também será possível exibir todas as transações que você fez em um membro, mesmo se não tiver mais permissão para atributos específicos.  
  
 Você pode ver todas as transações feitas em um membro. Para obter mais informações, consulte [Exibir todas as anotações ou transações de um membro &#40;Suplemento MDS para Excel&#41;](view-all-annotations-or-transactions-for-a-member-mds-add-in-for-excel.md).  
  
> [!IMPORTANT]  
>  Se você inserir uma anotação de mais de 500 caracteres, a anotação será truncada automaticamente.  
  
## <a name="business-rule-and-other-validation"></a>Regra de negócio e outra validação  
 Ao publicar dados, a validação é executada para garantir que dados estejam precisos antes de serem adicionados ao repositório do MDS. Se os dados não estiverem de acordo com os critérios especificados, eles não serão publicados no repositório. Para obter mais informações, consulte [Validando dados &#40;Suplemento MDS para Excel&#41;](validating-data-mds-add-in-for-excel.md).  
  
## <a name="related-tasks"></a>Related Tasks  
  
|Descrição da tarefa|Tópico|  
|----------------------|-----------|  
|Publique dados da planilha ativa novamente no repositório do MDS.|[Publicar dados do Excel no MDS &#40;suplemento do MDS para Excel&#41;](import-data-from-excel-to-master-data-services-mds-add-in-for-excel.md)|  
|Exclua uma linha do repositório do MDS e da planilha ao mesmo tempo.|[Excluir uma linha &#40;Suplemento MDS para Excel&#41;](delete-a-row-mds-add-in-for-excel.md)|  
  
## <a name="related-content"></a>Conteúdo relacionado  
  
-   [Atualizando dados &#40;Suplemento MDS para Excel&#41;](refreshing-data-mds-add-in-for-excel.md)  
  
-   [Suplemento do Master Data Services para Microsoft Excel](master-data-services-add-in-for-microsoft-excel.md)  
  
  
