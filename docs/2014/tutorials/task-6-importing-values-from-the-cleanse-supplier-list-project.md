---
title: 'Tarefa 6: importando valores do projeto de lista de fornecedores de limpeza | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: fec0deef-a729-4ff1-b709-72d2b3f407ac
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: f6b90a36238cd4a02e86d49125ee662f07d32882
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "65489091"
---
# <a name="task-6-importing-values-from-the-cleanse-supplier-list-project"></a>Tarefa 6: Importando valores do projeto Limpar Lista de Fornecedores
  Nesta tarefa, você importará o conhecimento de qualidade de dados adquirido durante o processo de limpeza. Consulte [importando valores de projeto de limpeza em um](https://msdn.microsoft.com/library/hh479581.aspx) tópico de domínio para obter mais detalhes. Você também exporta a base de dados de conhecimento para um arquivo do DQS antes de publicar a base de dados de conhecimento dos **fornecedores** atualizados.  
  
1.  Na página principal do **cliente do DQS**, clique na **seta para a direita** ao lado de **fornecedores** em bases de **dados de conhecimento recentes** e clique em **Gerenciamento de domínio**.  
  
2.  Clique em **email de contato** na lista de domínios e alterne para a guia valores de **domínio** no painel direito.  
  
3.  Clique na **seta para baixo** ao lado do ícone **importar valores** na barra de ferramentas e clique em **importar valores do projeto**.  
  
     ![Botão de barra de ferramentas Importar Valores de Projeto](../../2014/tutorials/media/et-importingvaluesfromthecslistproject-01.jpg "Botão de barra de ferramentas Importar Valores de Projeto")  
  
4.  Na caixa de diálogo **importar valores do projeto** , selecione o projeto de **lista limpar fornecedor** e clique em **OK**.  
  
5.  Observe que todos os emails são importados juntamente com as duas correções feitas durante a limpeza interativa. Role a tela para ver as duas correções.  
  
    |Valor|Corrigir para|  
    |-----------|----------------|  
    |bobby0@adventure-work.com|bobby0@adventure-works.com|  
    |tad0@adventure-work.com|tad0@adventure-works.com|  
  
6.  Repita a etapa anterior da importação de valores de projeto para o domínio de **país** e observe que uma nova entrada é adicionada para corrigir o **estado United** para **Estados Unidos** (com ').  
  
    |Valor|Corrigir para|  
    |-----------|----------------|  
    |United State|Estados Unidos|  
  
7.  Para ver os valores de domínio antigos, desmarque **Mostrar somente nova** caixa de seleção.  
  
8.  Repita a etapa anterior da importação de valores de projeto para o domínio de **nome do fornecedor** . Por padrão, após a importação, você verá apenas os novos valores. Para ver todos os valores, desmarque **Mostrar somente nova** caixa de seleção. Você enriqueceu a base de dados de conhecimento dos **fornecedores** com o que aprendeu na atividade de limpeza. Quanto mais forte for a base de dados de conhecimento, melhores serão os resultados da limpeza.  
  
    > [!NOTE]  
    >  Não há valores de importação possíveis para um domínio composto.  
  
9. Clique no ícone **Exportar base de dados de conhecimento** na barra de ferramentas e clique em **Exportar base de dados de conhecimento**.  
  
     ![Menu Exportar Base de Dados de Conhecimento](../../2014/tutorials/media/et-importingvaluesfromthecslistproject-02.jpg "Menu Exportar Base de Dados de Conhecimento")  
  
10. Navegue até a pasta tutorial, digite **suppliers. DQS** para o **nome do arquivo**e clique em **salvar**. Você pode usar esse arquivo do DQS para criar uma nova base de dados de conhecimento baseada nele.  
  
11. Clique em **OK** para fechar a caixa de mensagem **Exportar base de dados de conhecimento-fornecedores** .  
  
12. Clique em **concluir** para concluir a atividade.  
  
13. Clique em **Publicar**.  
  
14. Clique em **OK** na caixa de mensagem.  
  
## <a name="next-step"></a>Próxima etapa  
 [Lição 3: Correspondendo dados para remover duplicatas da lista de fornecedores](../../2014/tutorials/lesson-3-matching-data-to-remove-duplicates-from-supplier-list.md)  
  
  
