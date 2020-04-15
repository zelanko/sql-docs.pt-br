---
title: Criando etiquetas de mailing no Microsoft Word usando dados visuais foxpro | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Visual FoxPro data [ODBC], mailing labels
- Visual FoxPro data [ODBC], Word
- mailing labels [ODBC]
- Visual FoxPro ODBC driver [ODBC], Word
- FoxPro ODBC driver [ODBC], word
ms.assetid: c901b60c-9f84-407a-b3d1-b4d301a71370
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c3ca6c729cfa988e2560192d705bc24e9e7b4fa1
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81280796"
---
# <a name="creating-mailing-labels-in-microsoft-word-using-visual-foxpro-data"></a>Criar rótulos de correspondência no Microsoft Word usando dados do Visual FoxPro
Você pode usar dados do Visual FoxPro em um documento do Microsoft Word para Windows 95 ou Windows 98. Por exemplo, você pode querer criar etiquetas de e-mail a partir das informações do cliente armazenadas em uma tabela Visual FoxPro.  
  
### <a name="to-create-mailing-labels"></a>Para criar etiquetas de e-mail  
  
1.  No Microsoft Word, crie um novo documento em branco.  
  
2.  No menu Ferramentas, escolha Mesclagem de correio.  
  
3.  No Mail Merge Helper, escolha Criar e, em seguida, selecione Etiquetas de envio de correspondência.  
  
4.  Em Documento Principal, escolha Janela Ativa.  
  
5.  Em Data Source, escolha Obter dados e, em seguida, selecione Código de dados aberto.  
  
6.  Na caixa de diálogo Código de dados aberto, escolha Consulta MS.  
  
7.  Na caixa de diálogo Selecionar fonte de dados, selecione uma fonte de dados Visual FoxPro e clique em Usar.  
  
8.  Se o banco de dados acessado pela sua fonte de dados incluir tabelas, selecione uma tabela na caixa de diálogo Adicionar tabelas. O Microsoft Query exibe a tabela adicionada na metade superior do designer de consulta.  
  
9. Selecione campos para sua consulta arrastando-os da tabela para a metade inferior do designer.  
  
10. No menu Arquivo, escolha 'Retornar dados' ao Microsoft Word. A Consulta Microsoft fecha e os dados selecionados estão disponíveis para uso no documento de mesclagem de e-mails.  
  
11. Em Documento Principal, escolha Configuração.  
  
12. Na caixa de diálogo 'Opções de rótulo', selecione as informações da impressora e do rótulo desejadas e clique em OK.  
  
13. Na caixa de diálogo Criar rótulos, selecione os campos que deseja imprimir nos rótulos de e-mail e clique em OK.  
  
14. No Mail Merge Helper, sob a Mesclagem dos Dados com o Documento, clique em Mesclar.  
  
15. Na caixa de diálogo Mesclar, selecione as opções desejadas e clique em Mesclar.
