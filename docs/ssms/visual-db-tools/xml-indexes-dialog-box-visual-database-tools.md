---
title: Caixa de diálogo Índices XML (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.component: ssms-visual-db
ms.reviewer: ''
ms.suite: sql
ms.technology: ssms
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- vdt.dlgbox.xmlindexes
ms.assetid: eef38310-4498-4ccc-bb77-5bbd1c7cc477
caps.latest.revision: 5
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 00757208c128ef00ea58c5139b6edc8461621307
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="xml-indexes-dialog-box-visual-database-tools"></a>Caixa de diálogo Índices XML (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
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
Mostra o nome do índice XML. Quando um novo índice é criado ele recebe um nome padrão com base na tabela da janela ativa no Designer de tabelas. O nome pode ser alterado a qualquer momento.  
  
**Descrição**  
Descreve o índice. Para redigir uma descrição mais detalhada, clique em **Descrição** e depois clique no botão de reticências (**…**) que aparece à direita do campo de propriedade. Isso criará uma área maior para a redação do texto.  
  
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
[Criar índices XML](http://msdn.microsoft.com/en-us/6ecac598-355d-4408-baf7-1b2e8d4cf7c1)  
  
