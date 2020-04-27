---
title: Gerar automaticamente valores de atributo de código (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: 19b354ee-2906-4cc7-ba2f-32b4543bddcf
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 9d6bdaf3e34ab6386cf4270c2610bd7b1a70e668
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "65483618"
---
# <a name="automatically-generate-code-attribute-values-master-data-services"></a>Gerar automaticamente valores de atributo de código (Master Data Services)
  No [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], gera automaticamente valores para o atributo Code de uma entidade quando você deseja atribuir um inteiro automaticamente ao valor de código toda vez que um novo membro é criado.  
  
## <a name="prerequisites"></a>Pré-requisitos  
 Para executar esse procedimento:  
  
-   Você deve ter permissão para acessar a área funcional **Administração do sistema** .  
  
-   Você deve ser um administrador de modelo. Para obter mais informações, consulte [administradores &#40;Master Data Services&#41;](administrators-master-data-services.md).  
  
-   A entidade deve existir. Para obter mais informações, consulte [criar uma entidade &#40;Master Data Services&#41;](../../2014/master-data-services/create-an-entity-master-data-services.md).  
  
### <a name="to-automatically-generate-code-values"></a>Para gerar valores de código automaticamente.  
  
1.  No [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)], clique em **Administração do Sistema**.  
  
2.  Na página **Gerenciador de modelos** , na barra de menus, aponte para **gerenciar** e clique em **entidades**.  
  
3.  Na página **Manutenção da Entidade** , na lista **Modelo** , selecione um modelo.  
  
4.  Selecione a linha da entidade para a qual você deseja gerar códigos.  
  
5.  Clique em **Editar entidade selecionada**.  
  
6.  Marque a caixa de seleção **Criar valores de códigos automaticamente** .  
  
7.  Na caixa **Iniciar com** , digite um número para começar a incrementar. Se os membros já existirem, o Código será definido com base no valor existente mais alto. Por exemplo, se o valor de código existente mais alto for 299, o valor de código do próximo membro será definido como 300.  
  
8.  Clique em **Salvar entidade**.  
  
## <a name="see-also"></a>Consulte Também  
 [Criação de código automática &#40;Master Data Services&#41;](../../2014/master-data-services/automatic-code-creation-master-data-services.md)   
 [Gerar automaticamente valores de atributo diferentes de código &#40;Master Data Services&#41;](../../2014/master-data-services/automatically-generate-attribute-values-other-than-code-master-data-services.md)  
  
  
