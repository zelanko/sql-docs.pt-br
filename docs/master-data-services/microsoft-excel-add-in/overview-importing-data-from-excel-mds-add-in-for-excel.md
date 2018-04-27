---
title: 'Visão geral: Importando dados do Excel (Suplemento MDS para Excel) | Microsoft Docs'
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.service: ''
ms.component: microsoft-excel-add-in
ms.reviewer: ''
ms.suite: sql
ms.technology:
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: ea84a9aa-aeec-411b-ab8d-bc1b14f864a3
caps.latest.revision: 13
author: leolimsft
ms.author: lle
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 75c910f482f97090ec46e9ae97be297095e8d9c0
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2018
---
# <a name="overview-importing-data-from-excel-mds-add-in-for-excel"></a>Visão geral: importação de dados do Excel (Suplemento MDS para Excel)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  No [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)], publique dados no repositório do MDS quando quiser compartilhá-lo com outros usuários. Assim que os dados são publicados, eles ficam disponíveis para outros usuários do suplemento para download.  
  
 Ao publicar dados, qualquer dado que você adicionar ou atualizar será publicado no repositório do MDS. Os dados que você excluir não serão publicados – você deverá excluir os dados separadamente. Para obter mais informações, consulte [Excluir uma linha &#40;Suplemento MDS para Excel&#41;](../../master-data-services/microsoft-excel-add-in/delete-a-row-mds-add-in-for-excel.md).  
  
> [!NOTE]  
>  A publicação não pode ser usada para criar uma nova entidade. Para obter mais informações sobre como criar entidades, consulte [Criar uma entidade &#40;Suplemento MDS para Excel&#41;](../../master-data-services/microsoft-excel-add-in/create-an-entity-mds-add-in-for-excel.md).  
  
## <a name="when-multiple-users-publish-at-the-same-time"></a>Quando vários usuários publicam ao mesmo tempo  
 Vários usuários podem publicar atualizações dos mesmos dados. Conforme cada usuário publica, a atualização é salva no banco de dados. Isso significa que um usuário que não estava trabalhando com os dados atualizados mais recentemente ainda pode alterar o valor quando ele publicá-los.  
  
 Somente as atualizações que você faz são publicadas no banco de dados. Os dados desatualizados na planilha não são publicados.  
  
## <a name="transactions-and-annotations"></a>Transações e anotações  
 Cada alteração publicada é salva como transação. Se quiser, você pode adicionar anotações (comentários) a uma transação, para explicar por que fez a alteração.  
  
-   Você não pode anotar exclusões, embora as exclusões sejam salvas como transações que podem ser revertidas por um administrador.  
  
-   Se você alterar o valor de **Código** para um membro, todas as transações anteriores do membro não serão disponibilizadas. Ao retornar o valor **Code** para o valor original, você pode acessar as transações anteriores.  
  
-   Você pode ver as transações feitas em um membro por outros usuários. Você também pode ver todas as transações que você fez em um membro, mesmo se não tiver mais permissão para atributos específicos. Não é possível exibir as transações que envolvam atributos em que a permissão esteja definida como Negar.  
  
 Você pode ver todas as transações feitas em um membro. Para obter mais informações, consulte [Exibir todas as anotações ou transações de um membro &#40;Suplemento MDS para Excel&#41;](../../master-data-services/microsoft-excel-add-in/view-all-annotations-or-transactions-for-a-member-mds-add-in-for-excel.md).  
  
> [!IMPORTANT]  
>  Se você inserir uma anotação de mais de 500 caracteres, a anotação será truncada automaticamente.  
  
## <a name="business-rule-and-other-validation"></a>Regra de negócio e outra validação  
 Ao publicar dados, a validação é executada para garantir que dados estejam precisos antes de serem adicionados ao repositório do MDS. Se os dados não estiverem de acordo com os critérios especificados, eles não serão publicados no repositório. Para obter mais informações, consulte [Validando dados &#40;Suplemento MDS para Excel&#41;](../../master-data-services/microsoft-excel-add-in/validating-data-mds-add-in-for-excel.md).  
  
## <a name="related-tasks"></a>Related Tasks  
  
|Descrição da tarefa|Tópico|  
|----------------------|-----------|  
|Publique dados da planilha ativa novamente no repositório do MDS.|[Importar dados do Excel para o Master Data Services &#40;Suplemento MDS para Excel&#41;](../../master-data-services/microsoft-excel-add-in/import-data-from-excel-to-master-data-services-mds-add-in-for-excel.md)|  
|Exclua uma linha do repositório do MDS e da planilha ao mesmo tempo.|[Excluir uma linha &#40;Suplemento MDS para Excel&#41;](../../master-data-services/microsoft-excel-add-in/delete-a-row-mds-add-in-for-excel.md)|  
|Veja anotações (comentários) e transações de linhas de dados (membros) quando quiser verificar as atualizações dos dados com o passar do tempo.|[Exibir todas as anotações ou transações de um membro &#40;Suplemento MDS para Excel&#41;](../../master-data-services/microsoft-excel-add-in/view-all-annotations-or-transactions-for-a-member-mds-add-in-for-excel.md)|  
|Combine dados de duas planilhas quando você desejar comparar dados antes de publicar.|[Combinar dados &#40;Suplemento MDS para Excel&#41;](../../master-data-services/microsoft-excel-add-in/combine-data-mds-add-in-for-excel.md)|  

  
## <a name="related-content"></a>Conteúdo relacionado  
  
-   [Atualizando dados &#40;Suplemento MDS para Excel&#41;](../../master-data-services/microsoft-excel-add-in/refreshing-data-mds-add-in-for-excel.md)  
  
-   [Suplemento do Master Data Services para Microsoft Excel](../../master-data-services/microsoft-excel-add-in/master-data-services-add-in-for-microsoft-excel.md)  
  
  
