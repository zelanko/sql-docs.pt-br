---
title: Formato de cadeia de caracteres de Conexão e os atributos | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- connection strings [ODBC], ODBC driver for Oracle
- ODBC driver for Oracle [ODBC], connection strings
ms.assetid: 0c360112-8720-4e54-a1a6-b9b18d943557
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 7a16ee8409a96433929e2b900e3f68c41573a8b1
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="connection-string-format-and-attributes"></a>Atributos e formato de cadeia de caracteres de Conexão
> [!IMPORTANT]  
>  Este recurso será removido em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Em vez disso, use o driver ODBC fornecido pela Oracle.  
  
 Em vez de usar uma caixa de diálogo, alguns aplicativos podem exigir uma cadeia de caracteres de conexão que especifica informações de conexão de fonte de dados. A cadeia de caracteres de conexão é composta de um número de atributos que especificam como um driver se conecta a uma fonte de dados. Um atributo identifica uma peça específica de informações que o driver precisa saber antes de ele pode tornar a conexão de fonte de dados apropriado. Cada driver pode ter um conjunto diferente de atributos, mas o formato de cadeia de caracteres de conexão é sempre o mesmo. Uma cadeia de caracteres de conexão tem o seguinte formato:  
  
```  
"DSN=data-source-name[;SERVER=value] [;PWD=value] [;UID=value] [;<Attribute>=<value>]"  
```  
  
> [!NOTE]  
>  O Microsoft ODBC Driver for Oracle suporta o formato de cadeia de caracteres de conexão da primeira versão do driver, usado `CONNECTSTRING`= em vez de `SERVER=`.  
  
 Se você estiver se conectando a um provedor de fonte de dados que oferece suporte à autenticação do Windows, você deve especificar `Trusted_Connection=yes` em vez das informações de ID e a senha do usuário na cadeia de conexão.  
  
 Você deve especificar a fonte de dados nome se você não especificar o UID, PWD, SERVER (ou CONNECTSTRING) e os atributos DRIVER. No entanto, todos os outros atributos são opcionais. Se você não especificar um atributo, esse atributo padrão é especificado na guia DSN relevante do **administrador de fonte de dados ODBC** caixa de diálogo. O valor do atributo pode diferenciar maiusculas de minúsculas.  
  
 Os atributos para a cadeia de caracteres de conexão são da seguinte maneira:  
  
|Atributo|Description|Valor padrão|  
|---------------|-----------------|-------------------|  
|DSN|O nome da fonte de dados listados na guia Drivers do **administrador de fonte de dados ODBC** caixa de diálogo.|""|  
|PWD|A senha para o servidor Oracle que você deseja acessar. Este driver suporta limitações Oracle coloca em senhas.|""|  
|SERVER|A cadeia de conexão para o servidor Oracle que você deseja acessar.|""|  
|UID|O nome de usuário do servidor Oracle. Dependendo do seu sistema, esse atributo não pode ser opcional — ou seja, determinados bancos de dados e tabelas podem exigir este atributo para fins de segurança.<br /><br /> Use "/" usar o Oracle operacional da autenticação do sistema.|""|  
|BUFFERSIZE|O tamanho do buffer ideal usado ao buscar colunas.<br /><br /> O driver otimiza a busca para que uma busca no servidor Oracle retorne linhas suficientes para preencher um buffer desse tamanho. Valores maiores tendem a aumentar o desempenho se você buscar muitos dados.|65535|  
|SYNONYMCOLUMNS|Quando esse valor é verdadeiro (1), uma chamada de API (,) SQLColumn retorna informações de coluna. Caso contrário, (SQLColumn) retorna apenas colunas para tabelas e exibições. O Driver ODBC do Oracle fornece acesso mais rápido quando esse valor não está definido.|1|  
|REMARKS|Quando esse valor é verdadeiro (1), o driver retorna colunas de comentários para o [SQLColumns](../../odbc/microsoft/level-1-api-functions-odbc-driver-for-oracle.md) conjunto de resultados. O Driver ODBC do Oracle fornece acesso mais rápido quando esse valor não está definido.|0|  
|StdDayOfWeek|Impõe o padrão ODBC para DayOfWeek. Por padrão for ativado, mas os usuários que precisam ter a versão localizada podem alterar o comportamento para usar o Oracle retorna.|1|  
|GuessTheColDef|Especifica se o driver deve retornar um valor diferente de zero para o *cbColDef* argumento de **SQLDescribeCol**. Aplica-se apenas a colunas onde há sem escala definidas para Oracle, como calculado numéricas colunas e colunas definidas como número sem precisão ou escala. Um **SQLDescribeCol** chamada retorna 130 para a precisão quando o Oracle não fornecer essas informações.|0|  
  
 Por exemplo, uma cadeia de caracteres de conexão que se conecta à fonte de dados minhaFonteDeDados usando o servidor de MyOracleServerOracle e o MyUserID de usuário do Oracle seria:  
  
```  
"DSN={MyDataSource};UID={MyUserID};PWD={MyPassword};SERVER={MyOracleServer}"  
```  
  
 Uma cadeia de caracteres de conexão que se conecta à fonte de dados MyOtherDataSource usando a autenticação do sistema operacional e o servidor de MyOtherOracleServerOracle seria:  
  
```  
"DSN=MyOtherDataSource;UID=/;PWD=;SERVER=MyOtherOracleServer"  
```
