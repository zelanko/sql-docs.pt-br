---
title: Caixa de diálogo Índice de Texto Completo (Ferramentas de Banco de Dados Visual) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- vdt.dlgbox.fulltextindex
ms.assetid: ef45b585-2567-4abe-b421-9fd0994e0146
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: adb00f8b0e7cb009420e9843532c3f3d4deb0833
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63028403"
---
# <a name="full-text-index-dialog-box-visual-database-tools"></a>Caixa de diálogo Índice de Texto Completo (Visual Database Tools)
  Essa caixa de diálogo permite que você crie um índice de texto completo, para executar pesquisas de texto completo em colunas baseadas em texto nas suas tabelas de banco de dados. Um índice de texto completo baseia-se em um índice regular, assim você deve criá-lo primeiro. O índice regular deve ser criado em uma coluna não nula exclusiva, e é melhor escolher uma coluna com valores baixos em vez de uma coluna com valores altos.  
  
> [!NOTE]  
>  Para criar um índice de texto completo, você deve criar primeiro um catálogo de texto completo para o banco de dados usando uma ferramenta externa, como o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou o Enterprise Manager.  
  
> [!NOTE]  
>  Não há uma funcionalidade de índice de texto completo disponível em todas as edições do [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obter uma lista de recursos com suporte nas edições do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], consulte [Features Supported by the Editions of SQL Server 2014](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md).  
  
## <a name="options"></a>Opções  
 **Índice de texto completo selecionado**  
 Exibe índices de texto completo existentes. Selecione um índice para exibir suas propriedades na grade à direita. Se a lista estiver vazia, nenhuma relação de texto completo foi definida para a tabela.  
  
 **Adicionar**  
 Crie um novo índice de texto completo.  
  
 **Delete (excluir)**  
 Exclua o índice de texto completo selecionado na lista **Índice de texto completo selecionado** .  
  
 **Categoria Geral**  
 Quando expandida, mostra **Colunas** e o **Nome do Catálogo de Texto Completo**.  
  
 **Colunas**  
 Exibe uma lista de nomes de colunas pesquisável de texto completo separados por vírgula. Para ver a lista completa, clique no botão de reticências ( **...** ) à esquerda do campo de propriedade.  
  
 **Full-Text Catalog Name**  
 Exibe o nome do catálogo de texto completo no qual este índice de texto completo é armazenado. Para armazenar o índice em um catálogo diferente, clique no nome do catálogo e escolha outro na lista suspensa.  
  
> [!NOTE]  
>  O catálogo deve ser criado primeiro em uma ferramenta externa, como o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou o Enterprise Manager.  
  
 **Categoria de identidade**  
 Quando expandida, mostra o campo de nome para este índice.  
  
 **Nome**  
 Exibe o nome especificado pelo sistema para este índice de texto completo.  
  
 **Categoria do Designer de Tabelas**  
 Quando expandido, mostra as propriedades que ditam como o índice é executado.  
  
 **Ativa**  
 Indica se você pode executar uma pesquisa de texto completo usando este índice de texto completo.  
  
 **Definição de Rastreamento de alterações**  
 Descreve o status do controle de alterações deste índice: Manual, automático ou desabilitado.  
  
 **Rastreamento Concluído**  
 Mostra se o rastreamento mais recente foi concluído. Se este valor de propriedade for Não, um rastreamento está em progresso no momento.  
  
 **Data e Hora de Término do Rastreamento Atual ou Último**  
 Exibe a data e a hora de término do rastreamento mais recente.  
  
 **Erros no Rastreamento Atual ou Último**  
 Exibe o número de erros em rastreamentos atuais ou mais recentes.  
  
 **Versão do Índice**  
 Exibe a versão do esquema da tabela na hora em que o rastreamento iniciou.  
  
 **Linhas no Rastreamento Atual ou Último**  
 Exibe o número de linhas atualizado no rastreamento atual ou mais recente.  
  
 **Data e Hora de Início do Rastreamento Atual ou Último**  
 Exibe a data e a hora em que o rastreamento atual ou mais recente iniciou.  
  
 **Carimbo de Data/Hora do Próximo Rastreamento**  
 Exibe a data e a hora em que o próximo rastreamento iniciará.  
  
 **Tipo do Rastreamento Atual ou Último**  
 Exibe o tipo do rastreamento atual ou mais recente: Completo, Incremental, Atualização ou Propagação Automática.  
  
 **Nome do Índice Exclusivo**  
 Exibe uma lista de todos os nomes de colunas neste banco de dados que têm índices de uma única coluna exclusivos. Estas colunas podem ser usadas para criar um índice de texto completo.  
  
## <a name="see-also"></a>Consulte também  
 [Use o Assistente para indexação de texto completo](../../relational-databases/search/use-the-full-text-indexing-wizard.md)   
 [CREATE FULLTEXT INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-fulltext-index-transact-sql)  
  
  
