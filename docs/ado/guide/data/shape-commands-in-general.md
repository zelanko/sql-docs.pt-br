---
title: Comandos de forma em geral | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- shape commands [ADO]
- data shaping [ADO], shape commands
ms.assetid: 1fac7831-a187-4b15-9b43-aad380c5556c
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 09fec8bd07d036fd6a93b8f6bcb54a51a68150fa
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67924171"
---
# <a name="shape-commands-in-general"></a>Modelar comandos em geral
O data Shaping define as colunas de um **conjunto de registros**moldado, as relações entre as entidades representadas pelas colunas e a maneira como o **conjunto de registros** é preenchido com os dados.  
  
 Um **conjunto de registros** moldado pode consistir nos seguintes tipos de colunas.  
  
|Tipo de coluna|DESCRIÇÃO|  
|-----------------|-----------------|  
|data|Campos de um **conjunto de registros** retornado por um comando de consulta para um provedor de dados, uma tabela ou um **conjunto de registros**moldado anteriormente.|  
|6|Uma referência a outro **conjunto de registros**, chamada de *capítulo*. As colunas de capítulo possibilitam definir uma relação *pai-filho* em que o *pai* é o **conjunto de registros** que contém a coluna de capítulo e o *filho* é o conjunto de **registros** representado pelo capítulo.|  
|aggregate|O valor da coluna é derivado pela execução de uma *função de agregação* em todas as linhas ou em uma coluna de todas as linhas de um **conjunto de registros**filho. (Consulte funções de agregação no tópico a seguir, [funções de agregação, a função Calc e a nova palavra-chave](../../../ado/guide/data/aggregate-functions-the-calc-function-and-the-new-keyword.md).)|  
|expressão calculada|O valor da coluna é derivado ao calcular uma expressão de Visual Basic for Applications em colunas na mesma linha do conjunto de **registros**. A expressão é o argumento para a função CALC. (Consulte a expressão calculada no tópico a seguir, [funções de agregação, a função Calc e a nova palavra-chave](../../../ado/guide/data/aggregate-functions-the-calc-function-and-the-new-keyword.md) e em [funções Visual Basic for Applications](../../../ado/guide/data/visual-basic-for-applications-functions.md).)|  
|novo|Campos vazios, criei, que podem ser preenchidos com dados posteriormente. A coluna é definida com a nova palavra-chave. (Consulte a nova palavra-chave no tópico a seguir, [funções de agregação, a função Calc e a nova palavra-chave](../../../ado/guide/data/aggregate-functions-the-calc-function-and-the-new-keyword.md).)|  
  
 Um comando Shape pode conter uma cláusula que especifica um comando de consulta para um provedor de dados subjacente que retornará um objeto **Recordset** . A sintaxe da consulta depende dos requisitos do provedor de dados subjacente. Isso geralmente será SQL, embora o ADO não exija o uso de nenhuma linguagem de consulta específica.  
  
 Os comandos de forma podem ser emitidos por objetos **Recordset** ou definindo a propriedade [CommandText](../../../ado/reference/ado-api/commandtext-property-ado.md) do objeto [Command](../../../ado/reference/ado-api/command-object-ado.md) e, em seguida, chamando o método [Execute](../../../ado/reference/ado-api/execute-method-ado-command.md) .  
  
 Você pode usar uma cláusula SQL JOIN para relacionar duas tabelas; no entanto, um **conjunto de registros** hierárquico pode representar as informações com mais eficiência. Cada linha de um **conjunto de registros** criado por uma junção repete as informações de forma redundante de uma das tabelas. Um **conjunto de registros** hierárquico tem apenas um **conjunto de registros** pai para cada um dos vários objetos filho do conjunto de **registros** .  
  
 Os comandos de forma podem ser aninhados. Ou seja, o comando *pai* ou *filho-Command* pode ser um outro comando de forma.  
  
 O provedor Shape sempre retorna um cursor do cliente, mesmo quando o usuário especifica um local de cursor de **adUseServer**.  
  
 Você pode acessar os componentes do **conjunto** de **registros** com formato programaticamente ou por meio de um controle visual apropriado.  
  
 A Microsoft fornece uma ferramenta visual que gera comandos de forma (consulte o [Designer de ambiente de dados](https://go.microsoft.com/fwlink/?LinkId=5689) na documentação do Visual Basic 6) e outro que exibe cursores hierárquicos (consulte "usando o controle de FlexGrid hierárquico da Microsoft" na documentação do Visual Basic 6).  
  
 Para obter informações sobre como navegar em um **conjunto de registros**hierárquico, consulte [acessando linhas em um conjunto de registros hierárquico](../../../ado/guide/data/accessing-rows-in-a-hierarchical-recordset.md).  
  
 Para obter informações precisas sobre os comandos de forma sintaticamente corretos, consulte [gramática formal de forma](../../../ado/guide/data/formal-shape-grammar.md).  
  
 Esta seção contém os seguintes tópicos:  
  
-   [Funções de agregação, a função CALC e a palavra-chave NEW](../../../ado/guide/data/aggregate-functions-the-calc-function-and-the-new-keyword.md)  
  
-   [Emitir comandos para o Provedor de Dados subjacente](../../../ado/guide/data/issuing-commands-to-the-underlying-data-provider.md)
