---
title: Comandos de forma em geral | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: guide
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- shape commands [ADO]
- data shaping [ADO], shape commands
ms.assetid: 1fac7831-a187-4b15-9b43-aad380c5556c
caps.latest.revision: "16"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: f58f3450a097d2c84de5909a8f2f6817e1274947
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="shape-commands-in-general"></a>Comandos de forma em geral
Modelagem de dados define as colunas de uma forma **registros**, as relações entre as entidades representadas pelas colunas e a maneira na qual o **registros** é preenchida com dados.  
  
 Uma forma **registros** pode consistir nos seguintes tipos de colunas.  
  
|Tipo de coluna|Description|  
|-----------------|-----------------|  
|data|Campos de um **registros** retornado por um comando de consulta para um provedor de dados, tabela ou anteriormente em forma de **registros**.|  
|Capítulo|Uma referência a outro **registros**, chamado um *capítulo*. Colunas de capítulo possibilitam definir um *pai-filho* relação onde a *pai* é o **registros** que contém a coluna de capítulo e o *filho* é o **registros** representado pelo capítulo.|  
|agregação|O valor da coluna é derivado executando um *função de agregação* em todas as linhas ou uma coluna de todas as linhas de um filho **registros**. (Consulte o tópico a seguir, as funções de agregação [funções de agregação, a função de CÁLCULO e a nova palavra-chave](../../../ado/guide/data/aggregate-functions-the-calc-function-and-the-new-keyword.md).)|  
|expressão calculada|O valor da coluna é derivado, calculando um Visual Basic para a expressão de aplicativos em colunas na mesma linha do **registros**. A expressão é o argumento para a função de CÁLCULO. (Consulte expressão calculada no tópico a seguir, [funções de agregação, a função de CÁLCULO e a nova palavra-chave](../../../ado/guide/data/aggregate-functions-the-calc-function-and-the-new-keyword.md) e em [do Visual Basic for Applications funções](../../../ado/guide/data/visual-basic-for-applications-functions.md).)|  
|novo|Campos vazios, fabricados, que podem ser preenchidos com dados em um momento posterior. A coluna é definida com a nova palavra-chave. (Consulte a nova palavra-chave no tópico a seguir, [funções de agregação, a função de CÁLCULO e a nova palavra-chave](../../../ado/guide/data/aggregate-functions-the-calc-function-and-the-new-keyword.md).)|  
  
 Um comando de forma pode conter uma cláusula que especifica um comando de consulta para um provedor de dados subjacente que retornará um **registros** objeto. Sintaxe da consulta depende dos requisitos do provedor de dados subjacente. Isso geralmente será SQL, embora o ADO não requerem o uso de qualquer linguagem de consulta específica.  
  
 Comandos de forma podem ser emitidos por **Recordset** objetos ou definindo o [CommandText](../../../ado/reference/ado-api/commandtext-property-ado.md) propriedade o [comando](../../../ado/reference/ado-api/command-object-ado.md) objeto e, em seguida, chamar o [Execute ](../../../ado/reference/ado-api/execute-method-ado-command.md) método.  
  
 Você pode usar uma cláusula JOIN do SQL para relacionar duas tabelas; No entanto, um hierárquica **registros** pode representar as informações com mais eficiência. Cada linha de um **registros** criado por um informações de repetições de junção redundante de uma das tabelas. Hierárquico **registros** tem apenas um pai **registros** para cada um dos vários filhos **registros** objetos.  
  
 Comandos de forma podem ser aninhados. Ou seja, o *comando pai* ou *filho comando* por si só pode ser outro comando de forma.  
  
 O provedor de forma sempre retorna um cursor do cliente, mesmo quando o usuário Especifica um local do cursor do **adUseServer**.  
  
 Você pode acessar o **registros** componentes com o formato **registros** programaticamente ou por meio de um controle visual apropriado.  
  
 A Microsoft fornece uma ferramenta visual que gera os comandos de forma (consulte o [dados ambiente Designer](http://go.microsoft.com/fwlink/?LinkId=5689) na documentação do Visual Basic 6) e outra que exibe cursores hierárquicas (consulte "usando o Microsoft hierárquica Flexgrid controle"na documentação do Visual Basic 6).  
  
 Para obter informações sobre como navegar hierárquico **registros**, consulte [acessar linhas em um conjunto de registros hierárquicos](../../../ado/guide/data/accessing-rows-in-a-hierarchical-recordset.md).  
  
 Para obter informações precisas sobre os comandos de forma sintaticamente correto, consulte [Formal gramática de forma](../../../ado/guide/data/formal-shape-grammar.md).  
  
 Esta seção contém os tópicos a seguir.  
  
-   [Funções de agregação, a função CALC e a palavra-chave NEW](../../../ado/guide/data/aggregate-functions-the-calc-function-and-the-new-keyword.md)  
  
-   [Emitindo comandos para o Provedor de Dados subjacente](../../../ado/guide/data/issuing-commands-to-the-underlying-data-provider.md)
