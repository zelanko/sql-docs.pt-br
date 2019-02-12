---
title: 'Tarefa 2 (opcional): Criando uma exibição de assinatura do MDS usando o Master Data Manager | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: f3da8219-e0cb-4848-95ca-285a76ec1ba9
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: 4596485b4eebeba66028d03f5a54b3ee2461205b
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/11/2019
ms.locfileid: "56015277"
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
 [Tarefa 3 &#40;opcional&#41;: Examinando exibições de assinatura](task-3-optional-reviewing-the-subscription-views.md)  
  
  
