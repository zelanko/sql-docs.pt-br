---
title: 'Tarefa 2 (opcional): criando uma exibição de assinatura do MDS usando Master Data Manager | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: f3da8219-e0cb-4848-95ca-285a76ec1ba9
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: cc923792adc3fefb5ebaab9e225169648394c71f
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81484706"
---
# <a name="task-2-optional-creating-a-mds-subscription-view-using-master-data-manager"></a>Tarefa 2 (opcional): Criando uma exibição de assinatura do MDS usando o Master Data Manager
  Nesta tarefa, você cria uma exibição de assinatura para expor a entidade **Supplier** no modelo **suppliers** para outros aplicativos. Você não utiliza essa exibição na versão atual do tutorial.  
  
1.  Alterne para a página principal do **Master Data Manager** (`http://localhost/MDS`) clicando em **SQL Server 2012 Master Data Services** na parte superior.  
  
2.  Clique em **Gerenciamento de integração**.  
  
3.  Clique em **criar modos de exibição** na barra de menus.  
  
     ![Botão Adicionar uma Nova Exibição de Assinatura](../../2014/tutorials/media/et-creatingamdssubscriptionviewusingmdm-01.jpg "Botão Adicionar uma Nova Exibição de Assinatura")  
  
4.  Clique no ícone **+ (mais)** na barra de ferramentas para criar uma exibição de assinatura.  
  
5.  No painel **criar exibição de assinatura** , digite **fornecedores** para **nome de exibição de assinatura**.  
  
6.  Selecione **Fornecedores** como **Modelo**.  
  
7.  Selecione **VERSION_1** como **Versão**.  
  
8.  Selecione **fornecedor** para **entidade**.  
  
9. Selecione **membros folha** para o **formato**.  
  
     ![Botão Salvar Exibição de Assinatura](../../2014/tutorials/media/et-creatingamdssubscriptionviewusingmdm-02.jpg "Botão Salvar Exibição de Assinatura")  
  
10. Clique em **salvar** na barra de ferramentas para salvar a exibição de assinatura. Essa ação cria uma exibição em SQL Server **fornecedores**nomeados. Você pode verificar isso usando o SQL Server Management Studio (SSMS).  
  
## <a name="next-step"></a>Próxima etapa  
 [Tarefa 3 &#40;&#41; opcional: revisando as exibições de assinatura](task-3-optional-reviewing-the-subscription-views.md)  
  
  
