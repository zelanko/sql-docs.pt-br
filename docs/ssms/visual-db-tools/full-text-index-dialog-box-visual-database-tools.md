---
title: "Caixa de diálogo Índice de Texto Completo (Ferramentas de Banco de Dados Visual) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- vdt.dlgbox.fulltextindex
ms.assetid: ef45b585-2567-4abe-b421-9fd0994e0146
caps.latest.revision: 5
author: stevestein
ms.author: sstein
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 9643dbca781cb469fd3895e1de265948bfbc873e
ms.lasthandoff: 04/11/2017

---
# <a name="full-text-index-dialog-box-visual-database-tools"></a>Caixa de diálogo Índice de Texto Completo (Visual Database Tools)
Essa caixa de diálogo permite que você crie um índice de texto completo, para executar pesquisas de texto completo em colunas baseadas em texto nas suas tabelas de banco de dados. Um índice de texto completo baseia-se em um índice regular, assim você deve criá-lo primeiro. O índice regular deve ser criado em uma coluna não nula exclusiva, e é melhor escolher uma coluna com valores baixos em vez de uma coluna com valores altos.  
  
> [!NOTE]  
> Para criar um índice de texto completo, você deve criar primeiro um catálogo de texto completo para o banco de dados usando uma ferramenta externa, como o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] ou o Enterprise Manager.  
  
> [!NOTE]  
> Não há uma funcionalidade de índice de texto completo disponível em todas as edições do [!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Para obter uma lista de recursos com suporte nas edições do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], consulte [Recursos com suporte nas edições do SQL Server 2012](http://msdn.microsoft.com/en-us/5da61ff5-12b9-48e6-b3c8-0dacca1751c4).  
  
## <a name="options"></a>Opções  
**Índice de texto completo selecionado**  
Exibe índices de texto completo existentes. Selecione um índice para exibir suas propriedades na grade à direita. Se a lista estiver vazia, nenhuma relação de texto completo foi definida para a tabela.  
  
**Adicionar**  
Crie um novo índice de texto completo.  
  
**Delete (excluir) (excluir)**  
Exclua o índice de texto completo selecionado na lista **Índice de texto completo selecionado** .  
  
**Categoria Geral**  
Quando expandida, mostra **Colunas** e o **Nome do Catálogo de Texto Completo**.  
  
**Colunas**  
Exibe uma lista de nomes de colunas pesquisável de texto completo separados por vírgula. Para consultar a lista completa, clique no botão de reticências (**…**) à esquerda do campo de propriedade.  
  
**Full-Text Catalog Name**  
Exibe o nome do catálogo de texto completo no qual este índice de texto completo é armazenado. Para armazenar o índice em um catálogo diferente, clique no nome do catálogo e escolha outro na lista suspensa.  
  
> [!NOTE]  
> O catálogo deve ser criado primeiro em uma ferramenta externa, como o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] ou o Enterprise Manager.  
  
**Categoria de identidade**  
Quando expandida, mostra o campo de nome para este índice.  
  
**Nome**  
Exibe o nome especificado pelo sistema para este índice de texto completo.  
  
**Categoria do Designer de Tabelas**  
Quando expandido, mostra as propriedades que ditam como o índice é executado.  
  
**Ativa**  
Indica se você pode executar uma pesquisa de texto completo usando este índice de texto completo.  
  
**Definição de Rastreamento de alterações**  
Descreve o status do controle de alterações para este índice: Manual, Automático ou Desligado.  
  
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
[Usar o Assistente para Indexação de Texto Completo](http://msdn.microsoft.com/en-us/3e9d9605-6525-4781-9168-fdaa06db3459)  
[CREATE FULLTEXT INDEX (Transact-SQL)](http://msdn.microsoft.com/en-us/8b80390f-5f8b-4e66-9bcc-cabd653c19fd)  
  

