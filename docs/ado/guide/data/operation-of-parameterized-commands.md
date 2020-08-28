---
description: Operação de comandos parametrizados
title: Operação de comandos com parâmetros | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- data shaping [ADO], parameterized commands
- parameterized commands [ADO]
ms.assetid: 4fae0d54-83b6-4ead-99cc-bcf532daa121
author: rothja
ms.author: jroth
ms.openlocfilehash: 91fe315304cc2be0ccfb8c638665ce699c75e248
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88980167"
---
# <a name="operation-of-parameterized-commands"></a>Operação de comandos parametrizados
Se você estiver trabalhando com um conjunto de **registros**filho grande, especialmente comparado ao tamanho do **conjunto de registros**pai, mas precisar acessar apenas alguns capítulos filhos, poderá achar mais eficiente usar um comando com parâmetros.  
  
 Um *comando não parametrizado* recupera todos os **conjuntos de registros**pai e filho, acrescenta uma coluna de capítulo ao pai e atribui uma referência ao capítulo filho relacionado para cada linha pai.  
  
 Um *comando com parâmetros* recupera todo o **conjunto de registros**pai, mas recupera somente o **conjunto de registros** do capítulo quando a coluna de capítulo é acessada. Essa diferença na estratégia de recuperação pode gerar benefícios de desempenho significativos.  
  
 Por exemplo, você pode especificar o seguinte:  
  
```  
SHAPE {SELECT * FROM customer}   
   APPEND ({SELECT * FROM orders WHERE cust_id = ?}   
   RELATE cust_id TO PARAMETER 0)  
```  
  
 As tabelas pai e filho têm um nome de coluna em comum, *Cust_ID*. O *comando filho* tem um espaço reservado "?", ao qual a cláusula relate se refere (ou seja, "... PARÂMETRO 0 ").  
  
> [!NOTE]
>  A cláusula de parâmetro pertence exclusivamente à sintaxe de comando de forma. Ele não está associado ao objeto de [parâmetro](../../reference/ado-api/parameter-object.md) do ADO ou à coleção de [parâmetros](../../reference/ado-api/parameters-collection-ado.md) .  
  
 Quando o comando de forma com parâmetros é executado, ocorre o seguinte:  
  
1.  O *comando pai* é executado e retorna um conjunto de **registros** pai da tabela Customers.  
  
2.  Uma coluna de capítulo é anexada ao **conjunto de registros**pai.  
  
3.  Quando a coluna de capítulo de uma linha pai é acessada, o *comando filho* é executado usando o valor de customer. Cust_ID como o valor do parâmetro.  
  
4.  Todas as linhas no conjunto de linhas do provedor de dados criado na etapa 3 são usadas para preencher o **conjunto de registros**filho. Neste exemplo, são todas as linhas na tabela Orders em que o cust_id é igual ao valor de Customer. cust_id. Por padrão, os s **conjuntos de registros**filho serão armazenados em cache no cliente até que todas as referências ao **conjunto de registros** pai sejam liberadas. Para alterar esse comportamento, defina as **linhas filho do cache** de [propriedade dinâmica](../../reference/ado-api/ado-dynamic-property-index.md) do **conjunto de registros** como **false**.  
  
5.  Uma referência às linhas filho recuperadas (ou seja, o capítulo do conjunto de **registros**filho) é colocada na coluna capítulo da linha atual do **conjunto de registros**pai.  
  
6.  As etapas 3-5 são repetidas quando a coluna de capítulo de outra linha é acessada.  
  
 A propriedade dinâmica de **linhas filhas de cache** é definida como **true** por padrão. O comportamento de cache varia dependendo dos valores de parâmetro da consulta. Em uma consulta com um único parâmetro, o **conjunto de registros** filho para um determinado valor de parâmetro será armazenado em cache entre as solicitações de um filho com esse valor. O código a seguir demonstra isso:  
  
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
  
 Em uma consulta com dois ou mais parâmetros, um filho armazenado em cache será usado somente se todos os valores de parâmetro corresponderem aos valores armazenados em cache.  
  
## <a name="parameterized-commands-and-complex-parent-child-relations"></a>Comandos com parâmetros e relações de filho pai complexas  
 Além de usar comandos com parâmetros para melhorar o desempenho de uma hierarquia de tipo de junção de equivalência, comandos com parâmetros podem ser usados para dar suporte a relações pai-filho mais complexas. Por exemplo, considere um pequeno banco de dados de League com duas tabelas: uma consistindo nas equipes (team_id, team_name) e a outra de jogos (data, home_team visiting_team).  
  
 Usando uma hierarquia sem parâmetros, não há como relacionar as tabelas de equipes e jogos de forma que o **conjunto de registros** filho de cada equipe contenha sua programação completa. Você pode criar capítulos que contenham a agenda inicial ou a agenda de estrada, mas não ambos. Isso ocorre porque a cláusula relate limita você a relações pai-filho do formulário (Altova = cc1) e (PC2 = PC2). Portanto, se o comando tiver incluído "RELACIONAr team_id a home_team, team_id para visiting_team", você obterá apenas jogos em que a equipe estava jogando. O que você deseja é "(team_id = home_team) ou (team_id = visiting_team)", mas o provedor de forma não oferece suporte à cláusula OR.  
  
 Para obter o resultado desejado, você pode usar um comando com parâmetros. Por exemplo:  
  
```  
SHAPE {SELECT * FROM teams}   
APPEND ({SELECT * FROM games WHERE home_team = ? OR visiting_team = ?}   
        RELATE team_id TO PARAMETER 0,   
               team_id TO PARAMETER 1)   
```  
  
 Este exemplo explora a maior flexibilidade da cláusula WHERE do SQL para obter o resultado necessário.  
  
> [!NOTE]
>  Ao usar cláusulas WHERE, os parâmetros não podem usar os tipos de dados do SQL para Text, ntext e Image, ou um erro resultará em conter a seguinte descrição: `Invalid operator for data type` .  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo de formatação de dados](./data-shaping-example.md)   
 [Gramática forma formal](./formal-shape-grammar.md)   
 [Modelar comandos em geral](./shape-commands-in-general.md)