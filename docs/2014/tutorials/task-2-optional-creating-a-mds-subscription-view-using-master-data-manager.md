---
title: 'Tarefa 2 (opcional): Criando uma exibição de assinatura do MDS usando o Master Data Manager | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- data-quality-services
- integration-services
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: f3da8219-e0cb-4848-95ca-285a76ec1ba9
caps.latest.revision: 6
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: b1245beb168f2781e5acca344eb412bde104e4c9
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37284242"
---
# <a name="task-2-optional-creating-a-mds-subscription-view-using-master-data-manager"></a>Tarefa 2 (opcional): Criando uma exibição de assinatura do MDS usando o Master Data Manager
  Nesta tarefa, você criará uma exibição de assinatura para expor a **Supplier** entidade na **fornecedores** modelo para outros aplicativos. Você não utiliza essa exibição na versão atual do tutorial.  
  
1.  Alterne para a página principal do **Master Data Manager** ([http://localhost/MDS](http://localhost/MDS)), clicando em **SQL Server 2012 Master Data Services** na parte superior.  
  
2.  Clique em **gerenciamento de integração**.  
  
3.  Clique em **criar exibições** na barra de menus.  
  
     ![Adicionar um novo botão de modo de exibição de assinatura](../../2014/tutorials/media/et-creatingamdssubscriptionviewusingmdm-01.jpg "adicionar um novo botão de modo de exibição de assinatura")  
  
4.  Clique em **+ (adição)** ícone na barra de ferramentas para criar uma exibição de assinatura.  
  
5.  No **criar exibição de assinatura** painel, digite **fornecedores** para **nome de exibição de assinatura**.  
  
6.  Selecione **Fornecedores** como **Modelo**.  
  
7.  Selecione **VERSION_1** como **Versão**.  
  
8.  Selecione **Supplier** para **entidade**.  
  
9. Selecione **membros folha** para **formato**.  
  
     ![Salve o botão de modo de exibição de assinatura](../../2014/tutorials/media/et-creatingamdssubscriptionviewusingmdm-02.jpg "Salvar botão de modo de exibição de assinatura")  
  
10. Clique em **salvar** na barra de ferramentas para salvar a exibição de assinatura. Essa ação cria um modo de exibição no SQL Server denominada **fornecedores**. Você pode verificar isso usando o SQL Server Management Studio (SSMS).  
  
## <a name="next-step"></a>Próxima etapa  
 [Tarefa 3 &#40;opcional&#41;: examinando exibições de assinatura](task-3-optional-reviewing-the-subscription-views.md)  
  
  
