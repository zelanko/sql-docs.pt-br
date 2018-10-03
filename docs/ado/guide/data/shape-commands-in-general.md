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
manager: craigg
ms.openlocfilehash: 1d35f549581e9ac0a12c37cef90f66969aff1659
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47633424"
---
# <a name="shape-commands-in-general"></a>Modelar comandos em geral
Formatação de dados define as colunas de uma forma **conjunto de registros**, as relações entre as entidades representadas por colunas e a maneira na qual o **Recordset** é preenchido com dados.  
  
 Um moldado **Recordset** pode conter os seguintes tipos de colunas.  
  
|Tipo de coluna|Description|  
|-----------------|-----------------|  
|data|Campos de um **conjunto de registros** retornado por um comando de consulta para um provedor de dados, tabela ou em forma de anteriormente **conjunto de registros**.|  
|Capítulo|Uma referência a outro **conjunto de registros**, chamado um *capítulo*. Colunas de capítulo tornam possível definir uma *pai-filho* relação em que o *pai* é o **Recordset** que contém a coluna de capítulo e o *filho* é o **Recordset** representado pelo capítulo.|  
|agregação|O valor da coluna é derivado, executando uma *função de agregação* em todas as linhas ou uma coluna de todas as linhas de um filho **conjunto de registros**. (Consulte as funções de agregação no tópico a seguir [funções de agregação, a função CALC e a nova palavra-chave](../../../ado/guide/data/aggregate-functions-the-calc-function-and-the-new-keyword.md).)|  
|expressão calculada|O valor da coluna é derivado, calculando um Visual Basic para a expressão de aplicativos em colunas na mesma linha dos **conjunto de registros**. A expressão é o argumento para a função CALC. (Consulte expressão calculada no tópico a seguir [funções de agregação, a função CALC e a nova palavra-chave](../../../ado/guide/data/aggregate-functions-the-calc-function-and-the-new-keyword.md) e, na [funções de aplicativos Visual Basic for](../../../ado/guide/data/visual-basic-for-applications-functions.md).)|  
|novo|Campos vazios, fabricados, que podem ser populados com dados em um momento posterior. A coluna é definida com a nova palavra-chave. (Consulte a nova palavra-chave no tópico a seguir [funções de agregação, a função CALC e a nova palavra-chave](../../../ado/guide/data/aggregate-functions-the-calc-function-and-the-new-keyword.md).)|  
  
 Um comando de forma pode conter uma cláusula que especifica um comando de consulta para um provedor de dados subjacente que retornará um **Recordset** objeto. Sintaxe da consulta depende dos requisitos do provedor de dados subjacente. Isso geralmente será SQL, embora o ADO não requer o uso de qualquer linguagem de consulta específica.  
  
 Comandos de forma podem ser emitidos por **conjunto de registros** objetos ou definindo o [CommandText](../../../ado/reference/ado-api/commandtext-property-ado.md) propriedade do [comando](../../../ado/reference/ado-api/command-object-ado.md) objeto e, em seguida, chamar o [Execute ](../../../ado/reference/ado-api/execute-method-ado-command.md) método.  
  
 Você pode usar uma cláusula SQL JOIN para relacionar duas tabelas; No entanto, um hierárquica **Recordset** pode representar as informações de forma mais eficiente. Cada linha de uma **Recordset** criado por uma informações de repetições de junção redundante de uma das tabelas. Modo hierárquico **conjunto de registros** tem apenas um pai **conjunto de registros** para cada um dos vários filho **Recordset** objetos.  
  
 Comandos de forma podem ser aninhados. Ou seja, o *comando pai* ou *comando filho* pode ser ele próprio comando de outra forma.  
  
 O provedor shape sempre retorna um cursor do cliente, mesmo quando o usuário Especifica um local do cursor do **adUseServer**.  
  
 Você pode acessar o **conjunto de registros** componentes do moldado **Recordset** programaticamente ou por meio de um controle visual apropriado.  
  
 A Microsoft fornece uma ferramenta visual que gera os comandos de forma (consulte a [dados de ambiente de Designer](http://go.microsoft.com/fwlink/?LinkId=5689) na documentação do Visual Basic 6) e outra que exibe cursores hierárquicas (consulte "usando o Microsoft hierárquica Flexgrid controle"na documentação do Visual Basic 6).  
  
 Para obter informações sobre como navegar de modo hierárquico **conjunto de registros**, consulte [acessar linhas em um conjunto de registros hierárquicos](../../../ado/guide/data/accessing-rows-in-a-hierarchical-recordset.md).  
  
 Para obter informações precisas sobre os comandos de forma sintaticamente correto, consulte [gramática Formal de forma](../../../ado/guide/data/formal-shape-grammar.md).  
  
 Esta seção contém os tópicos a seguir.  
  
-   [Funções de agregação, a função CALC e a palavra-chave NEW](../../../ado/guide/data/aggregate-functions-the-calc-function-and-the-new-keyword.md)  
  
-   [Emitindo comandos para o Provedor de Dados subjacente](../../../ado/guide/data/issuing-commands-to-the-underlying-data-provider.md)
