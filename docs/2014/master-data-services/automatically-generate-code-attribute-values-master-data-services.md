---
title: Gerar automaticamente valores de atributo de código (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 19b354ee-2906-4cc7-ba2f-32b4543bddcf
caps.latest.revision: 3
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: a8cfcda0d6fc37db1b620fd64c044e322f81877e
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36116619"
---
# <a name="automatically-generate-code-attribute-values-master-data-services"></a>Gerar automaticamente valores de atributo de código (Master Data Services)
  No [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], gera automaticamente valores para o atributo Code de uma entidade quando você deseja atribuir um inteiro automaticamente ao valor de código toda vez que um novo membro é criado.  
  
## <a name="prerequisites"></a>Prerequisites  
 Para executar esse procedimento:  
  
-   Você deve ter permissão para acessar a área funcional **Administração do Sistema** .  
  
-   Você deve ser um administrador de modelo. Para obter mais informações, veja [Administrators &#40;Master Data Services&#41;](administrators-master-data-services.md).  
  
-   A entidade deve existir. Para obter mais informações, consulte [Criar uma entidade &#40;Master Data Services&#41;](../../2014/master-data-services/create-an-entity-master-data-services.md).  
  
### <a name="to-automatically-generate-code-values"></a>Para gerar valores de código automaticamente.  
  
1.  No [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)], clique em **Administração do Sistema**.  
  
2.  Sobre o **Gerenciador de modelos** página, na barra de menus, aponte para **gerenciar** e clique em **entidades**.  
  
3.  Na página **Manutenção da Entidade** , na lista **Modelo** , selecione um modelo.  
  
4.  Selecione a linha da entidade para a qual você deseja gerar códigos.  
  
5.  Clique em **Editar entidade selecionada**.  
  
6.  Marque a caixa de seleção **Criar valores de códigos automaticamente** .  
  
7.  Na caixa **Iniciar com** , digite um número para começar a incrementar. Se os membros já existirem, o Código será definido com base no valor existente mais alto. Por exemplo, se o valor de código existente mais alto for 299, o valor de código do próximo membro será definido como 300.  
  
8.  Clique em **Salvar entidade**.  
  
## <a name="see-also"></a>Consulte também  
 [Criação automática de código &#40;Master Data Services&#41;](../../2014/master-data-services/automatic-code-creation-master-data-services.md)   
 [Gerar automaticamente valores de atributo que não sejam código &#40;Master Data Services&#41;](../../2014/master-data-services/automatically-generate-attribute-values-other-than-code-master-data-services.md)  
  
  