---
title: Adicionar itens existentes a um projeto | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- projects [SQL Server Management Studio], item additions
- adding project items
ms.assetid: 084b3879-e96b-45a7-b421-6a4b0db2b92b
author: markingmyname
ms.author: maghan
ms.openlocfilehash: cfdc8405fd958efb34a607736648eddf5f4732dc
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/16/2019
ms.locfileid: "68252833"
---
# <a name="add-existing-items-to-a-project"></a>Adicionar itens existentes a um projeto
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
Adicione novos itens a um projeto para estender a funcionalidade do aplicativo. Um item existente pode ser uma consulta ou um arquivo diverso. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] tem dois tipos de projeto: Projeto de Script do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e Projeto de Script do Analysis Services. O tipo de projeto determina os arquivos de consulta que você pode adicionar ao projeto. Por exemplo, você pode adicionar uma consulta [!INCLUDE[tsql](../../includes/tsql-md.md)] (um arquivo com uma extensão .sql) a um projeto de script do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , mas não pode adicioná-lo a um Projeto de Script do Analysis Services. Confira como associar extensões de arquivo adicionais a um tipo de projeto em [Como associar extensões de arquivo a um Editor de Códigos](../../relational-databases/scripting/associate-file-extensions-to-a-code-editor.md).  
  
### <a name="to-add-an-existing-query-or-a-miscellaneous-file-to-a-project"></a>Para adicionar uma consulta existente ou um arquivo diverso a um projeto  
  
1.  No Gerenciador de Soluções, selecione um projeto de destino.  
  
2.  No menu **Projeto** , clique em **Adicionar Item Existente**.  
  
    **Look in**  
    Localize os arquivos ou pastas a adicionar ao seu projeto nesta lista. Em XML Web Services e aplicativos Web ASP.NET, os arquivos se localizam no servidor Web.  
  
    **Área de Trabalho**  
    Exibe os arquivos e pastas localizadas na área de trabalho.  
  
    **Meus Projetos**  
    Exibe os arquivos e pastas no local padrão **Meus Projetos** .  
  
    **Meu Computador**  
    Exibe o conteúdo de sua pasta **Meu Computador** .  
  
    **Nome do arquivo**  
    Use esta opção para filtrar os arquivos e pastas a serem exibidos. Insira o nome completo ou parcial do arquivo a filtrar; use um asterisco (`*`) como curinga.  
  
    > [!NOTE]  
    > Navegue na Web e em locais de rede inserindo a URL ou o caminho de rede na caixa **Nome do arquivo** . Por exemplo, **`https://mywebsite`** exibe os arquivos disponíveis no local da Web meusite e **\\\meuservidor\meucompartilhamento** exibe os arquivos disponíveis no local meucompartilhamento em meuservidor.  
  
    **Arquivos do tipo**  
    Use esta opção para filtrar arquivos com base na extensão de arquivo. Cada produto lista filtros padrões dos tipos de arquivo mais comuns.  
  
    **Adicionar**  
    Use este botão suspenso para adicionar o item ao projeto e abrir o item em seu editor padrão.  
  
    -   **Adicionar**  
  
        Copia o item existente na sua pasta de projeto no disco e adiciona o item sob o projeto selecionado no Gerenciador de Soluções. Nenhuma alteração feita ao item é refletida no item no local original. Esse é o editor padrão do tipo de arquivo.  
  
    -   **Adicionar Como Vínculo**  
  
        Adiciona o arquivo selecionado ao projeto e abre-o com o editor padrão do tipo de arquivo. Essa opção abre o arquivo originalmente selecionado e não copia o arquivo na pasta de projeto.  
  
3.  Na adição de arquivos de consulta, a caixa de diálogo de conexão solicitará que você especifique uma conexão para a consulta. Você poderá clicar em **Cancelar** na caixa de diálogo de conexão se não quiser associar uma conexão à consulta.  
  
4.  O arquivo será adicionado à pasta **Consultas** ou **Arquivos Diversos** do projeto.  
  
## <a name="see-also"></a>Consulte Também  
[Gerenciador de Soluções](../../ssms/solution/solution-explorer.md)  
[Adicionar novos itens a um projeto](../../ssms/solution/add-new-items-to-a-project.md)  
[Remover ou excluir um item ou projeto](../../ssms/solution/remove-or-delete-an-item-or-project.md)  
  
