---
title: Solução de problemas (Driver ODBC do Visual FoxPro) | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7f0576d017068b8ab0694da798c5be458f115e56
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62632602"
---
# <a name="troubleshooting-visual-foxpro-odbc-driver"></a>Solução de problemas (Driver ODBC do Visual FoxPro)
As seções a seguir discutem como melhorar o desempenho e solucionar problemas que podem ocorrer ao usar o Driver de ODBC do Visual FoxPro.  
  
## <a name="accessing-parameterized-views"></a>Acessando exibições com parâmetros  
 Você não pode acessar exibições com parâmetros em um banco de dados do Visual FoxPro usando o driver. Uma exibição com parâmetros cria uma cláusula WHERE no SQL da exibição **selecionar** baixado de instrução que limita os registros para os registros que atendem às condições da cláusula WHERE criada usando o valor fornecido para o parâmetro. Porque o driver não dá suporte a passando parâmetros para o modo de exibição, as tentativas de acessar uma exibição com parâmetros usando o driver falharão.  
  
 O valor do parâmetro pode ser fornecido em tempo de execução ou passado para o modo de exibição de forma programática.  
  
## <a name="accessing-remote-views"></a>Acessar modos de exibição remotos  
 Você não pode acessar exibições remotas em um banco de dados do Visual FoxPro usando o driver. Exibições remotas são que acessam dados não FoxPro ou uma combinação de FoxPro e dados não FoxPro. Para acessar modos de exibição remotos, use o Visual FoxPro.  
  
## <a name="deleting-records"></a>Exclusão de registros  
 Você pode marcar os registros para exclusão usando o driver, mas você não pode remover permanentemente os registros do banco de dados. Para remover permanentemente os registros de uma tabela, use o Visual FoxPro.  
  
## <a name="increasing-performance-using-background-fetching"></a>Aumentando o desempenho usando a busca em segundo plano  
 Você pode melhorar o desempenho em grandes buscas por meio do plano de fundo, buscando o recurso do driver. Busca em segundo plano usa um thread separado para buscar os dados solicitados de uma fonte de dados específico.  
  
 Você pode empregar em segundo plano, obtenção de uma fonte de dados em uma das seguintes maneiras:  
  
-   Verifique as **buscar dados em segundo plano** caixa de seleção a [caixa de diálogo de instalação do ODBC Visual FoxPro](../../odbc/microsoft/odbc-visual-foxpro-setup-dialog-box.md).  
  
-   Use a palavra-chave de atributo BackgroundFetch em sua cadeia de conexão.  
  
 Para obter informações sobre palavras-chave atributo de cadeia de caracteres de conexão, consulte [usando cadeias de caracteres de Conexão](../../odbc/microsoft/using-connection-strings.md).  
  
## <a name="updating-multitiered-views"></a>Atualizando exibições de várias camadas  
 Uma exibição de várias camadas é uma exibição com base em um ou mais modos de exibição e não em uma tabela base. Quando você atualiza dados em uma exibição de várias camadas, as atualizações descer apenas um nível, para a exibição na qual baseia-se a exibição de nível superior; tabelas base não são atualizadas.  
  
## <a name="using-data-definition-language-ddl-in-stored-procedures"></a>Usando a linguagem de definição de dados (DDL) em procedimentos armazenados  
 É possível usar DDL, como CREATE TABLE ou ALTER TABLE em procedimentos armazenados de Visual FoxPro.  
  
 Para obter informações sobre a linguagem que você pode usar em procedimentos armazenados, consulte [suporte para procedimentos armazenados, gatilhos, valores padrão e regras](../../odbc/microsoft/support-rules-triggers-defaults-stored-procedures-visual-foxpro-odbc-driver.md).  
  
## <a name="using-positioned-updates"></a>Usando atualizações posicionadas  
 O driver não dá suporte a atualizações posicionadas. Use a cláusula SQL WHERE para identificar as linhas que você deseja atualizar.  
  
## <a name="using-the-set-ansi-command"></a>Usando o comando SET ANSI  
 Se você for um desenvolvedor do Visual FoxPro, você deve estar ciente de que a configuração padrão para SET ANSI é ON para o driver, em contraste com uma configuração padrão de OFF para o Visual FoxPro. O padrão na configuração para SET ANSI permite que fontes de dados do Visual FoxPro se comportem consistentemente com outras fontes de dados ODBC que normalmente executam comparações exatas. Você pode alterar a configuração padrão. Para obter mais informações, consulte [SET ANSI](../../odbc/microsoft/set-ansi-command.md).
