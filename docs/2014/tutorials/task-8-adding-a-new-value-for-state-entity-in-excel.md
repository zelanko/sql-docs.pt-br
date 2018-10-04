---
title: 'Tarefa 8: Adicionando um novo valor à entidade State do Excel | Microsoft Docs'
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- data-quality-services
- integration-services
- master-data-services
ms.topic: conceptual
ms.assetid: a763d76b-06a3-4d51-9614-01fc9fb1c158
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 04fe6fa0a9036ca3835fd4bc0afcb0e35854fd85
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48222147"
---
# <a name="task-8-adding-a-new-value-for-state-entity-in-excel"></a>Tarefa 8: Adicionando um novo valor à entidade State do Excel
  Nesta tarefa, você adicionará um valor para a entidade State no Excel e publicará a alteração no servidor MDS.  
  
1.  Adicionar um **folha de trabalho** no Excel clicando na nova guia na parte inferior.  
  
     ![Excel - nova guia de planilha](../../2014/tutorials/media/et-addinganewvalueforstateentityinexcel-01.jpg "Excel - nova guia de planilha")  
  
2.  Na **Excel**, clique no **dados mestres** guia no menu e, em seguida, clique em **Mostrar Gerenciador** na faixa de opções.  
  
3.  No **Master Data Explorer**, selecione **fornecedores** para **modelo**. Você deve ver duas entidades: **Supplier** e **estado** na lista de entidades.  
  
4.  Clique duas vezes em **estado** na lista. Todos os membros de **estado** entidade do MDS deve ser exibida na planilha.  
  
5.  Agora, adicione uma linha no final com os seguintes valores: **Carolina do Norte** para **nome** e **NC** para **código**. A codificação por cores diferencia qualquer registro novo/atualizado dos outros registros.  
  
     ![Excel - adicionar Carolina do Norte a estados](../../2014/tutorials/media/et-addinganewvalueforstateentityinexcel-02.jpg "Excel - adicionar Carolina do Norte a estados")  
  
6.  Clique em **publicar** na faixa de opções para publicar a alteração no MDS.  
  
     ![Excel - botão Publicar na guia dados mestre](../../2014/tutorials/media/et-addinganewvalueforstateentityinexcel-03.jpg "Excel - botão Publicar na guia dados mestre")  
  
7.  Sobre o **publicar e anotar** caixa de diálogo caixa, observe que o **usar a mesma anotação para todas as alterações** está selecionado. Você pode inserir uma anotação única de todas as alterações aqui.  
  
8.  Selecione **examinar as alterações e fornecer anotações individualmente** opção para fornecer a anotação para cada alteração (nesse caso, apenas um).  
  
     ![Excel - publicar e anotar a caixa de diálogo](../../2014/tutorials/media/et-addinganewvalueforstateentityinexcel-04.jpg "do Excel - publicar e anotar a caixa de diálogo")  
  
9. Clique em **publicar** para publicar dados no MDS.  
  
10. Observe que **codificação de cores** para a linha com **Carolina do Norte** como o **estado** é o mesmo que outros registros agora.  
  
11. **Opcional:** Verifique se o novo membro (NC) é adicionado para o **estado** entidade usando o **Explorer** na **Master Data Manager**.  
  
12. No Excel, clique com botão direito do **estado** planilha na parte inferior e clique em **excluir** para excluir a planilha. Excluir a planilha não exclui os dados do servidor MDS.  
  
## <a name="next-step"></a>Próxima etapa  
 [Tarefa 9: Criando uma hierarquia derivada usando o Master Data Manager](../../2014/tutorials/task-9-creating-a-derived-hierarchy-using-master-data-manager.md)  
  
  
