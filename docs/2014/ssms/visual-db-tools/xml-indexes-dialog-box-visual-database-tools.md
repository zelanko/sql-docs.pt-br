---
title: Caixa de diálogo Índices XML (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- vdt.dlgbox.xmlindexes
ms.assetid: eef38310-4498-4ccc-bb77-5bbd1c7cc477
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: a0c946e0e195937dd2e722ac3f092a57e40427b8
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "63228368"
---
# <a name="xml-indexes-dialog-box-visual-database-tools"></a>Caixa de diálogo Índices XML (Visual Database Tools)
  Use a caixa de diálogo **Índices XML** para criar índices para colunas do tipo de dados XML, que não podem ser indexadas utilizando a caixa de diálogo **Índice/Chaves** . Cada coluna XML pode ter mais de um índice XML, mas o primeiro a ser criado (primário) será a base para os demais (secundários). Se você excluir o índice XML primário, os índices secundários também serão excluídos.  
  
## <a name="options"></a>Opções  
 **Índice XML selecionado**  
 Lista os índices XML existentes. Selecione para exibir suas propriedades na grade à direita. Se a lista estiver vazia, nenhum terá sido definido para a tabela.  
  
 **Adicionar**  
 Cria um índice XML novo.  
  
 **Delete (excluir)**  
 Exclui um índice XML selecionado na lista **Índice XML selecionado** . Se você excluir o índice XML primário, você será notificado que isso também excluirá todos os índices secundários e você pode continuar ou cancelar a ação.  
  
 **Categoria Geral**  
 Quando expandida, mostra os campos de propriedade para **Colunas**, **É primário**e **Tipo**.  
  
 **Colunas**  
 Mostra que esse índice é classificado em ordem crescente.  
  
 **É primário**  
 Indica se esse é o índice primário. O primeiro índice XML criado na coluna será a base para os outros.  
  
 **Nome de referência primário**  
 Mostra o nome do índice primário se esse for um índice secundário. Disponível apenas se este for um índice secundário.  
  
 **Tipo secundário**  
 Mostra o tipo de índice secundário. Disponível apenas se este for um índice secundário.  
  
 **Tipo**  
 Mostra que esse é um índice XML.  
  
 **Categoria de identidade**  
 Quando expandida, mostra os campos de propriedade **Nome** e **Descrição** .  
  
 **Nome**  
 Mostra o nome do índice XML. Quando um novo índice é criado ele recebe um nome padrão com base na tabela da janela ativa no Designer de tabelas. É possível alterar o nome a qualquer momento.  
  
 **Descrição**  
 Descreve o índice. Para escrever uma descrição mais detalhada, clique em **Descrição** e, em seguida, clique no botão de reticências ( **…** ) que aparece à direita do campo de propriedade. Isso criará uma área maior para a redação do texto.  
  
 **Categoria do Designer de Tabelas**  
 Quando expandida, mostra informações sobre as propriedades desse índice XML.  
  
 **Especificação de preenchimento**  
 Quando expandido, mostra informações de **Fator de Preenchimento** e **Preenchimento de índice**.  
  
 **Fator de Preenchimento**  
 Especifica a porcentagem da página de índice que o sistema poderá preencher. Após o preenchimento da página, o sistema precisa dividir a página se forem adicionados novos dados, o que compromete o desempenho.  
  
-   Um valor de 100 significa que as páginas serão preenchidas; isso exige o espaço mínimo de armazenamento mas é o menos eficaz. Essa configuração só deverá usada quando não houver alterações de dados; por exemplo, em uma tabela somente leitura.  
  
-   Um valor inferior propicia mais espaço vazio nas páginas de dados, o que reduz a necessidade de dividir as páginas de dados à medida que os índices aumentam. Porém, isso requer mais espaço de armazenamento. Essa configuração é mais adequada quando houver alterações nos dados da tabela.  
  
 **Preenchimento de índice**  
 Fornece páginas nesse índice com a mesmo percentual de espaço vazio (preenchimento) especificado em **Fator de Preenchimento**.  
  
 **Está Desabilitado**  
 Especifica se esse índice está desabilitado. Índices desabilitados não oferecem suporte para pesquisas, nem são atualizados quando são adicionados itens novos à tabela. Você pode melhorar o desempenho para inserções em massa e atualizações desabilitando um índice.  
  
 **Bloqueios de página permitidos**  
 Especifica se o bloqueio de página é permitido no índice. A permissão ou não dos bloqueios de página afeta o desempenho do banco de dados.  
  
 **Recalcular estatísticas**  
 Calcula estatísticas novas quando o índice é criado. Ao se recalcular estatísticas retarda-se a criação dos índices, mas em geral melhora-se o desempenho da consulta.  
  
 **Bloqueios de Linha Permitidos**  
 Especifica se o bloqueio de linha é permitido no índice. A permissão ou não dos bloqueios de linha afeta o desempenho do banco de dados.  
  
## <a name="see-also"></a>Consulte Também  
 [Criar índices XML](../../relational-databases/xml/create-xml-indexes.md)  
  
  
