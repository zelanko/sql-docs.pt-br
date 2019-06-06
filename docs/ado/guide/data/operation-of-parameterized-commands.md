---
title: Operação de comandos parametrizados | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- data shaping [ADO], parameterized commands
- parameterized commands [ADO]
ms.assetid: 4fae0d54-83b6-4ead-99cc-bcf532daa121
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 4001ac5b449609683293cd3174dc4410cabf4c4b
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/05/2019
ms.locfileid: "66701867"
---
# <a name="operation-of-parameterized-commands"></a>Operação de comandos parametrizados
Se você estiver trabalhando com um grande filho **conjunto de registros**, especialmente se comparado ao tamanho do pai **conjunto de registros**, mas que precisam acessar apenas poucos capítulos de filho, você talvez ache mais eficiente usar um comando parametrizado.  
  
 Um *sem parâmetros de comando* recupera todo pai e filho **conjuntos de registros**, acrescente uma coluna de capítulo para o pai e, em seguida, atribui uma referência para o capítulo filho relacionados para cada linha pai .  
  
 Um *comando com parâmetros* recupera o pai inteiro **conjunto de registros**, mas recupera somente o capítulo **Recordset** quando a coluna de capítulo é acessada. Essa diferença na estratégia de recuperação pode proporcionar benefícios de desempenho significativa.  
  
 Por exemplo, você pode especificar o seguinte:  
  
```  
SHAPE {SELECT * FROM customer}   
   APPEND ({SELECT * FROM orders WHERE cust_id = ?}   
   RELATE cust_id TO PARAMETER 0)  
```  
  
 As tabelas pai e filho têm um nome de coluna em comum, cust_id *.* O *comando filho* tem um "?" espaço reservado, ao qual se refere a cláusula RELATE (ou seja, "... PARÂMETRO 0").  
  
> [!NOTE]
>  A cláusula de parâmetro está relacionado exclusivamente a sintaxe do comando de forma. Ele não está associado com o ADO [parâmetro](../../../ado/reference/ado-api/parameter-object.md) objeto ou o [parâmetros](../../../ado/reference/ado-api/parameters-collection-ado.md) coleção.  
  
 Quando o comando de forma com parâmetros é executado, ocorre o seguinte:  
  
1.  O *comando pai* é executada e retorna um pai **conjunto de registros** da tabela Customers.  
  
2.  Uma coluna de capítulo é acrescentada ao pai **conjunto de registros**.  
  
3.  Quando a coluna de capítulo de uma linha pai é acessada, o *comando filho* é executado usando o valor da customer.cust_id como o valor do parâmetro.  
  
4.  Todas as linhas no conjunto de linhas do provedor de dados criado na etapa 3 são usadas para preencher o filho **conjunto de registros**. Neste exemplo, que é de todas as linhas na tabela de pedidos em que o cust_id igual ao valor de customer.cust_id. Por padrão, o filho **conjunto de registros**s será ser armazenado em cache no cliente até que todas as referências ao pai **Recordset** são liberados. Para alterar esse comportamento, defina as **conjunto de registros** [propriedade dinâmica](../../../ado/reference/ado-api/ado-dynamic-property-index.md) **linhas filho de Cache** para **False**.  
  
5.  Uma referência para as linhas filho recuperados (ou seja, o capítulo do filho **conjunto de registros**) é colocado na coluna de capítulo da linha atual do pai **conjunto de registros**.  
  
6.  As etapas 3 a 5 são repetidas quando a coluna de capítulo de outra linha é acessada.  
  
 O **linhas filho de Cache** dinâmico estiver definida como **verdadeiro** por padrão. O comportamento de cache varia de acordo com os valores de parâmetro da consulta. Em uma consulta com um único parâmetro, o filho **Recordset** para um determinado parâmetro valor será ser armazenado em cache entre as solicitações para uma criança com esse valor. O código a seguir demonstra isso:  
  
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
  
## <a name="parameterized-commands-and-complex-parent-child-relations"></a>Comandos parametrizados e relações de filho de pai complexos  
 Além de usar comandos parametrizados para melhorar o desempenho de uma hierarquia de tipo de junção de igualdade, os comandos com parâmetros podem ser usados para dar suporte a relações de pai-filho mais complexas. Por exemplo, considere um banco de dados de liga pequena com duas tabelas: consiste as equipes (team_id, team_name) e o outro de jogos (data, home_team, visiting_team).  
  
 Usando uma hierarquia sem parâmetros, há nenhuma maneira para relacionar as tabelas de jogos e equipes de tal forma que o filho **Recordset** para cada equipe contém sua agenda completa. Você pode criar capítulos que contêm a agenda inicial ou a agenda de estrada, mas não ambos. Isso ocorre porque a cláusula RELATE limita você a relações pai-filho do formulário (pc1 = cc1) AND (pc2 = pc2). Portanto, se o comando inclui "Relacionar team_id TO home_team, team_id TO visiting_team", você obteria apenas jogos onde uma equipe estava jogando em si. O que você deseja é "(team_id=home_team) ou (team_id = visiting_team)", mas o provedor de forma não oferece suporte a cláusula OR.  
  
 Para obter o resultado desejado, você pode usar um comando com parâmetros. Por exemplo:  
  
```  
SHAPE {SELECT * FROM teams}   
APPEND ({SELECT * FROM games WHERE home_team = ? OR visiting_team = ?}   
        RELATE team_id TO PARAMETER 0,   
               team_id TO PARAMETER 1)   
```  
  
 Este exemplo explora a maior flexibilidade da cláusula SQL WHERE para obter o resultado que necessário.  
  
> [!NOTE]
>  Quando usar as cláusulas WHERE, parâmetros não podem usar os tipos de dados SQL para text, ntext e image ou ocorrerá um erro que contém a seguinte descrição: `Invalid operator for data type`.  
  
## <a name="see-also"></a>Consulte também  
 [Exemplo de Data Shaping](../../../ado/guide/data/data-shaping-example.md)   
 [Gramática de forma formal](../../../ado/guide/data/formal-shape-grammar.md)   
 [Modelar comandos em geral](../../../ado/guide/data/shape-commands-in-general.md)
