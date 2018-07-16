---
title: 'Tarefa 6: Verifique se o atributo baseado em domínio é criado usando o Master Data Manager | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- data-quality-services
- integration-services
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 6e90517a-910c-4c33-8f11-92ac3cff4fdc
caps.latest.revision: 6
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: f607a6faaf8a6891ff2d7191142f11dbaa55f961
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37191296"
---
# <a name="task-6-verify-that-the-domain-based-attribute-is-created-using-master-data-manager"></a>Tarefa 6: Verificar se o atributo baseado em domínio foi criado usando o Master Data Manager
  Nesta tarefa, verifique se a entidade **State** foi criada no **MDS** e o atributo **State** da entidade **Supplier** é um atributo baseado em domínio que depende da entidade **State** usando o **Master Data Manager**.  
  
1.  Alterne para o aplicativo Web **Master Data Manager**.  
  
2.  Clique em **SQL Server 2012 Master Data Services** na parte superior para acessar a home page.  
  
3.  Verifique se o modelo **Fornecedores** está selecionado e clique em **Gerenciador**. Você poderia atualizar a página se o **Gerenciador** já estivesse aberto.  
  
4.  Passe o mouse sobre **Entidades** na barra de menus e observe que agora há duas entidades: **Supplier** e **State**.  
  
     ![Menu entidades com estado e fornecedor](../../2014/tutorials/media/et-verifythatthedbaiscreatedusingmdm-01.jpg "Menu entidades com estado e fornecedor")  
  
5.  Clique em **State** se a entidade ainda não estiver aberta.  
  
6.  Selecione **GA** na lista.  
  
7.  No painel **Detalhes** à direita, altere o **Nome** para **Geórgia** no **painel à direita** e clique em **OK**.  
  
8.  Repita as etapas anteriores para outros estados.  
  
    |Código|Nome|  
    |----------|----------|  
    |CA|Califórnia|  
    |CO|Colorado|  
    |IL|Illinois|  
    |DC|District of Columbia|  
    |FL|Florida|  
    |AL|Alabama|  
    |KY|Kentucky|  
    |MA|Massachusetts|  
    |AZ|Arizona|  
    |MI|Michigan|  
    |MN|Minnesota|  
    |NJ|New Jersey|  
    |NV|Nevada|  
    |NY|New York|  
    |OH|Ohio|  
    |OK|Oklahoma|  
    |OU|Oregon|  
    |PA|Pensilvânia|  
    |SC|South Carolina|  
    |KS|Kansas|  
    |TN|Tennessee|  
    |TX|Texas|  
    |UT|Utah|  
    |VA|Virginia|  
    |WA|Washington|  
    |WI|Wisconsin|  
    |HI|Hawaii|  
    |MD|Maryland|  
    |CT|Connecticut|  
  
9. Selecione qualquer uma das entradas de estado e clique em **Exibir Transações** na barra de ferramentas. Você deverá visualizar a transação da atualização que acabou de fazer na lista de transações.  
  
10. Passe o mouse sobre o menu **Entidades** e clique em **Fornecedor**.  
  
11. Agora, observe que um valor para o campo **Estado** pode ser alterado no painel **Detalhes** usando a lista suspensa. Você também pode observar que, na lista à esquerda e na lista suspensa no painel **Detalhes**, o código será exibido primeiro e depois o nome entre chaves. Também é possível alterar qualquer outro valor no painel **Detalhes**.  
  
     ![Atributo com o código atualizado e nomes de estado](../../2014/tutorials/media/et-verifythatthedbaiscreatedusingmdm-02.jpg "atributo com o código atualizado e nomes de estado")  
  
## <a name="next-step"></a>Próxima etapa  
 [Tarefa 7: Exibindo as atualizações feitas usando o Master Data Manager no Excel](../../2014/tutorials/task-7-viewing-updates-made-using-master-data-manager-in-excel.md)  
  
  
