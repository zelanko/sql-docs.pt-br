---
description: Criar uma hierarquia explícita (Master Data Services)
title: Criar uma hierarquia explícita
ms.custom: ''
ms.date: 04/01/2016
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- creating explicit hierarchies [Master Data Services]
- explicit hierarchies, creating
ms.assetid: ba768393-6990-4eda-8cb0-d58cb3cfc2e2
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 8512e53686d747fedb8ac5158a388e48b38469e1
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88461803"
---
# <a name="create-an-explicit-hierarchy-master-data-services"></a>Criar uma hierarquia explícita (Master Data Services)

[!INCLUDE [SQL Server - Windows only ASDBMI  ](../includes/applies-to-version/sql-windows-only-asdbmi.md)]

  No [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], crie uma hierarquia explícita quando precisar de uma hierarquia desbalanceada em que os membros podem existir em qualquer nível. As hierarquias explícitas contêm membros de uma única entidade.  
  
 Depois que você criar uma hierarquia explícita, pode adicionar os membros a ela na área funcional do **Gerenciador** .  
  
## <a name="prerequisites"></a>Pré-requisitos  
 Para executar esse procedimento:  
  
-   Você deve ter permissão para acessar a área funcional **Administração do sistema** .  
  
-   Você deve ser um administrador de modelo. Para obter mais informações, consulte [administradores &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md).  
  
-   A entidade deve estar habilitada para hierarquias explícitas e coleções.  
  
### <a name="to-create-an-explicit-hierarchy"></a>Para criar uma hierarquia explícita  
  
1.  No [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)], clique em **Administração do Sistema**.  
  
2.  Na página **gerenciar modelo** , selecione um modelo na grade e clique em **entidades**.  
  
3.  Na página **Gerenciar Entidade** , na grade, selecione a linha para a entidade para a qual você deseja criar uma hierarquia explícita.  
  
4.  Clique em **hierarquias explícitas**.  
  
5.  Na página **Gerenciar Hierarquia Explícita** , clique em **Adicionar**.  
  
6.  Na caixa **Nome** , digite um nome para a hierarquia.  
  
7.  Opcionalmente, desmarque a caixa de seleção **Hierarquia obrigatória** para criar a hierarquia como não obrigatória. Para obter mais informações sobre tipos de hierarquia, consulte [Hierarquias explícitas &#40;Master Data Services&#41;](../master-data-services/explicit-hierarchies-master-data-services.md).  
  
8.  Clique em **Save** (Salvar).  
  
## <a name="grid-columns"></a>Colunas da grade  
 Para cada hierarquia explícita que você criar, uma linha com sete colunas será adicionada à grade. A seguir está uma descrição das colunas.  
  
|Nome|Descrição|  
|----------|-----------------|  
|Status|O status da entidade. Quando você clica em **Salvar** , a imagem a seguir é exibida, indicando que a entidade está atualizando.<br /><br /> ![Ícone para atualizar o status](../master-data-services/media/mds-statusicon-updating.png "Ícone para atualizar o status")<br /><br /> Se houver erros ao criar ou editar uma entidade, a imagem a seguir será exibida.<br /><br /> ![Ícone para status de erro](../master-data-services/media/mds-statusicon-error.png "Ícone para status de erro")<br /><br /> Se o status for OK, a imagem a seguir será exibida.<br /><br /> ![Ícone para status OK](../master-data-services/media/mds-statusicon-ok.png "Ícone para status OK")|  
|Nome|O nome da hierarquia explícita.|  
|É obrigatório|Especifica se a hierarquia explícita é obrigatória.|  
|Criado por|O nome do usuário que criou a hierarquia explícita.|  
|Criado em|A data e a hora de criação da hierarquia explícita.|  
|Atualizado por|O nome de usuário do último usuário que atualizou a hierarquia explícita.|  
|Atualizado Em|A data e a hora da última atualização da hierarquia explícita.|  
  
## <a name="next-steps"></a>Próximas etapas  
  
-   [Criar um membro consolidado &#40;Master Data Services&#41;](../master-data-services/create-a-consolidated-member-master-data-services.md)  
  
  
  
## <a name="see-also"></a>Consulte Também  
 [Hierarquias explícitas &#40;Master Data Services&#41;](../master-data-services/explicit-hierarchies-master-data-services.md)   
 [Hierarquias derivadas com limites explícitos &#40;Master Data Services&#41;](../master-data-services/derived-hierarchies-with-explicit-caps-master-data-services.md)   
 [Alterar o nome de uma hierarquia explícita &#40;Master Data Services&#41;](../master-data-services/change-an-explicit-hierarchy-name-master-data-services.md)  
  
  

