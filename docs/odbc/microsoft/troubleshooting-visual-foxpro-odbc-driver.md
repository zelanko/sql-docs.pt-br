---
title: "Solução de problemas (Driver ODBC do Visual FoxPro) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: microsoft
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
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
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: ea6c45c362047d45275b6895d58faafe0250d26f
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/20/2017
---
# <a name="troubleshooting-visual-foxpro-odbc-driver"></a>Solução de problemas (Driver ODBC do Visual FoxPro)
As seções a seguir discutem como melhorar o desempenho e solucionar problemas que podem ocorrer ao usar o Driver de ODBC do Visual FoxPro.  
  
## <a name="accessing-parameterized-views"></a>Acessar exibições com parâmetros  
 Você não pode acessar exibições com parâmetros em um banco de dados do Visual FoxPro usando o driver. Uma exibição com parâmetros cria uma cláusula WHERE da exibição SQL **selecione** baixado de instrução que limita os registros para os registros que atendem às condições da cláusula WHERE criados usando o valor fornecido para o parâmetro. Porque o driver não dá suporte a passando parâmetros para o modo de exibição, tentar acessar uma exibição com parâmetros usando o driver irá falhar.  
  
 O valor do parâmetro pode ser fornecido em tempo de execução ou programaticamente passado para o modo de exibição.  
  
## <a name="accessing-remote-views"></a>Acessar modos de exibição remotos  
 Você não pode acessar modos de exibição remotos em um banco de dados do Visual FoxPro usando o driver. Exibições de remotas são que acessam dados não FoxPro ou uma combinação de FoxPro e dados de não-FoxPro. Para acessar os modos de exibição remotos, use do Visual FoxPro.  
  
## <a name="deleting-records"></a>Excluindo registros  
 Você pode marcar os registros para exclusão usando o driver, mas você não pode remover permanentemente os registros do banco de dados. Para remover permanentemente os registros de uma tabela, use o Visual FoxPro.  
  
## <a name="increasing-performance-using-background-fetching"></a>Aumentando o desempenho usando a busca em segundo plano  
 Você pode melhorar o desempenho em buscas grandes usando o plano de fundo buscando o recurso do driver. Busca em segundo plano usa um thread separado para buscar os dados solicitados de uma fonte de dados específico.  
  
 Você pode usar o plano de fundo buscando para uma fonte de dados em uma das seguintes maneiras:  
  
-   Verifique o **buscar dados no plano de fundo** caixa de seleção a [caixa de diálogo a instalação do Visual FoxPro ODBC](../../odbc/microsoft/odbc-visual-foxpro-setup-dialog-box.md).  
  
-   Use a palavra-chave de atributo BackgroundFetch em sua cadeia de conexão.  
  
 Para obter informações sobre palavras-chave atributo de cadeia de caracteres de conexão, consulte [usando cadeias de caracteres de Conexão](../../odbc/microsoft/using-connection-strings.md).  
  
## <a name="updating-multitiered-views"></a>Atualizando exibições de várias camadas  
 Uma exibição de várias camadas é um modo de exibição com base em uma ou mais exibições em vez de em uma tabela base. Quando você atualiza dados em um modo de exibição de várias camadas, as atualizações acessem apenas um nível, o modo de exibição na qual baseia-se a exibição de nível superior; tabelas base não são atualizadas.  
  
## <a name="using-data-definition-language-ddl-in-stored-procedures"></a>Usando a linguagem de definição de dados (DDL) em procedimentos armazenados  
 Você não pode usar DDL, como CREATE TABLE ou ALTER TABLE, procedimentos do Visual FoxPro armazenados.  
  
 Para obter informações sobre o idioma que você pode usar procedimentos armazenados, consulte [suporte para procedimentos armazenados, disparadores, valores padrão e regras](../../odbc/microsoft/support-rules-triggers-defaults-stored-procedures-visual-foxpro-odbc-driver.md).  
  
## <a name="using-positioned-updates"></a>Usando atualizações posicionadas  
 O driver não dá suporte a atualizações posicionadas. Use a cláusula SQL WHERE para identificar as linhas que você deseja atualizar.  
  
## <a name="using-the-set-ansi-command"></a>Usando o comando de ANSI SET  
 Se você for um desenvolvedor do Visual FoxPro, você deve estar ciente de que a configuração padrão para SET ANSI é ON para o driver, em contraste com uma configuração padrão de OFF para o Visual FoxPro. O padrão na configuração de SET ANSI permite fontes de dados do Visual FoxPro se comportem de forma consistente com outras fontes de dados ODBC que geralmente executam comparações exatas. Você pode alterar a configuração padrão. Para obter mais informações, consulte [SET ANSI](../../odbc/microsoft/set-ansi-command.md).
