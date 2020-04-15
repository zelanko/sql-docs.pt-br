---
title: Formato e atributos da corda de conexão | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d95866976d2e83c058f83b3a0ae5e9a4e8888ed1
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81281146"
---
# <a name="connection-string-format-and-attributes"></a>Atributos e formato da cadeia de conexão
> [!IMPORTANT]  
>  Esse recurso será removido em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Em vez disso, use o driver ODBC fornecido pela Oracle.  
  
 Em vez de usar uma caixa de diálogo, alguns aplicativos podem exigir uma seqüência de conexão que especifica informações de conexão de origem de dados. A seqüência de conexões é composta por uma série de atributos que especificam como um driver se conecta a uma fonte de dados. Um atributo identifica uma informação específica que o motorista precisa saber antes de poder fazer a conexão de origem de dados apropriada. Cada driver pode ter um conjunto diferente de atributos, mas o formato de seqüência de conexões é sempre o mesmo. Uma seqüência de conexões tem o seguinte formato:  
  
```  
"DSN=data-source-name[;SERVER=value] [;PWD=value] [;UID=value] [;<Attribute>=<value>]"  
```  
  
> [!NOTE]  
>  O Microsoft ODBC Driver for Oracle suporta o formato de seqüência de conexão da primeira versão do driver, que usou `CONNECTSTRING`= em vez de `SERVER=`.  
  
 Se você estiver se conectando a um provedor de origem `Trusted_Connection=yes` de dados que suporta a autenticação do Windows, você deve especificar, em vez de Informações de ID do usuário e senha na seqüência de conexões.  
  
 Você deve especificar o nome de origem dos dados se não especificar os atributos UID, PWD, SERVER (ou CONNECTSTRING) e DRIVER. No entanto, todos os outros atributos são opcionais. Se você não especificar um atributo, esse atributo será padrão ao especificado na guia DSN relevante da caixa de diálogo Administrador de origem de **dados ODBC.** O valor do atributo pode ser sensível a maiúsculas e minúsculas.  
  
 Os atributos para a seqüência de conexões são os seguintes:  
  
|Atributo|Descrição|Valor padrão|  
|---------------|-----------------|-------------------|  
|DSN|O nome da fonte de dados listado na guia Drivers da caixa de diálogo Administrador de origem de **dados ODBC.**|""|  
|PWD|A senha para o Servidor Oracle que você deseja acessar. Este driver suporta limitações que a Oracle coloca em senhas.|""|  
|SERVER|A seqüência de conexões para o Servidor Oracle que você deseja acessar.|""|  
|UID|O nome de usuário do Oracle Server. Dependendo do seu sistema, esse atributo pode não ser opcional - ou seja, certos bancos de dados e tabelas podem exigir esse atributo para fins de segurança.<br /><br /> Use "/" para usar a autenticação do sistema operacional da Oracle.|""|  
|Buffersize|O tamanho ideal do buffer usado ao buscar colunas.<br /><br /> O driver otimiza a busca para que uma busca do Servidor Oracle retorne linhas suficientes para preencher um buffer deste tamanho. Valores maiores tendem a aumentar o desempenho se você buscar um monte de dados.|65535|  
|COLUNAS SINÔNIMOS|Quando esse valor for verdadeiro (1), uma chamada de API da SQLColumn retorna as informações da coluna. Caso contrário, sQLColumn( ) retorna apenas colunas para tabelas e visualizações. O Driver ODBC para Oracle fornece acesso mais rápido quando esse valor não é definido.|1|  
|COMENTÁRIOS|Quando esse valor for verdadeiro (1), o driver retorna colunas de observações para o conjunto de resultados [SQLColumns.](../../odbc/microsoft/level-1-api-functions-odbc-driver-for-oracle.md) O Driver ODBC para Oracle fornece acesso mais rápido quando esse valor não é definido.|0|  
|StdDayOfWeek|Impõe o padrão ODBC para o escalar DAYOFWEEK. Por padrão, isso é ligado, mas os usuários que precisam da versão localizada podem alterar o comportamento para usar o que o Oracle retornar.|1|  
|GuessTheColDef|Especifica se o driver deve ou não retornar um valor não-zero para o argumento *cbColDef* do **SQLDescribeCol**. Aplica-se apenas a colunas onde não há escala definida pelo Oracle, como colunas numéricas computadas e colunas definidas como NÚMERO sem precisão ou escala. Uma chamada **SQLDescribeCol** retorna 130 para a precisão quando a Oracle não fornece essas informações.|0|  
  
 Por exemplo, uma seqüência de conexões que se conecta à fonte de dados MyDataSource usando o MyOracleServerOracle Server e o Oracle User MyUserID seria:  
  
```  
"DSN={MyDataSource};UID={MyUserID};PWD={MyPassword};SERVER={MyOracleServer}"  
```  
  
 Uma seqüência de conexão que se conecta à fonte de dados MyOtherDataSource usando a autenticação do sistema operacional e o MyOtherOracleServerOracle Server seria:  
  
```  
"DSN=MyOtherDataSource;UID=/;PWD=;SERVER=MyOtherOracleServer"  
```
