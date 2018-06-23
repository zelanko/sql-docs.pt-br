---
title: 'Tarefa 5: Criando um atributo baseado em domínio do Excel | Microsoft Docs'
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
ms.topic: article
ms.assetid: 07cbc624-2c6b-4568-96e4-f18663a05d80
caps.latest.revision: 6
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 5e7a8dda16d8f513b2c4b07b9f41712be806b8a9
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36115331"
---
# <a name="task-5-creating-a-domain-based-attribute-from-excel"></a>Tarefa 5: Criando um atributo baseado em domínio no Excel
  Nesta tarefa, você deve converter o **estado** atributo do **Supplier** entidade como um **atributo baseado em domínio**. Depois de configurar o atributo de estado para ser baseado em domínio e publicá-lo no MDS, uma nova entidade chamada **estado** será criado no servidor MDS com todos os valores na coluna e o **estado** atributo das **Supplier** entidade será preenchida com valores da **estado** entidade. Agora, o **fornecedores** modelo deve ter duas entidades: **Supplier** e **estado** onde o **estado** atributo do  **Fornecedor** entidade é um atributo baseado em domínio que depende de **estado** entidade.  
  
1.  Alternar para **Excel** janela tem **Cleansed and Matched Suppliers.xlsx** abrir.  
  
2.  Clique em **atualização** botão na faixa de opções para obter as atualizações mais recentes do MDS. Você deve ver os outros dois registros se você realizou opcional **tarefa 4**.  
  
3.  Clique em nome da coluna **estado** (célula **I1**) no **linha de cabeçalho**.  
  
     ![Excel - botão de propriedades de atributo](../../2014/tutorials/media/et-creatingadomainbasedattributefromexcel-01.jpg "Excel - botão de propriedades de atributo")  
  
4.  Clique em **propriedades de atributo** na faixa de opções.  
  
5.  No **propriedades de atributo** caixa de diálogo, selecione **lista restrita (baseada em domínio)** para o **tipo de atributo**.  
  
6.  Tipo **estado** para o **novo nome da entidade** e clique em **Okey**.  
  
     ![Excel - caixa de diálogo de propriedades de atributo](../../2014/tutorials/media/et-creatingadomainbasedattributefromexcel-02.jpg "Excel - caixa de diálogo de propriedades de atributo")  
  
7.  Agora, no Excel, você deve ver **a seta para baixo** quando você clica em qualquer valor de **estado** coluna. Você poderá alterar o valor usando a lista suspensa se necessário.  
  
     ![Excel - lista com os estados suspensa](../../2014/tutorials/media/et-creatingadomainbasedattributefromexcel-03.jpg "Excel - lista com os estados suspensa")  
  
## <a name="next-step"></a>Próxima etapa  
 [Tarefa 6: Verificar se o atributo baseado em domínio foi criado usando o Master Data Manager](../../2014/tutorials/task-6-verify-domain-based-attribute-master-data-manager.md)  
  
  