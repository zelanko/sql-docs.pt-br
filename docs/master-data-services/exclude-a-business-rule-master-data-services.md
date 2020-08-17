---
description: Apagar uma regra de negócio (Master Data Services)
title: Apagar uma regra de negócio
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- business rules [Master Data Services], excluding
ms.assetid: bdbc9df0-23f7-40b9-8aba-4445c1482580
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: bc69a5cfcd36e96ed6bc0778c72e6a3a09e6fb23
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88388952"
---
# <a name="exclude-a-business-rule-master-data-services"></a>Apagar uma regra de negócio (Master Data Services)

[!INCLUDE [SQL Server - Windows only ASDBMI  ](../includes/applies-to-version/sql-windows-only-asdbmi.md)]

  No [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], exclua uma regra de negócio quando não desejar removê-la permanentemente, nem validar dados em relação a ela.  
  
## <a name="prerequisites"></a>Pré-requisitos  
 Para executar esse procedimento:  
  
-   Você deve ter permissão para acessar a área funcional **Administração do sistema** .  
  
-   Você deve ser um administrador de modelo. Para obter mais informações, consulte [administradores &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md).  
  
### <a name="to-exclude-a-business-rule"></a>Para excluir uma regra de negócios  
  
1.  No [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)], clique em **Administração do Sistema**.  
  
2.  Na barra de menus, aponte para **Gerenciar** e clique em **Regras de Negócios**.  
  
3.  Na página **regras de negócio** , na lista suspensa **modelo** , selecione um modelo.  
  
4.  Na lista suspensa **Entidade** , escolha uma entidade.  
  
5.  Na lista suspensa **Tipos de Membro** , escolha um tipo de membro.  
  
6.  Na grade, selecione a linha da regra de negócio que deseja excluir e clique em **Editar**.  
  
7.  Marque a caixa de seleção **Excluído** .  
  
8.  Clique em **Save** (Salvar).  
  
9. Clique em **Publicar Tudo**.  
  
10. Na caixa de diálogo de confirmação, clique em **OK**. O valor na coluna **Status da Regra de Negócio** é **Excluído** e a coluna **Excluído** é **Sim**.  
  
## <a name="see-also"></a>Consulte Também  
 [Excluir uma regra de negócio &#40;Master Data Services&#41;](../master-data-services/delete-a-business-rule-master-data-services.md)   
 [Criar e publicar uma regra de negócio &#40;Master Data Services&#41;](../master-data-services/create-and-publish-a-business-rule-master-data-services.md)   
 [Regras de negócio &#40;Master Data Services&#41;](../master-data-services/business-rules-master-data-services.md)  
  
  
