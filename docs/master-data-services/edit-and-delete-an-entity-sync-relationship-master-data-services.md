---
description: Editar e excluir um relacionamento de sincronização de entidade (Master Data Services)
title: Editar e excluir um relacionamento de sincronização de entidade
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: 9a5e37f3-352e-45a6-b4a0-6f98f83b4bd8
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 68b88f98626f2645d2ca69311f4302e0d51fe51c
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88389462"
---
# <a name="edit-and-delete-an-entity-sync-relationship-master-data-services"></a>Editar e excluir um relacionamento de sincronização de entidade (Master Data Services)

[!INCLUDE [SQL Server - Windows only ASDBMI  ](../includes/applies-to-version/sql-windows-only-asdbmi.md)]

  A sincronização de entidade é uma sincronização unidirecional e repetível entre versões da entidade. Ela fornece uma maneira de compartilhar dados de entidade entre diferentes modelos. Você pode editar e excluir um relacionamento de sincronização que você criou.  
  
## <a name="prerequisites"></a>Pré-requisitos  
 Pré-requisitos para executar um relacionamento de sincronização de entidade.  
  
-   Você deve ter permissão para acessar a área funcional Administração do Sistema. Para obter mais informações, consulte [permissões de área funcional &#40;Master Data Services&#41;](../master-data-services/functional-area-permissions-master-data-services.md).  
  
-   Você deve ser um administrador de modelo do modelo de destino. Para obter mais informações, consulte [administradores &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md).  
  
-   É necessário ter, pelo menos, acesso de leitura à entidade de origem e a todos os seus atributos e membros.  
  
 Pré-requisitos para excluir um relacionamento de sincronização de entidade.  
  
-   Você deve ter permissão para acessar a área funcional Administração do Sistema. Para obter mais informações, consulte [permissões de área funcional &#40;Master Data Services&#41;](../master-data-services/functional-area-permissions-master-data-services.md).  
  
-   Você deve ser um administrador de modelo do modelo de destino. Para obter mais informações, consulte [administradores &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md).  
  
 Considere o seguinte ao editar um relacionamento de sincronização de entidade.  
  
-   As entidades de origem e de destino devem ser em modelos diferentes.  
  
-   Um status de versão da entidade de destino não deve ser confirmado.  
  
-   Depois que o relacionamento de sincronização é estabelecido, o destino é imediatamente sincronizado com a origem.  
  
-   A versão da entidade de destino não pode ser uma versão da entidade de origem de outro relacionamento de sincronização.  
  
 Considere o seguinte ao executar um relacionamento de sincronização de entidade.  
  
-   Somente membros folha serão copiados  
  
-   Atributos baseados em domínio não serão copiados.  
  
-   Membros flexíveis excluídos não serão copiados.  
  
-   Sincronização não gera transações/históricos da entidade de destino.  
  
 **Para editar um relacionamento de sincronização de entidade**  
  
1.  No Master Data Manager, clique em **Administração do Sistema**.  
  
2.  Na página **Exibição de Modelos** , na barra de menus, aponte para **Gerenciar** e clique em **Sincronização de Entidades**.  
  
3.  Na página **Manutenção de Sincronização da Entidade** selecione um relacionamento de sincronização na grade.  
  
4.  Clique em **Editar**. Um painel aparece no lado direito.  
  
5.  Alterar **Frequência**. Selecione **Sincronização Sob Demanda**, ou selecione **Sincronização Automática** e configure uma frequência.  
  
6.  Clique em **Save** (Salvar).  
  
 **Para excluir um relacionamento de sincronização de entidade**  
  
1.  No Master Data Manager, clique em **Administração do Sistema**.  
  
2.  Na página **Exibição de Modelos** , na barra de menus, aponte para **Gerenciar** e clique em **Sincronização de Entidades**.  
  
3.  Na página **Manutenção de Sincronização da Entidade** selecione um relacionamento de sincronização na grade.  
  
4.  Clique em **Excluir**.  
  
5.  Na caixa de diálogo de confirmação, clique em **OK**.  
  
## <a name="see-also"></a>Consulte Também  
 [Criar e executar uma relação de sincronização de entidade &#40;Master Data Services&#41;](../master-data-services/create-and-execute-an-entity-sync-relationship-master-data-services.md)   
 [Relação de sincronização de entidade &#40;Master Data Services&#41;](../master-data-services/entity-sync-relationship-master-data-services.md)  
  
  
