---
title: Solução de problemas (driver ODBC do Visual FoxPro) | Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81303027"
---
# <a name="troubleshooting-visual-foxpro-odbc-driver"></a>Solução de problemas (Driver ODBC do Visual FoxPro)
As seções a seguir discutem como melhorar o desempenho e resolver problemas que você pode encontrar ao usar o driver ODBC do Visual FoxPro.  
  
## <a name="accessing-parameterized-views"></a>Acessando exibições parametrizadas  
 Você não pode acessar exibições parametrizadas em um banco de dados do Visual FoxPro usando o driver. Uma exibição com parâmetros cria uma cláusula WHERE na instrução SQL **Select** da exibição que limita os registros baixados para os registros que atendem às condições da cláusula WHERE criada usando o valor fornecido para o parâmetro. Como o driver não dá suporte à passagem de parâmetros para a exibição, as tentativas de acessar uma exibição parametrizada usando o driver falharão.  
  
 O valor do parâmetro pode ser fornecido em tempo de execução ou transmitido programaticamente para a exibição.  
  
## <a name="accessing-remote-views"></a>Acessando exibições remotas  
 Você não pode acessar exibições remotas em um banco de dados do Visual FoxPro usando o driver. Exibições remotas são exibições que acessam dados não-FoxPro ou uma combinação de dados do FoxPro e não do FoxPro. Para acessar exibições remotas, use o Visual FoxPro.  
  
## <a name="deleting-records"></a>Excluindo registros  
 Você pode marcar registros para exclusão usando o driver, mas não pode remover permanentemente os registros do banco de dados. Para remover permanentemente os registros de uma tabela, use o Visual FoxPro.  
  
## <a name="increasing-performance-using-background-fetching"></a>Aumentando o desempenho usando a busca em segundo plano  
 Você pode melhorar o desempenho em buscas grandes usando o recurso de busca em segundo plano do driver. A busca em segundo plano usa um thread separado para buscar dados solicitados de uma fonte de dados específica.  
  
 Você pode empregar busca em segundo plano para uma fonte de dados de uma das seguintes maneiras:  
  
-   Marque a caixa de seleção **buscar dados no plano de fundo** em [configuração do ODBC Visual FoxPro](../../odbc/microsoft/odbc-visual-foxpro-setup-dialog-box.md).  
  
-   Use a palavra-chave do atributo BackgroundFetch em sua cadeia de conexão.  
  
 Para obter informações sobre palavras-chave de atributo de cadeia de conexão, consulte [usando cadeias de conexão](../../odbc/microsoft/using-connection-strings.md).  
  
## <a name="updating-multitiered-views"></a>Atualizando exibições em várias camadas  
 Uma exibição multicamada é uma exibição baseada em uma ou mais exibições em vez de em uma tabela base. Quando você atualiza dados em uma exibição multicamada, as atualizações ficam inativas apenas um nível, até a exibição na qual a exibição de nível superior é baseada; As tabelas base não são atualizadas.  
  
## <a name="using-data-definition-language-ddl-in-stored-procedures"></a>Usando DDL (linguagem de definição de dados) em procedimentos armazenados  
 Você não pode usar DDL, como CREATE TABLE ou ALTER TABLE, em procedimentos armazenados do Visual FoxPro.  
  
 Para obter informações sobre o idioma que você pode usar em procedimentos armazenados, consulte [suporte para regras, gatilhos, valores padrão e procedimentos armazenados](../../odbc/microsoft/support-rules-triggers-defaults-stored-procedures-visual-foxpro-odbc-driver.md).  
  
## <a name="using-positioned-updates"></a>Usando atualizações posicionadas  
 O driver não dá suporte a atualizações posicionadas. Use a cláusula SQL WHERE para identificar as linhas que você deseja atualizar.  
  
## <a name="using-the-set-ansi-command"></a>Usando o comando SET ANSI  
 Se você for um desenvolvedor do Visual FoxPro, deve estar ciente de que a configuração padrão para SET ANSI está ativada para o driver, em contraste com uma configuração padrão OFF para Visual FoxPro. A configuração padrão ON para SET ANSI permite que as fontes de dados do Visual FoxPro se comportem consistentemente com outras fontes de dados ODBC que normalmente executam comparações exatas. Você pode alterar a configuração padrão. Para obter mais informações, consulte [set ANSI](../../odbc/microsoft/set-ansi-command.md).
