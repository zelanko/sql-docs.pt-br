---
title: Opções (Designers de tabela e página de Designers de banco de dados) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- VS.ToolsOptionsPages.Designers.Table_Designer
ms.assetid: b43f4b97-17b9-4004-a824-f77b9e145741
caps.latest.revision: 25
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 4a324f7e0bd9ca0d71b727dd109f8d7dd0a8aec7
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37240276"
---
# <a name="options-designers-table-and-database-designers-page"></a>Opções (Designers de tabela e página de Designers de banco de dados)
  Use esta página para determinar o comportamento padrão do designer. Para acessar as configurações, no menu **Ferramentas** , clique em **Opções**, expanda  a pasta **Designers** e clique em **Designer de Tabela**.  
  
## <a name="uielement-list"></a>Lista de elementos de interface do usuário  
 **Substituir valor de tempo limite da cadeia de caracteres da conexão para atualizações do designer de tabela**  
 Permite que um novo valor de tempo limite seja definido para ações no designer de tabela. Isso pode ser útil quando o designer de tabela afetar uma tabela grande e requerer tempo extra para concluir a modificação da tabela.  
  
 **Tempo limite de transação após**  
 Define um valor de tempo limite para o designer de tabela.  
  
 **Gerar scripts de alteração automaticamente**  
 Cria, automaticamente, um script para implementar as alterações definidas no designer de tabela.  
  
 **Avisar sobre chaves primárias nulas**  
 Fornece uma caixa de diálogo de aviso quando um campo que é selecionado para uma chave primária puder conter valores nulos.  
  
 **Aviso sobre detecção de diferença**  
 Se você selecionar esta caixa, uma caixa de mensagens listará qualquer conflito entre suas alterações e as feitas por outro usuário ao salvar alterações.  
  
 **Avisar sobre tabelas afetadas**  
 Fornece uma caixa de diálogo de aviso que lista as tabelas que serão afetadas pela ação e solicita confirmação.  
  
 **Evitar salvar alterações que exijam recriação de tabela**  
 Impede um usuário de fazer alterações que requerem recriação de tabela. As ações seguintes poderiam exigir a recriação de uma tabela:  
  
-   Adição de uma nova coluna no meio da tabela  
  
-   Descarte de uma coluna  
  
-   Alteração da nulidade da coluna  
  
-   Alteração da ordem das colunas  
  
-   Alteração do tipo de dados de uma coluna  
  
 **Exibição de tabela padrão**  
 Selecione o modo que você deseja ver tabelas no designer:  
  
-   **Standard**  
  
     Mostra o cabeçalho, todos os nomes das colunas, os tipos de dados e a configuração Permitir Nulos da tabela.  
  
-   **Nomes de coluna**  
  
     Mostra os nomes das colunas.  
  
-   **Chave**  
  
     Mostra o cabeçalho de tabela e as colunas de chave primária.  
  
-   **Apenas nome**  
  
     Mostra apenas o cabeçalho da tabela com seu nome.  
  
-   **Personalizar**  
  
     Permite que você escolha quais colunas deseja exibir.  
  
 **Iniciar diálogo de adição de tabela no novo diagrama**  
 Abre automaticamente a caixa de diálogo **Adicionar Tabela** quando os designers são abertos.  
  
  
