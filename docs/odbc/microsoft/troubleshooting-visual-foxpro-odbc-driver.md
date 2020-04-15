---
title: Solução de problemas (Driver Visual FoxPro ODBC) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- set ANSI [ODBC]
- troubleshooting Visual FoxPro ODBC driver [ODBC]
- remote views [ODBC]
- multitiered views [ODBC]
- parameterized views [ODBC], Visual FoxPro ODBC driver
- fetches [ODBC], Visual FoxPro ODBC driver
- positioned updates [ODBC]
- background fetching [ODBC]
ms.assetid: fd478dd8-666a-4f0a-a2d6-b94e81cbbe4b
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 70b035069c0be88d05a3aa5e17b96af991c27405
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303027"
---
# <a name="troubleshooting-visual-foxpro-odbc-driver"></a>Solução de problemas (Driver ODBC do Visual FoxPro)
As seções a seguir discutem como melhorar o desempenho e resolver problemas que você pode encontrar ao usar o Driver Visual FoxPro ODBC.  
  
## <a name="accessing-parameterized-views"></a>Acessando visualizações parametrizadas  
 Você não pode acessar visualizações parametrizadas em um banco de dados Visual FoxPro usando o driver. Uma exibição parametrizada cria uma cláusula WHERE na declaração SQL **SELECT** da exibição que limita os registros baixados para os registros que atendem às condições da cláusula WHERE construída usando o valor fornecido para o parâmetro. Como o driver não suporta parâmetros de passagem para a visualização, as tentativas de acessar uma visualização parametrizada usando o driver falharão.  
  
 O valor do parâmetro pode ser fornecido em tempo de execução ou passado programáticamente para a exibição.  
  
## <a name="accessing-remote-views"></a>Acessando visualizações remotas  
 Você não pode acessar visualizações remotas em um banco de dados Visual FoxPro usando o driver. Visualizações remotas são visualizações que acessam dados não-FoxPro ou uma combinação de dados FoxPro e não-FoxPro. Para acessar vistas remotas, use o Visual FoxPro.  
  
## <a name="deleting-records"></a>Excluindo registros  
 Você pode marcar registros de exclusão usando o driver, mas não pode remover permanentemente registros do banco de dados. Para remover permanentemente os registros de uma tabela, use o Visual FoxPro.  
  
## <a name="increasing-performance-using-background-fetching"></a>Aumento do desempenho usando busca de fundo  
 Você pode melhorar o desempenho em grandes buscas usando o recurso de busca de fundo do driver. A busca de antecedentes usa um segmento separado para buscar dados solicitados de uma fonte de dados específica.  
  
 Você pode empregar busca de antecedentes para uma fonte de dados de uma das seguintes maneiras:  
  
-   Verifique os **dados do Fetch na** caixa de seleção de fundo na caixa de diálogo De [configuração Visual FoxPro do ODBC](../../odbc/microsoft/odbc-visual-foxpro-setup-dialog-box.md).  
  
-   Use a palavra-chave de atributo BackgroundFetch na seqüência de conexões.  
  
 Para obter informações sobre palavras-chave de atributo de seqüência de conexão, consulte [Usando strings de conexão](../../odbc/microsoft/using-connection-strings.md).  
  
## <a name="updating-multitiered-views"></a>Atualizando visualizações multicamadas  
 Uma visão multicamadas é uma visão baseada em uma ou mais visualizações em vez de em uma tabela base. Quando você atualiza dados em uma exibição multinível, as atualizações descem apenas um nível, para a exibição na qual a exibição de nível superior é baseada; as tabelas básicas não são atualizadas.  
  
## <a name="using-data-definition-language-ddl-in-stored-procedures"></a>Usando o DDL (Data Definition Language, linguagem de definição de dados) em procedimentos armazenados  
 Você não pode usar DDL, como CREATE TABLE ou ALTER TABLE, em procedimentos armazenados pelo Visual FoxPro.  
  
 Para obter informações sobre o idioma que você pode usar em procedimentos armazenados, consulte [Suporte para Regras, Gatilhos, Valores padrão e procedimentos armazenados.](../../odbc/microsoft/support-rules-triggers-defaults-stored-procedures-visual-foxpro-odbc-driver.md)  
  
## <a name="using-positioned-updates"></a>Usando atualizações posicionadas  
 O driver não suporta atualizações posicionadas. Use a cláusula SQL WHERE para identificar as linhas que deseja atualizar.  
  
## <a name="using-the-set-ansi-command"></a>Usando o comando SET ANSI  
 Se você é um desenvolvedor Visual FoxPro, você deve estar ciente de que a configuração padrão para SET ANSI está ON para o driver, em contraste com uma configuração padrão de OFF para Visual FoxPro. A configuração PADRÃO ON para SET ANSI permite que as fontes de dados do Visual FoxPro se comportem consistentemente com outras fontes de dados ODBC que normalmente realizam comparações exatas. Você pode alterar a configuração padrão. Para obter mais informações, consulte [SET ANSI](../../odbc/microsoft/set-ansi-command.md).
