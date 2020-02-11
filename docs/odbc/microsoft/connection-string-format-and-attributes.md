---
title: Formato e atributos da cadeia de conexão | Microsoft Docs
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
ms.openlocfilehash: a007f4c7c92bf4254e4d36638cf2d92ba0764be5
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68082022"
---
# <a name="connection-string-format-and-attributes"></a>Atributos e formato da cadeia de conexão
> [!IMPORTANT]  
>  Este recurso será removido em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Em vez disso, use o driver ODBC fornecido pela Oracle.  
  
 Em vez de usar uma caixa de diálogo, alguns aplicativos podem exigir uma cadeia de conexão que especifica informações de conexão de fonte de dados. A cadeia de conexão é composta de vários atributos que especificam como um driver se conecta a uma fonte de dados. Um atributo identifica uma informação específica que o driver precisa saber antes de poder fazer a conexão de fonte de dados apropriada. Cada driver pode ter um conjunto diferente de atributos, mas o formato da cadeia de conexão é sempre o mesmo. Uma cadeia de conexão tem o seguinte formato:  
  
```  
"DSN=data-source-name[;SERVER=value] [;PWD=value] [;UID=value] [;<Attribute>=<value>]"  
```  
  
> [!NOTE]  
>  O Microsoft ODBC driver for Oracle dá suporte ao formato de cadeia de conexão da primeira versão do driver, que `CONNECTSTRING`usou = em `SERVER=`vez de.  
  
 Se você estiver se conectando a um provedor de fonte de dados que dá suporte à `Trusted_Connection=yes` autenticação do Windows, especifique o lugar das informações de ID de usuário e senha na cadeia de conexão.  
  
 Você deve especificar o nome da fonte de dados se não especificar os atributos UID, PWD, SERVER (ou CONNECTstring) e DRIVER. No entanto, todos os outros atributos são opcionais. Se você não especificar um atributo, esse atributo será padronizado para aquele especificado na guia DSN relevante da caixa de diálogo **administrador de fonte de dados ODBC** . O valor do atributo pode diferenciar maiúsculas de minúsculas.  
  
 Os atributos da cadeia de conexão são os seguintes:  
  
|Atributo|DESCRIÇÃO|Valor padrão|  
|---------------|-----------------|-------------------|  
|DSN|O nome da fonte de dados listada na guia Drivers da caixa de diálogo **administrador de fonte de dados ODBC** .|""|  
|PWD|A senha do servidor Oracle que você deseja acessar. Esse driver dá suporte a limitações que o Oracle coloca em senhas.|""|  
|SERVER|A cadeia de conexão para o servidor Oracle que você deseja acessar.|""|  
|UID|O nome de usuário do servidor Oracle. Dependendo do seu sistema, esse atributo pode não ser opcional, ou seja, determinados bancos de dados e tabelas podem exigir esse atributo para fins de segurança.<br /><br /> Use "/" para usar a autenticação do sistema operacional da Oracle.|""|  
|BUFFERSIZE|O tamanho de buffer ideal usado ao buscar colunas.<br /><br /> O driver otimiza a busca para que uma busca do servidor Oracle retorne linhas suficientes para preencher um buffer desse tamanho. Valores maiores tendem a aumentar o desempenho se você buscar muitos dados.|65535|  
|SYNONYMCOLUMNS|Quando esse valor é true (1), uma chamada à API sqlcolumn () retorna informações de coluna. Caso contrário, sqlcolumn () retornará apenas colunas para tabelas e exibições. O ODBC driver for Oracle fornece acesso mais rápido quando esse valor não é definido.|1|  
|COMENTÁRIOS|Quando esse valor é true (1), o driver retorna colunas de comentários para o conjunto de resultados [SQLColumns](../../odbc/microsoft/level-1-api-functions-odbc-driver-for-oracle.md) . O ODBC driver for Oracle fornece acesso mais rápido quando esse valor não é definido.|0|  
|StdDayOfWeek|Impõe o padrão ODBC para a Scalar DAYOFWEEK. Por padrão, isso é ativado, mas os usuários que precisam da versão localizada podem alterar o comportamento para usar qualquer retorno do Oracle.|1|  
|GuessTheColDef|Especifica se o driver deve ou não retornar um valor diferente de zero para o argumento *cbColDef* de **SQLDescribeCol**. Aplica-se somente a colunas em que não há nenhuma escala definida pelo Oracle, como colunas numéricas computadas e colunas definidas como número sem precisão ou escala. Uma chamada **SQLDescribeCol** retorna 130 para a precisão quando o Oracle não fornece essas informações.|0|  
  
 Por exemplo, uma cadeia de conexão que se conecta à fonte de dados mydatary usando o servidor MyOracleServerOracle e o usuário Oracle myuserid seria:  
  
```  
"DSN={MyDataSource};UID={MyUserID};PWD={MyPassword};SERVER={MyOracleServer}"  
```  
  
 Uma cadeia de conexão que se conecta à fonte de dados MyOtherDataSource usando a autenticação do sistema operacional e o servidor MyOtherOracleServerOracle seria:  
  
```  
"DSN=MyOtherDataSource;UID=/;PWD=;SERVER=MyOtherOracleServer"  
```
