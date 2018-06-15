---
title: Operação de comandos parametrizados | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- data shaping [ADO], parameterized commands
- parameterized commands [ADO]
ms.assetid: 4fae0d54-83b6-4ead-99cc-bcf532daa121
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ea5f45e5f7fa1b60bb9f6b4884fcb1e480534d00
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/11/2018
ms.locfileid: "35272165"
---
# <a name="operation-of-parameterized-commands"></a>Operação de comandos com parâmetros
Se você estiver trabalhando com um grande filho **registros**, especialmente em comparação com o tamanho do pai **registros**, mas que precisam acessar apenas alguns capítulos de filho, talvez seja mais eficiente usar um comando com parâmetros.  
  
 Um *comando sem parâmetros* recupera todo pai e filho **conjuntos de registros**, acrescente uma coluna de capítulo ao pai e, em seguida, atribui uma referência para o capítulo filhos relacionados para cada linha pai .  
  
 Um *comando com parâmetros* recupera o pai inteiro **registros**, mas recupera apenas o capítulo **registros** quando a coluna de capítulo é acessada. Essa diferença na estratégia de recuperação pode gerar benefícios significativos de desempenho.  
  
 Por exemplo, você pode especificar o seguinte:  
  
```  
SHAPE {SELECT * FROM customer}   
   APPEND ({SELECT * FROM orders WHERE cust_id = ?}   
   RELATE cust_id TO PARAMETER 0)  
```  
  
 As tabelas pai e filho têm um nome de coluna em comum, cust_id *.* O *filho comando* tem um "?" espaço reservado, ao qual se refere a cláusula RELATE (ou seja, "... PARÂMETRO 0").  
  
> [!NOTE]
>  A cláusula de parâmetro referem-se exclusivamente para a sintaxe de comando de forma. Ele não está associado com o ADO [parâmetro](../../../ado/reference/ado-api/parameter-object.md) objeto ou o [parâmetros](../../../ado/reference/ado-api/parameters-collection-ado.md) coleção.  
  
 Quando o comando de forma com parâmetros é executado, ocorre o seguinte:  
  
1.  O *comando pai* é executada e retorna um pai **registros** da tabela Customers.  
  
2.  Uma coluna de capítulo é acrescentada ao pai **registros**.  
  
3.  Quando a coluna de capítulo de uma linha pai é acessada, o *filho comando* é executado usando o valor de customer.cust_id como o valor do parâmetro.  
  
4.  Todas as linhas no conjunto de linhas do provedor de dados criado na etapa 3 são usadas para preencher o filho **registros**. Neste exemplo, que é de todas as linhas na tabela na qual o cust_id igual ao valor de customer.cust_id. Por padrão, o filho **registros**s serão armazenados em cache até que todas as referências para o pai **registros** são liberados. Para alterar esse comportamento, defina o **registros** [propriedades dinâmicas](../../../ado/reference/ado-api/ado-dynamic-property-index.md) **linhas filho de Cache** para **False**.  
  
5.  Uma referência para as linhas filho recuperada (ou seja, o capítulo do filho **registros**) é colocado na coluna de capítulo da linha atual do pai **registros**.  
  
6.  As etapas 3 a 5 são repetidas quando a coluna de capítulo de outra linha é acessada.  
  
 O **linhas filho de Cache** dinâmico está definida como **True** por padrão. O comportamento do cache varia de acordo com os valores dos parâmetros da consulta. Em uma consulta com um único parâmetro, o filho **registros** para um determinado parâmetro valor será armazenada na cache entre solicitações para um filho com esse valor. O código a seguir demonstra isso:  
  
```  
SCmd = "SHAPE {select * from customer} " & _  
         "APPEND({select * from orders where cust_id = ?} " & _  
         "RELATE cust_id TO PARAMETER 0) AS chpCustOrder"  
Rst1.Open sCmd, Cnn1  
Set RstChild = Rst1("chpCustOrder").Value  
Rst1.MoveNext      ' Next cust_id passed to Param 0, & new rs fetched   
                   ' into RstChild.  
Rst1.MovePrevious  ' RstChild now holds cached rs, saving round trip.  
```  
  
 Em uma consulta com dois ou mais parâmetros, um filho em cache é usado somente se todos os valores de parâmetro correspondem aos valores armazenados em cache.  
  
## <a name="parameterized-commands-and-complex-parent-child-relations"></a>Relações de filho do pai complexos e comandos parametrizados  
 Além de usar os comandos com parâmetros para melhorar o desempenho de uma hierarquia de tipo de junção de igualdade, os comandos com parâmetros podem ser usados para oferecer suporte a relações pai-filho mais complexas. Por exemplo, considere um banco de dados pouco liga com duas tabelas: consiste as equipes (team_id, team_name) e o outro de jogos (data, home_team, visiting_team).  
  
 Uso de uma hierarquia sem parâmetros, não é possível relacionar as tabelas de equipes e jogos de forma que o filho **registros** para cada equipe contém sua programação completa. Você pode criar capítulos que contêm a agenda inicial ou a agenda de estrada, mas não ambos. Isso ocorre porque a cláusula RELATE limita você a relações pai-filho do formulário (pc1 = cc1) e (pc2 = pc2). Portanto, se o comando inclui "Relacionar team_id para home_team, team_id para visiting_team", você obterá apenas jogos onde uma equipe de execução em si. O que você deseja é "(team_id=home_team) ou (team_id = visiting_team)", mas o provedor de forma não dá suporte a cláusula OR.  
  
 Para obter o resultado desejado, você pode usar um comando com parâmetros. Por exemplo:  
  
```  
SHAPE {SELECT * FROM teams}   
APPEND ({SELECT * FROM games WHERE home_team = ? OR visiting_team = ?}   
        RELATE team_id TO PARAMETER 0,   
               team_id TO PARAMETER 1)   
```  
  
 Este exemplo explora a maior flexibilidade de uma cláusula SQL WHERE para obter o resultado que necessário.  
  
> [!NOTE]
>  Quando usar as cláusulas WHERE, parâmetros não podem usar os tipos de dados SQL para text, ntext e image ou ocorrerá um erro que contém a seguinte descrição: `Invalid operator for data type`.  
  
## <a name="see-also"></a>Consulte também  
 [Exemplo de modelagem de dados](../../../ado/guide/data/data-shaping-example.md)   
 [Gramática de forma formal](../../../ado/guide/data/formal-shape-grammar.md)   
 [Modelar comandos em geral](../../../ado/guide/data/shape-commands-in-general.md)
