---
title: 'Tarefa 5: Criando um atributo baseado em domínio no Excel | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 07cbc624-2c6b-4568-96e4-f18663a05d80
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: 1a2826bb0c9b542837e05b7f600c9ce7d934fd4e
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/11/2019
ms.locfileid: "56031597"
---
# <a name="task-5-creating-a-domain-based-attribute-from-excel"></a>Tarefa 5: Criando um atributo baseado em domínio com base no Excel
  Nesta tarefa, você deve converter o **estado** atributo da **Supplier** entidade como um **atributo baseado em domínio**. Depois de configurar o atributo de estado para ser um baseado em domínio e publicá-lo no MDS, uma nova entidade chamada **estado** será criado no servidor MDS com todos os valores na coluna e o **estado** atributo das **Supplier** será preenchida com valores da entidade a **estado** entidade. Agora, o **fornecedores** modelo deverá ter duas entidades: **Supplier** e **estado** onde a **estado** atributo do **Supplier** entidade é um atributo baseado em domínio que depende de **estado** entidade.  
  
1.  Alterne para **Excel** janela que tem **Cleansed and Matched Suppliers** abrir.  
  
2.  Clique em **Refresh** botão na faixa de opções para obter as atualizações mais recentes do MDS. Você deve ver os outros dois registros se você tiver executado opcional **tarefa 4**.  
  
3.  Clique em nome da coluna **estado** (célula **I1**) na **linha de cabeçalho**.  
  
     ![Excel - botão de propriedades de atributo](../../2014/tutorials/media/et-creatingadomainbasedattributefromexcel-01.jpg "Excel - botão de propriedades de atributo")  
  
4.  Clique em **propriedades de atributo** na faixa de opções.  
  
5.  No **propriedades do atributo** caixa de diálogo, selecione **lista restrita (baseada em domínio)** para o **tipo de atributo**.  
  
6.  Tipo de **estado** para o **nome da nova entidade** e clique em **Okey**.  
  
     ![Excel - caixa de diálogo de propriedades de atributo](../../2014/tutorials/media/et-creatingadomainbasedattributefromexcel-02.jpg "Excel - caixa de diálogo de propriedades de atributo")  
  
7.  Agora, no Excel, você deverá ver **seta para baixo** quando você clica em qualquer valor na **estado** coluna. Você poderá alterar o valor usando a lista suspensa se necessário.  
  
     ![Excel - lista suspensa lista com os estados](../../2014/tutorials/media/et-creatingadomainbasedattributefromexcel-03.jpg "Excel - lista suspensa lista com os estados")  
  
## <a name="next-step"></a>Próxima etapa  
 [Tarefa 6: Verifique se o atributo baseado em domínio é criado usando o Master Data Manager](../../2014/tutorials/task-6-verify-domain-based-attribute-master-data-manager.md)  
  
  
