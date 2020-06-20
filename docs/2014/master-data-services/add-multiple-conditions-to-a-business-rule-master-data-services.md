---
title: Adicionar várias condições a uma regra de negócios (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- business rules [Master Data Services], multiple conditions
ms.assetid: 5f0f6958-6cf2-444b-bdcd-05b887637a0b
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: bf135e4c1f67a7187ec67284d52adcdb25c9bd27
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84972276"
---
# <a name="add-multiple-conditions-to-a-business-rule-master-data-services"></a>Adicionar várias condições a uma regra de negócio (Master Data Services)
  No [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], adicione várias condições **AND** ou **OR** a uma regra de negócio quando desejar uma regra mais complexa.  
  
> [!NOTE]  
>  Se você criar uma regra de negócio que usa o operador **OR** , considere a criação de uma regra separada para cada instrução condicional que possa ser avaliada independentemente. É possível excluir regras conforme necessário, para garantir mais flexibilidade e uma solução de problemas mais fácil.  
  
## <a name="prerequisites"></a>Pré-requisitos  
 Para executar esse procedimento:  
  
-   Você deve ter permissão para acessar a área funcional **Administração do sistema** .  
  
-   Você deve ser um administrador de modelo. Para obter mais informações, consulte [administradores &#40;Master Data Services&#41;](administrators-master-data-services.md).  
  
-   Uma regra de negócios deve existir. Para obter mais informações, consulte [Criar e publicar uma regra de negócio &#40;Master Data Services&#41;](../../2014/master-data-services/create-and-publish-a-business-rule-master-data-services.md).  
  
### <a name="to-add-multiple-conditions-to-a-business-rule"></a>Para acrescentar várias condições a uma regra de negócio  
  
1.  No [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)], clique em **Administração do Sistema**.  
  
2.  Na barra de menus, aponte para **Gerenciar** e clique em **Regras de Negócios**.  
  
3.  Na página **Manutenção de Regra de Negócio** , na lista **Modelo** , selecione um modelo.  
  
4.  Na lista **Entidade** , selecione uma entidade.  
  
5.  Na lista **tipo de membro** , selecione um tipo de membro.  
  
6.  Na lista **Atributo** , selecione um atributo ou deixe o valor padrão **Todos**.  
  
7.  Clique na linha da regra de negócio que deseja editar.  
  
8.  Clique em **Editar regra de negócio selecionada**.  
  
9. No painel **componentes** , expanda o nó **operadores lógicos** .  
  
10. Clique **AND** em e **ou em e arraste** -o para o painel de **If** **e** o rótulo.  
  
11. No painel **Componentes** , expanda o nó **Condições** .  
  
12. Clique em uma condição e arraste-a para **se** painel, para o **e** ou **ou** para o rótulo da etapa 10.  
  
13. No painel **atributos** , clique em um atributo e arraste-o para o rótulo de **atributo selecionar** do painel de **condição de edição** .  
  
14. No painel **Editar condição** , preencha todos os campos obrigatórios.  
  
15. No painel **Editar Condição** , clique em **Salvar item**.  
  
16. Opcionalmente, para adicionar mais condições, no painel **componentes** , arraste **e** ou **ou** para qualquer **e** **ou ou no painel** **If** . Então siga as etapas 13 a 15.  
  
    > [!TIP]  
    >  Para excluir uma condição, clique no nome da condição e, no painel **Editar condição** , clique em **Excluir item**.  
  
## <a name="see-also"></a>Consulte Também  
 [Regras de negócio &#40;Master Data Services&#41;](../../2014/master-data-services/business-rules-master-data-services.md)   
 [Alterar o nome de uma regra de negócio &#40;Master Data Services&#41;](../../2014/master-data-services/change-a-business-rule-name-master-data-services.md)   
 [Configurar regras de negócio para enviar notificações &#40;Master Data Services&#41;](../../2014/master-data-services/configure-business-rules-to-send-notifications-master-data-services.md)  
  
  
