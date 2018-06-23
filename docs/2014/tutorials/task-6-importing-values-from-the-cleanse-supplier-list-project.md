---
title: 'Tarefa 6: Importando valores do fornecedor projeto Limpar lista | Microsoft Docs'
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
ms.assetid: fec0deef-a729-4ff1-b709-72d2b3f407ac
caps.latest.revision: 6
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 7a915013d779392d585bd5609384fab7bffd2800
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36009256"
---
# <a name="task-6-importing-values-from-the-cleanse-supplier-list-project"></a>Tarefa 6: Importando valores do projeto Limpar Lista de Fornecedores
  Nesta tarefa, você importará o conhecimento de qualidade de dados adquirido durante o processo de limpeza. Consulte [importar valores de projeto de limpeza para um domínio](http://msdn.microsoft.com/library/hh479581.aspx) tópico para obter mais detalhes. Você também exportar base de conhecimento em um arquivo DQS antes de publicar a atualização **fornecedores** da Base de dados de Conhecimento.  
  
1.  Na página principal do **cliente DQS**, clique em **seta para a direita** lado **fornecedores** em **Bases de conhecimento recente** e clique em **Gerenciamento de domínio**.  
  
2.  Clique em **Contact Email** na lista de domínios e alterne para o **valores de domínio** guia no painel direito.  
  
3.  Clique em **a seta para baixo** lado a **importar valores de** ícone na barra de ferramentas, clique em **importar valores do projeto**.  
  
     ![Botão de barra de ferramentas de valores de projeto de importação](../../2014/tutorials/media/et-importingvaluesfromthecslistproject-01.jpg "importar botão de barra de ferramentas de valores de projeto")  
  
4.  No **importar valores de projeto** caixa de diálogo, selecione o **Limpar lista de fornecedores** do projeto e clique em **Okey**.  
  
5.  Observe que todos os emails são importados juntamente com as duas correções feitas durante a limpeza interativa. Role a tela para ver as duas correções.  
  
    |Valor|Corrigir para|  
    |-----------|----------------|  
    |bobby0@adventure-work.com|bobby0@adventure-works.com|  
    |tad0@adventure-work.com|tad0@adventure-works.com|  
  
6.  Repita a etapa anterior de importação de valores de projeto para o **país** domínio e observe que uma nova entrada será adicionada para corrigir **United State** para **dos Estados Unidos** (com ' s').  
  
    |Valor|Corrigir para|  
    |-----------|----------------|  
    |United State|Estados Unidos|  
  
7.  Para ver os valores de domínio antigos, desmarque **Mostrar somente novo** caixa de seleção.  
  
8.  Repita a etapa anterior de importação de valores de projeto para o **Supplier Name** domínio. Por padrão, após a importação, você verá apenas os novos valores. Para ver todos os valores, desmarque **Mostrar somente novo** caixa de seleção. Você enriqueceu a **fornecedores** da base de conhecimento com a qual aprendeu da atividade de limpeza. Quanto mais forte for a base de dados de conhecimento, melhores serão os resultados da limpeza.  
  
    > [!NOTE]  
    >  Não há valores de importação possíveis para um domínio composto.  
  
9. Clique em **exportar Base de dados de Conhecimento** ícone na barra de ferramentas e clique **exportar Base de dados de Conhecimento**.  
  
     ![Exportar Base de Conhecimento Menu](../../2014/tutorials/media/et-importingvaluesfromthecslistproject-02.jpg "exportar Base de Conhecimento de Menu")  
  
10. Navegue até a pasta Tutorial, digite **Suppliers.dqs** para o **nome de arquivo**e clique em **salvar**. Você pode usar esse arquivo do DQS para criar uma nova base de dados de conhecimento baseada nele.  
  
11. Clique em **Okey** para fechar o **exportar Base de dados de Conhecimento – Suppliers** caixa de mensagem.  
  
12. Clique em **concluir** para concluir a atividade.  
  
13. Clique em **Publicar**.  
  
14. Clique em **OK** na caixa de mensagem.  
  
## <a name="next-step"></a>Próxima etapa  
 [Lição 3: Correspondendo dados para remover duplicatas da lista de fornecedores](../../2014/tutorials/lesson-3-matching-data-to-remove-duplicates-from-supplier-list.md)  
  
  