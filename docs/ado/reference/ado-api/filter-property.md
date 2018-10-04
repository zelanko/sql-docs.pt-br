---
title: Propriedade Filter | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: cede9be7c484d40c2220fc891779f7dfb6e5a8df
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47762726"
---
# <a name="filter-property"></a>Propriedade Filter
Indica um filtro para os dados em um [conjunto de registros](../../../ado/reference/ado-api/recordset-object-ado.md).  
  
## <a name="settings-and-return-values"></a>As configurações e valores de retorno

Define ou retorna um **Variant** valor, que pode conter um dos seguintes itens:  
  
-   **Cadeia de caracteres de critérios:** composta por uma ou mais cláusulas individuais concatenadas com uma cadeia de caracteres **AND** ou **OR** operadores.  
  
-   **Matriz de indicadores:** que apontam para os registros em valores de uma matriz de indicador exclusivo a **Recordset** objeto.  
  
-   Um [FilterGroupEnum](../../../ado/reference/ado-api/filtergroupenum.md) valor.  
  
## <a name="remarks"></a>Comentários

Use o **filtro** propriedade para bloquear seletivamente registros em uma **Recordset** objeto. Filtradas **Recordset** torna-se o cursor atual. Outras propriedades que retornam valores com base no atual **cursor** são afetadas, tais como [propriedade AbsolutePosition (ADO)](../../../ado/reference/ado-api/absoluteposition-property-ado.md), [propriedade AbsolutePage (ADO)](../../../ado/reference/ado-api/absolutepage-property-ado.md), [ Propriedade RecordCount (ADO)](../../../ado/reference/ado-api/recordcount-property-ado.md), e [propriedade PageCount (ADO)](../../../ado/reference/ado-api/pagecount-property-ado.md). Definindo o **filtro** propriedade para um novo valor específico se move para o registro atual para o primeiro registro que satisfaz o novo valor.
  
A cadeia de caracteres de critérios é composta por cláusulas no formulário *valor de operador FieldName* (por exemplo, `"LastName = 'Smith'"`). Você pode criar cláusulas compostas por meio da concatenação cláusulas individuais com **AND** (por exemplo, `"LastName = 'Smith' AND FirstName = 'John'"`) ou **OR** (por exemplo, `"LastName = 'Smith' OR LastName = 'Jones'"`). Para cadeias de caracteres de critérios, Use as seguintes diretrizes:

-   *FieldName* deve ser um nome de campo válido do **conjunto de registros**. Se o nome do campo contiver espaços, você deverá colocar o nome entre colchetes.  
  
-   Operador deve ser um dos seguintes: \<, >, \<=, > =, <>, =, ou **como**.  
  
-   Valor é o valor com o qual você irá comparar os valores de campo (por exemplo, 'Smith', # #8/24/95, 12.345 ou US $50,00). Use aspas simples com cadeias de caracteres e sinais de sustenido (#) com datas. Para números, você pode usar a notação científica, cifrões e pontos decimais. Se o operador está **como**, valor pode usar caracteres curinga. Somente o asterisco (*) e os curingas de sinal de porcentagem (%) são permitidas, e eles devem ser o último caractere na cadeia de caracteres. Valor não pode ser nulo.  
  
> [!NOTE]
>  Para incluir aspas simples (') no filtro de valor, use duas aspas simples para representar um. Por exemplo, para filtrar o ' Malley, a cadeia de caracteres de critérios deve ser `"col1 = 'O''Malley'"`. Para incluir aspas no início e final do valor do filtro, coloque a cadeia de caracteres com sinais de sustenido (#). Por exemplo, para filtrar '1', a cadeia de caracteres de critérios deve ser `"col1 = #'1'#"`.  
  
-   Não há nenhum precedência entre e e ou. As cláusulas podem ser agrupadas dentro dos parênteses. No entanto, você não pode agrupar cláusulas unidas por um ou e, em seguida, ingressar no grupo para outra cláusula com um AND, como no seguinte trecho de código:  
 `(LastName = 'Smith' OR LastName = 'Jones') AND FirstName = 'John'`  
  
-   Em vez disso, você poderia construir esse filtro como  
 `(LastName = 'Smith' AND FirstName = 'John') OR (LastName = 'Jones' AND FirstName = 'John')`  
  
-   Em um **como** cláusula, você pode usar um caractere curinga no início e no final do padrão. Por exemplo, você pode usar `LastName Like '*mit*'`. Ou com **como** você pode usar um caractere curinga somente no final do padrão. Por exemplo, `LastName Like 'Smit*'`.  
  
 As constantes de filtro tornam mais fácil de resolver conflitos de registros individuais durante o modo de atualização em lotes, permitindo que você exiba, por exemplo, somente os registros que foram afetados durante a última [método UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md) chamada de método.  
  
Definindo o **filtro** propriedade em si pode falhar devido a um conflito com os dados subjacentes. Por exemplo, essa falha pode ocorrer quando um registro já foi excluído por outro usuário. Nesse caso, o provedor retornará avisos para o [coleção de erros (ADO)](../../../ado/reference/ado-api/errors-collection-ado.md) coleção, mas não interrompem a execução do programa. Um erro em tempo de execução ocorre somente se houver conflitos em todos os registros solicitados. Use o [propriedade Status (conjunto de registros ADO)](../../../ado/reference/ado-api/status-property-ado-recordset.md) propriedade para localizar registros com conflitos.  
  
Definindo o **filtro** propriedade como uma cadeia de caracteres de comprimento zero ("") tem o mesmo efeito que usar o **adFilterNone** constante.
  
Sempre que o **filtro** propriedade for definida, a posição atual do registro se move para o primeiro registro no subconjunto filtrado de registros na **conjunto de registros**. Da mesma forma, quando o **filtro** propriedade estiver desmarcada, a posição atual do registro move para o primeiro registro na **conjunto de registros**.

Suponha que um **Recordset** é filtrado com base em um campo de algum tipo de variante, como o tipo sql_variant. Um erro (DISP_E_TYPEMISMATCH ou 80020005) ocorre quando os subtipos dos valores de campo e o filtro usados na cadeia de caracteres de critérios não coincidem. Por exemplo, suponha que:

- Um **Recordset** objeto (rs) contém uma coluna (C) do tipo sql_variant.
- E um campo desta coluna foi atribuído um valor de 1 do tipo I4. A cadeia de caracteres de critérios é definida como `rs.Filter = "C='A'"` no campo.

Essa configuração produz o erro durante o tempo de execução. No entanto, `rs.Filter = "C=2"` aplicado no mesmo campo não produzirá um erro. E o campo é filtrado fora do conjunto de registros atual.

Consulte a [propriedade Bookmark (ADO)](../../../ado/reference/ado-api/bookmark-property-ado.md) propriedade para obter uma explicação dos valores de indicador do qual você pode criar uma matriz a ser usada com a propriedade de filtro.

Somente os filtros na forma de cadeias de caracteres de critérios afetam o conteúdo de um persistente **conjunto de registros**. Um exemplo de uma cadeia de caracteres de critérios é `OrderDate > '12/31/1999'`. Filtros criados com uma matriz de indicadores, ou usando um valor da **FilterGroupEnum**, não afetam o conteúdo de persistido **conjunto de registros**. Essas regras se aplicam a conjuntos de registros criados com cursores do lado do cliente ou servidor.
  
> [!NOTE]
>  Quando você aplica o sinalizador adFilterPendingRecords a um filtrado e modificados **conjunto de registros** no modo de atualização em lotes, o resultante **Recordset** estará vazia se a filtragem se baseia o campo de chave de um tabela de chave única e a modificação foi feita nos valores de campo de chave. O resultante **Recordset** será vazio se uma das instruções a seguir for verdadeira:  
  
-   A filtragem foi baseada em campos de não-chave em uma tabela com chave única.  
  
-   A filtragem foi baseada em todos os campos em uma tabela com chave múltiplo.  
  
-   As modificações foram feitas nos campos de não-chave em uma tabela com chave única.  
  
-   As modificações foram feitas em todos os campos em uma tabela com chave múltiplo.  
  
A tabela a seguir resume os efeitos das **adFilterPendingRecords** em combinações diferentes de filtragem e modificações. A coluna esquerda mostra as modificações possíveis. Modificações podem ser feitas em qualquer um dos campos sem chave, no campo de chave em uma tabela com chave única, ou em qualquer um dos campos de chave em uma tabela com chave múltiplo. A linha superior mostra o critério de filtragem. Filtragem pode ser baseada em qualquer um dos campos sem chave, o campo de chave em uma tabela com chave única, ou qualquer um dos campos de chave em uma tabela com chave múltiplo. As células de interseção mostram os resultados. Um **+** sinal significa que se aplicam **adFilterPendingRecords** resulta em não-vazia **Recordset**. Um **-** sinal de subtração significa vazia **conjunto de registros**.  
  
||Não chaves|Chave única|Várias chaves|
|-|--------------|----------------|-------------------|
|**Não chaves**|+|+|+|
|**Chave única**|+|-|N/A|
|**Várias chaves**|+|N/A|+|
|||||
  
## <a name="applies-to"></a>Aplica-se a

[Objeto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Consulte também

[Exemplo de Filter e RecordCount propriedades (VB)](../../../ado/reference/ado-api/filter-and-recordcount-properties-example-vb.md)
[exemplo de Filter e RecordCount propriedades (VC + +)](../../../ado/reference/ado-api/filter-and-recordcount-properties-example-vc.md)
[método Clear (ADO)](../../../ado/reference/ado-api/clear-method-ado.md) 
 [Otimizar a propriedade dinâmica (ADO)](../../../ado/reference/ado-api/optimize-property-dynamic-ado.md)
