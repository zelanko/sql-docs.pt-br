---
title: Propriedade de filtro | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 03/20/2018
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::Filter
helpviewer_keywords:
- Filter property
ms.assetid: 80263a7a-5d21-45d1-84fc-34b7a9be4c22
author: rothja
ms.author: jroth
ms.openlocfilehash: bcc1b02671d73e9056babb417ba2fa22a4d6cf0e
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2020
ms.locfileid: "82762537"
---
# <a name="filter-property"></a>Propriedade Filter
Indica um filtro para dados em um [conjunto de registros](../../../ado/reference/ado-api/recordset-object-ado.md).  
  
## <a name="settings-and-return-values"></a>Configurações e valores de retorno

Define ou retorna um valor **Variant** , que pode conter um dos seguintes itens:  
  
-   **Cadeia de critérios:** Uma cadeia de caracteres composta por uma ou mais cláusulas individuais concatenadas com operadores **and** ou **or** .  
  
-   **Matriz de indicadores:** Uma matriz de valores de indicador exclusivos que apontam para registros no objeto **Recordset** .  
  
-   Um valor de [FilterGroupEnum](../../../ado/reference/ado-api/filtergroupenum.md) .  
  
## <a name="remarks"></a>Comentários

Use a propriedade **Filter** para desconectar seletivamente os registros em um objeto **Recordset** . O **conjunto de registros** filtrado se torna o cursor atual. Outras propriedades que retornam valores com base no **cursor** atual são afetadas, como a [propriedade AbsolutePosition (ADO)](../../../ado/reference/ado-api/absoluteposition-property-ado.md), a [Propriedade AbsolutePage (ADO)](../../../ado/reference/ado-api/absolutepage-property-ado.md), a [Propriedade RecordCount (ADO)](../../../ado/reference/ado-api/recordcount-property-ado.md)e a [Propriedade PageCount (ADO)](../../../ado/reference/ado-api/pagecount-property-ado.md). A definição da propriedade **Filter** para um novo valor específico move o registro atual para o primeiro registro que satisfaz o novo valor.
  
A cadeia de caracteres de critérios é composta de cláusulas no formato *FieldName-Operator-Value* (por exemplo, `"LastName = 'Smith'"` ). Você pode criar cláusulas compostas concatenando cláusulas individuais com **and** (por exemplo, `"LastName = 'Smith' AND FirstName = 'John'"` ) **OR** ou (por exemplo, `"LastName = 'Smith' OR LastName = 'Jones'"` ). Para cadeias de caracteres de critérios, use as seguintes diretrizes:

-   *FieldName* deve ser um nome de campo válido do **conjunto de registros**. Se o nome do campo contiver espaços, você deverá colocar o nome entre colchetes.  
  
-   O operador deve ser um dos seguintes: \< , >, \< =, >=,  <>, = ou **like**.  
  
-   Valor é o valor com o qual você vai comparar os valores de campo (por exemplo, ' Smith ', #8/24/95 #, 12,345 ou $50). Use aspas simples com cadeias de caracteres e sinais de sustenido (#) com datas. Para números, você pode usar pontos decimais, sinais de dólar e notação científica. Se o operador for **como**, o valor poderá usar curingas. Somente o asterisco (*) e o sinal de porcentagem (%) curingas são permitidos e devem ser o último caractere na cadeia de caracteres. O valor não pode ser nulo.  
  
> [!NOTE]
>  Para incluir aspas simples (') no valor do filtro, use duas aspas simples para representar uma. Por exemplo, para filtrar em ' Malley, a cadeia de caracteres de critérios deve ser `"col1 = 'O''Malley'"` . Para incluir aspas simples no início e no final do valor do filtro, coloque a cadeia de caracteres com sinais de sustenido (#). Por exemplo, para filtrar em ' 1 ', a cadeia de caracteres de critérios deve ser `"col1 = #'1'#"` .  
  
-   Não há precedência entre e e ou. As cláusulas podem ser agrupadas entre parênteses. No entanto, você não pode agrupar cláusulas Unidas por um ou e depois unir o grupo a outra cláusula com um e, como no seguinte trecho de código:  
 `(LastName = 'Smith' OR LastName = 'Jones') AND FirstName = 'John'`  
  
-   Em vez disso, você criaria esse filtro como  
 `(LastName = 'Smith' AND FirstName = 'John') OR (LastName = 'Jones' AND FirstName = 'John')`  
  
-   Em uma cláusula **like** , você pode usar um caractere curinga no início e no final do padrão. Por exemplo, você pode usar `LastName Like '*mit*'`. Ou com **like** , você pode usar um caractere curinga somente no final do padrão. Por exemplo, `LastName Like 'Smit*'`.  
  
 As constantes de filtro facilitam a resolução de conflitos de registro individuais durante o modo de atualização do lote, permitindo que você exiba, por exemplo, somente os registros que foram afetados durante a última chamada do método de [método UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md) .  
  
A definição da própria propriedade de **filtro** pode falhar devido a um conflito com os dados subjacentes. Por exemplo, essa falha pode ocorrer quando um registro já foi excluído por outro usuário. Nesse caso, o provedor retorna avisos para a coleção de [erros Collection (ADO)](../../../ado/reference/ado-api/errors-collection-ado.md) , mas não interrompe a execução do programa. Um erro no tempo de execução ocorrerá somente se houver conflitos em todos os registros solicitados. Use a propriedade [status (ADO Recordset)](../../../ado/reference/ado-api/status-property-ado-recordset.md) para localizar registros com conflitos.  
  
Definir a propriedade **Filter** para uma cadeia de caracteres de comprimento zero ("") tem o mesmo efeito que usar a constante **adFilterNone** .
  
Sempre que a propriedade **Filter** é definida, a posição do registro atual é movida para o primeiro registro no subconjunto filtrado de registros no **conjunto de registros**. Da mesma forma, quando a propriedade **Filter** é desmarcada, a posição do registro atual é movida para o primeiro registro no **conjunto de registros**.

Suponha que um **conjunto de registros** seja filtrado com base em um campo de algum tipo Variant, como o tipo sql_variant. Um erro (DISP_E_TYPEMISMATCH ou 80020005) ocorre quando os subtipos dos valores de campo e filtro usados na cadeia de caracteres de critérios não correspondem. Por exemplo, suponha:

- Um objeto **Recordset** (RS) contém uma coluna (C) do tipo sql_variant.
- E um campo dessa coluna foi atribuído a um valor de 1 do tipo i4. A cadeia de caracteres de critérios é definida como `rs.Filter = "C='A'"` no campo.

Essa configuração produz o erro durante o tempo de execução. No entanto, `rs.Filter = "C=2"` aplica-se ao mesmo campo não produzirá nenhum erro. E o campo é filtrado fora do conjunto de registros atual.

Consulte a propriedade de [propriedade de indicador (ADO)](../../../ado/reference/ado-api/bookmark-property-ado.md) para obter uma explicação dos valores de indicador dos quais você pode criar uma matriz para usar com a propriedade de filtro.

Somente filtros na forma de cadeias de caracteres de critérios afetam o conteúdo de um **conjunto de registros**persistente. Um exemplo de uma cadeia de caracteres de critérios é `OrderDate > '12/31/1999'` . Os filtros criados com uma matriz de indicadores, ou usando um valor de **FilterGroupEnum**, não afetam o conteúdo do **conjunto de registros**persistente. Essas regras se aplicam a conjuntos de registros criados com cursores do lado do cliente ou do servidor.
  
> [!NOTE]
>  Quando você aplicar o sinalizador adFilterPendingRecords a um **conjunto de registros** filtrado e modificado no modo de atualização do lote, o **conjunto de registros** resultante estará vazio se a filtragem tiver sido baseada no campo de chave de uma tabela com chaves únicas e a modificação tiver sido feita nos valores do campo de chave. O conjunto de **registros** resultante será não vazio se uma das seguintes instruções for verdadeira:  
  
-   A filtragem foi baseada em campos não-chave em uma tabela de chave única.  
  
-   A filtragem foi baseada em qualquer campo em uma tabela com várias chave.  
  
-   Foram feitas modificações em campos não-chave em uma tabela de chave única.  
  
-   Foram feitas modificações em todos os campos em uma tabela com várias chave.  
  
A tabela a seguir resume os efeitos de **adFilterPendingRecords** em diferentes combinações de filtragem e modificações. A coluna à esquerda mostra as possíveis modificações. As modificações podem ser feitas em qualquer um dos campos não chaveada, no campo de chave em uma tabela com chave única ou em qualquer um dos campos de chave em uma tabela com várias chaves. A linha superior mostra o critério de filtragem. A filtragem pode ser baseada em qualquer um dos campos não chaveada, no campo de chave em uma tabela com chave única ou em qualquer um dos campos de chave em uma tabela com várias chaves. As células de interseção mostram os resultados. Um **+** sinal de adição significa que a aplicação de resultados de **adFilterPendingRecords** em um **conjunto de registros**não vazio. Um **-** sinal de subtração significa um **conjunto de registros**vazio.  
  
||Não chaves|Chave única|Várias chaves|
|-|--------------|----------------|-------------------|
|**Não chaves**|+|+|+|
|**Chave única**|+|-|N/D|
|**Várias chaves**|+|N/D|+|
|||||
  
## <a name="applies-to"></a>Aplica-se A

[Objeto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Consulte Também

[Exemplo das propriedades Filter e RecordCount (VB)](../../../ado/reference/ado-api/filter-and-recordcount-properties-example-vb.md) 
 [Exemplo das propriedades Filter e RecordCount (VC + +)](../../../ado/reference/ado-api/filter-and-recordcount-properties-example-vc.md) 
 [Método Clear (ADO)](../../../ado/reference/ado-api/clear-method-ado.md) 
 [Otimizar propriedade-dinâmica (ADO)](../../../ado/reference/ado-api/optimize-property-dynamic-ado.md)
