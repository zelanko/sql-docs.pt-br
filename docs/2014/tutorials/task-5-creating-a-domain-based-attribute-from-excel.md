---
title: 'Tarefa 5: Criando um atributo baseado em domínio do Excel | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 07cbc624-2c6b-4568-96e4-f18663a05d80
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 6f7287091ddd64ef9df1c63706a2f562feed4a5d
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "84999670"
---
# <a name="task-5-creating-a-domain-based-attribute-from-excel"></a>Tarefa 5: Criando um atributo baseado em domínio no Excel
  Nesta tarefa, você converte o atributo de **estado** da entidade **Supplier** como um **atributo baseado em domínio**. Depois de configurar o atributo de estado para ser um baseado em domínio e publicá-lo no MDS, uma nova entidade chamada **State** será criada no servidor MDS com todos os valores na coluna e o atributo **State** da entidade **Supplier** será populado com valores da entidade **State** . Agora, o modelo **suppliers** deve ter duas entidades: **Supplier** e **State** , em que o atributo **State** da entidade **Supplier** é um atributo baseado em domínio que depende da entidade **State** .  
  
1.  Alternar para a janela do **Excel** que foi **limpa e correspondente Suppliers.xlsx** aberto.  
  
2.  Clique no botão **Atualizar** na faixa de faixas para obter as atualizações mais recentes do MDS. Você deverá ver os mais dois registros se tiver executado a **tarefa 4**opcional.  
  
3.  Clique em **estado** do nome da coluna (célula **i1**) na **linha de cabeçalho**.  
  
     ![Excel - Botão Propriedades de Atributo](../../2014/tutorials/media/et-creatingadomainbasedattributefromexcel-01.jpg "Excel - Botão Propriedades de Atributo")  
  
4.  Clique em **Propriedades do atributo** na faixa de faixas.  
  
5.  Na caixa de diálogo **Propriedades do atributo** , selecione **lista restrita (baseada em domínio)** para o **tipo de atributo**.  
  
6.  Digite **estado** para o **novo nome de entidade** e clique em **OK**.  
  
     ![Excel - Caixa de diálogo Propriedades de Atributo](../../2014/tutorials/media/et-creatingadomainbasedattributefromexcel-02.jpg "Excel - Caixa de diálogo Propriedades de Atributo")  
  
7.  Agora, no Excel, você deve ver a **seta para baixo** ao clicar em qualquer valor na coluna **estado** . Você poderá alterar o valor usando a lista suspensa se necessário.  
  
     ![Excel - Lista suspensa com estados](../../2014/tutorials/media/et-creatingadomainbasedattributefromexcel-03.jpg "Excel - Lista suspensa com estados")  
  
## <a name="next-step"></a>Próxima etapa  
 [Tarefa 6: Verificar se o atributo baseado em domínio foi criado usando o Master Data Manager](../../2014/tutorials/task-6-verify-domain-based-attribute-master-data-manager.md)  
  
  
