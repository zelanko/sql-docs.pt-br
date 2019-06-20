---
title: Formato de cadeia de caracteres de Conexão e atributos | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- connection strings [ODBC], ODBC driver for Oracle
- ODBC driver for Oracle [ODBC], connection strings
ms.assetid: 0c360112-8720-4e54-a1a6-b9b18d943557
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 98c8e18432bfd386555863a917824b18b2d11885
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62902814"
---
# <a name="connection-string-format-and-attributes"></a>Atributos e formato da cadeia de conexão
> [!IMPORTANT]  
>  Este recurso será removido em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Em vez disso, use o driver ODBC fornecido pela Oracle.  
  
 Em vez de usar uma caixa de diálogo, alguns aplicativos podem exigir uma cadeia de caracteres de conexão que especifica informações de conexão de fonte de dados. A cadeia de caracteres de conexão é composta por um número de atributos que especificam como um driver se conecta a uma fonte de dados. Um atributo identifica uma parte específica de informações que o driver precisa saber antes de poder fazer a conexão de fonte de dados apropriado. Cada driver pode ter um conjunto diferente de atributos, mas o formato de cadeia de caracteres de conexão é sempre o mesmo. Uma cadeia de caracteres de conexão tem o seguinte formato:  
  
```  
"DSN=data-source-name[;SERVER=value] [;PWD=value] [;UID=value] [;<Attribute>=<value>]"  
```  
  
> [!NOTE]  
>  O Microsoft ODBC Driver for Oracle suporta o formato de cadeia de caracteres de conexão da primeira versão do driver, usada `CONNECTSTRING`= em vez de `SERVER=`.  
  
 Se você estiver se conectando a um provedor de fonte de dados que dá suporte à autenticação do Windows, você deve especificar `Trusted_Connection=yes` em vez de informações de ID e a senha do usuário na cadeia de conexão.  
  
 Você deve especificar a fonte de dados nome se você não especificar o UID, PWD, servidor (ou CONNECTSTRING) e os atributos DRIVER. No entanto, todos os outros atributos são opcionais. Se você não especificar um atributo, esse atributo padrão é aquele especificado na guia DSN de relevantes do **administrador de fonte de dados ODBC** caixa de diálogo. O valor do atributo pode diferenciar maiusculas de minúsculas.  
  
 Os atributos da cadeia de caracteres de conexão são da seguinte maneira:  
  
|attribute|Descrição|Valor padrão|  
|---------------|-----------------|-------------------|  
|DSN|O nome da fonte de dados listados na guia Drivers do **administrador de fonte de dados ODBC** caixa de diálogo.|""|  
|PWD|A senha para o servidor Oracle que você deseja acessar. Este driver suporta limitações Oracle coloca em senhas.|""|  
|SERVER|A cadeia de conexão para o servidor Oracle que você deseja acessar.|""|  
|UID|O nome de usuário do servidor Oracle. Dependendo do sistema, esse atributo não pode ser opcional – ou seja, determinadas tabelas e bancos de dados podem exigir esse atributo para fins de segurança.<br /><br /> Use "/" usar o Oracle de operação da autenticação do sistema.|""|  
|BUFFERSIZE|O tamanho ideal do buffer usado ao buscar colunas.<br /><br /> O driver otimiza a busca de forma que uma busca no servidor Oracle retorne linhas suficientes para preencher um buffer desse tamanho. Valores maiores tendem a aumentar o desempenho se você buscar muitos dados.|65535|  
|SYNONYMCOLUMNS|Quando esse valor é true (1), uma chamada à API (,) SQLColumn retornar informações de coluna. Caso contrário, (SQLColumn) retorna apenas colunas para tabelas e exibições. O Driver ODBC para Oracle fornece acesso mais rápido quando esse valor não está definido.|1|  
|REMARKS|Quando esse valor é true (1), o driver retorna colunas de comentários para o [SQLColumns](../../odbc/microsoft/level-1-api-functions-odbc-driver-for-oracle.md) conjunto de resultados. O Driver ODBC para Oracle fornece acesso mais rápido quando esse valor não está definido.|0|  
|StdDayOfWeek|Impõe o padrão ODBC para DayOfWeek. Por padrão esse é ativado, mas os usuários que precisam da versão localizada podem alterar o comportamento para usar tudo o que retorna o Oracle.|1|  
|GuessTheColDef|Especifica se o driver deve retornar um valor diferente de zero para o *cbColDef* argumento de **SQLDescribeCol**. Aplica-se somente às colunas onde houver sem escala definidas para Oracle, por exemplo, calculado numéricas colunas e as colunas definidas como número sem uma escala ou precisão. Um **SQLDescribeCol** chamar retorna 130 para a precisão quando Oracle não fornece essas informações.|0|  
  
 Por exemplo, uma cadeia de caracteres de conexão que se conecta à fonte de dados MyDataSource usando o servidor MyOracleServerOracle e o Oracle usuário MyUserID seria:  
  
```  
"DSN={MyDataSource};UID={MyUserID};PWD={MyPassword};SERVER={MyOracleServer}"  
```  
  
 Uma cadeia de caracteres de conexão que se conecta à fonte de dados MyOtherDataSource usando autenticação do sistema operacional e o servidor de MyOtherOracleServerOracle seria:  
  
```  
"DSN=MyOtherDataSource;UID=/;PWD=;SERVER=MyOtherOracleServer"  
```
