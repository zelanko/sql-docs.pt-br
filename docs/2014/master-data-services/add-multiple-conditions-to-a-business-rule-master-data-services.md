---
title: Adicionar várias condições a uma regra de negócios (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- business rules [Master Data Services], multiple conditions
ms.assetid: 5f0f6958-6cf2-444b-bdcd-05b887637a0b
caps.latest.revision: 6
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: f7994861c246b31731dbff82069eed091379ad6a
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37275172"
---
# <a name="add-multiple-conditions-to-a-business-rule-master-data-services"></a>Adicionar várias condições a uma regra de negócio (Master Data Services)
  No [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], adicione várias condições **AND** ou **OR** a uma regra de negócio quando desejar uma regra mais complexa.  
  
> [!NOTE]  
>  Se você criar uma regra de negócio que usa o operador **OR** , considere a criação de uma regra separada para cada instrução condicional que possa ser avaliada independentemente. É possível excluir regras conforme necessário, para garantir mais flexibilidade e uma solução de problemas mais fácil.  
  
## <a name="prerequisites"></a>Prerequisites  
 Para executar esse procedimento:  
  
-   Você deve ter permissão para acessar a área funcional **Administração do Sistema** .  
  
-   Você deve ser um administrador de modelo. Para obter mais informações, veja [Administrators &#40;Master Data Services&#41;](administrators-master-data-services.md).  
  
-   Uma regra de negócios deve existir. Para obter mais informações, consulte [Criar e publicar uma regra de negócio &#40;Master Data Services&#41;](../../2014/master-data-services/create-and-publish-a-business-rule-master-data-services.md).  
  
### <a name="to-add-multiple-conditions-to-a-business-rule"></a>Para acrescentar várias condições a uma regra de negócio  
  
1.  No [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)], clique em **Administração do Sistema**.  
  
2.  Na barra de menus, aponte para **Gerenciar** e clique em **Regras de Negócios**.  
  
3.  Na página **Manutenção de Regra de Negócio** , na lista **Modelo** , selecione um modelo.  
  
4.  Na lista **Entidade** , selecione uma entidade.  
  
5.  Dos **tipo de membro** , selecione um tipo de membro.  
  
6.  Na lista **Atributo** , selecione um atributo ou deixe o valor padrão **Todos**.  
  
7.  Clique na linha da regra de negócio que deseja editar.  
  
8.  Clique em **Editar regra de negócio selecionada**.  
  
9. No **componentes** painel, expanda o **operadores lógicos** nó.  
  
10. Clique em **AND** ou **OR** e arraste-o para o **IF** do painel **AND** rótulo.  
  
11. No painel **Componentes** , expanda o nó **Condições** .  
  
12. Clique em uma condição e arraste-o para **IF** painel, para o **AND** ou **OR** rótulo da etapa 10.  
  
13. No **atributos** painel, clique em um atributo e arraste-o para o **Editar condição** do painel **Selecionar atributo** rótulo.  
  
14. No **Editar condição** painel, preencha os campos necessários.  
  
15. No painel **Editar Condição** , clique em **Salvar item**.  
  
16. Opcionalmente, para adicionar mais condições, a partir de **componentes** painel, arraste **AND** ou **OR** a qualquer **AND** ou **OR**no **IF** painel. Então siga as etapas 13 a 15.  
  
    > [!TIP]  
    >  Para excluir uma condição, clique no nome da condição e, além de **Editar condição** painel, clique em **para excluir um item**.  
  
## <a name="see-also"></a>Consulte também  
 [Regras de negócio &#40;Master Data Services&#41;](../../2014/master-data-services/business-rules-master-data-services.md)   
 [Alterar o nome de uma regra de negócios &#40;Master Data Services&#41;](../../2014/master-data-services/change-a-business-rule-name-master-data-services.md)   
 [Configurar regras de negócio para enviar notificações &#40;Master Data Services&#41;](../../2014/master-data-services/configure-business-rules-to-send-notifications-master-data-services.md)  
  
  
