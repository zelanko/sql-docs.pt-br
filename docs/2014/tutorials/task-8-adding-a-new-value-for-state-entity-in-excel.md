---
title: 'Tarefa 8: adicionando um novo valor para a entidade de estado no Excel | Microsoft Docs'
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: a763d76b-06a3-4d51-9614-01fc9fb1c158
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: f12a387a7c7b5ed60ca87159628aab989d37c953
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85006432"
---
# <a name="task-8-adding-a-new-value-for-state-entity-in-excel"></a>Tarefa 8: Adicionando um novo valor à entidade State do Excel
  Nesta tarefa, você adicionará um valor para a entidade State no Excel e publicará a alteração no servidor MDS.  
  
1.  Adicione uma **folha de trabalho** no Excel clicando na guia novo na parte inferior.  
  
     ![Excel - Nova guia Pasta de Trabalho](../../2014/tutorials/media/et-addinganewvalueforstateentityinexcel-01.jpg "Excel - Nova guia Pasta de Trabalho")  
  
2.  No **Excel**, clique na guia **dados mestres** no menu e, em seguida, clique em **Mostrar Explorer** na faixa de faixas.  
  
3.  No **Data Explorer mestre**, selecione **fornecedores** para **modelo**. Você deve ver duas entidades: **fornecedor** e **estado** na lista de entidades.  
  
4.  Clique duas vezes em **estado** na lista. Todos os membros da entidade de **estado** do MDS devem ser exibidos na planilha.  
  
5.  Agora, adicione uma linha no final com os seguintes valores: **Carolina do Norte** para **nome** e **NC** para **código**. A codificação por cores diferencia qualquer registro novo/atualizado dos outros registros.  
  
     ![Excel - Adicionar Carolina do Norte a Estados](../../2014/tutorials/media/et-addinganewvalueforstateentityinexcel-02.jpg "Excel - Adicionar Carolina do Norte a Estados")  
  
6.  Clique em **publicar** na faixa de faixas para publicar a alteração no MDS.  
  
     ![Excel - Botão Publicar na guia Dados Mestre](../../2014/tutorials/media/et-addinganewvalueforstateentityinexcel-03.jpg "Excel - Botão Publicar na guia Dados Mestre")  
  
7.  Na caixa de diálogo **publicar e anotar** , observe que o **uso da mesma anotação para todas as alterações** está selecionado. Você pode inserir uma anotação única de todas as alterações aqui.  
  
8.  Selecione a opção **revisar alterações e fornecer anotações individualmente** para fornecer anotação para cada alteração (neste caso, apenas uma).  
  
     ![Excel - Caixa de diálogo Publicar e Anotar](../../2014/tutorials/media/et-addinganewvalueforstateentityinexcel-04.jpg "Excel - Caixa de diálogo Publicar e Anotar")  
  
9. Clique em **publicar** para publicar dados no MDS.  
  
10. Observe que a **codificação por cores** para a linha com a Carolina do **norte** como o **estado** é igual a outros registros agora.  
  
11. **Opcional:** Verifique se o novo membro (NC) foi adicionado à entidade de **estado** usando o **Gerenciador** no **Master Data Manager**.  
  
12. No Excel, clique com o botão direito do mouse na planilha de **estado** na parte inferior e clique em **excluir** para excluir a planilha. Excluir a planilha não exclui os dados do servidor MDS.  
  
## <a name="next-step"></a>Próxima etapa  
 [Tarefa 9: Criando uma hierarquia derivada usando o Master Data Manager](../../2014/tutorials/task-9-creating-a-derived-hierarchy-using-master-data-manager.md)  
  
  
