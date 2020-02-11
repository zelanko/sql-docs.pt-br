---
title: Trabalhando com conjuntos de registros | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- Recordset object [ADO]
ms.assetid: bdf9a56a-de4a-44de-9111-2f11ab7b16ea
author: MightyPen
ms.author: genemi
ms.openlocfilehash: a3025140929d7a7cf281f72c035bf79e0a5883b3
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67923410"
---
# <a name="working-with-recordsets"></a>Trabalhar com conjuntos de registros
O objeto **Recordset** tem recursos internos que permitem reorganizar a ordem dos dados no conjunto de resultados, pesquisar um registro específico com base nos critérios fornecidos e até mesmo otimizar essas operações de pesquisa usando índices. A possibilidade de esses recursos estarem disponíveis para uso depende do provedor e, em alguns casos, da propriedade [index](../../../ado/reference/ado-api/index-property.md) – a estrutura da própria fonte de dados.  
  
## <a name="arranging-data"></a>Organizando dados  
 Frequentemente, a maneira mais eficiente de ordenar os dados em seu **conjunto de registros** é especificando uma cláusula order by no comando SQL usado para retornar os resultados a ele. No entanto, talvez seja necessário alterar a ordem dos dados em um **conjunto de registros** que já tenha sido criado. Você pode usar a propriedade **Sort** para estabelecer a ordem na qual as linhas de um **conjunto de registros** são percorridas. Além disso, a propriedade **Filter** determina quais linhas podem ser acessadas ao percorrer linhas.  
  
 A propriedade de **classificação** define ou retorna um valor de **cadeia de caracteres** que indica os nomes de campo no **conjunto de registros** no qual classificar. Cada nome é separado por uma vírgula e é opcionalmente seguido por um espaço e a palavra-chave **ASC** (que classifica o campo em ordem crescente) ou **desc** (que classifica o campo em ordem decrescente). Por padrão, se nenhuma palavra-chave for especificada, o campo será classificado em ordem crescente.  
  
 A operação de classificação é eficiente porque os dados não são reorganizados fisicamente, mas são acessados na ordem especificada por um índice.  
  
 A propriedade **Sort** requer que a propriedade [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) seja definida como **adUseClient**. Um índice temporário será criado para cada campo especificado na propriedade **Sort** se um índice ainda não existir.  
  
 Definir a propriedade **Sort** como uma cadeia de caracteres vazia redefinirá as linhas para sua ordem original e excluirá índices temporários. Os índices existentes não serão excluídos.  
  
 Suponha que um **conjunto de registros** contenha três campos nomeados *FirstName*, *inicialdomeio*e *LastName*. Defina a propriedade **Sort** como a cadeia de`lastName DESC, firstName ASC`caracteres "", que ordenará o **conjunto de registros** por sobrenome em ordem decrescente e, em seguida, pelo primeiro nome em ordem crescente. A inicial do meio é ignorada.  
  
 Nenhum campo referenciado em uma cadeia de caracteres de critérios de classificação pode ser nomeado "ASC" ou "DESC" porque esses nomes entram em conflito com as palavras-chave **ASC** e **desc**. Forneça um campo que tenha um nome conflitante **como** um alias usando a palavra-chave as na consulta que retorna o **conjunto de registros**.  
  
 Para obter mais informações sobre filtragem de **conjunto de registros** , consulte "filtrando os resultados" mais adiante neste tópico.  
  
## <a name="finding-a-specific-record"></a>Localizando um registro específico  
 O ADO fornece os métodos [Find](../../../ado/reference/ado-api/find-method-ado.md) e [Seek](../../../ado/reference/ado-api/seek-method.md) para localizar um registro específico em um **conjunto de registros**. Há suporte para o método **Find** por uma variedade de provedores, mas é limitado a um único critério de pesquisa. O método **Seek** dá suporte à pesquisa em vários critérios, mas não tem suporte de muitos provedores.  
  
 Os índices em campos podem aprimorar muito o desempenho do método **Find** e as propriedades de **classificação** e **filtro** do objeto **Recordset** . Você pode criar um índice interno para um objeto de **campo** definindo sua propriedade de [otimização](../../../ado/reference/ado-api/optimize-property-dynamic-ado.md) dinâmica. Essa propriedade dinâmica é adicionada à coleção **Properties** do objeto **Field** quando você define a propriedade [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) como **adUseClient**. Lembre-se de que esse índice é interno ao ADO-você não pode obter acesso a ele ou usá-lo para qualquer outra finalidade. Além disso, esse índice é diferente da propriedade [index](../../../ado/reference/ado-api/index-property.md) do objeto **Recordset** .  
  
 O método **Find** localiza rapidamente um valor dentro de uma coluna (campo) de um **conjunto de registros**. Com frequência, você pode melhorar a velocidade do método **Find** em uma coluna usando a propriedade **Optimize** para criar um índice nele.  
  
 O método **Find** limita a pesquisa ao conteúdo de um campo. O método **Seek** requer que você tenha um índice e também tenha outras limitações. Se for necessário pesquisar em vários campos que não sejam a base de um índice, ou se seu provedor não oferecer suporte a índices, você poderá limitar os resultados usando a propriedade **Filter** do objeto **Recordset** .  
  
### <a name="find"></a>Encontrar  
 O método **Find** pesquisa um **conjunto de registros** para a linha que atende a um critério especificado. Opcionalmente, a direção da pesquisa, a linha inicial e o deslocamento da linha inicial podem ser especificados. Se o critério for atendido, a posição da linha atual será definida no registro encontrado; caso contrário, a posição será definida como o final (ou início) do **conjunto de registros**, dependendo da direção da pesquisa.  
  
 Somente um nome de coluna única pode ser especificado para o critério. Em outras palavras, esse método não oferece suporte a pesquisas de várias colunas.  
  
 O operador de comparação para o critério pode ser**>**"" (maior que),**\<**"" (menor que), "=" (igual), ">=" (maior ou igual), "<=" (menor ou igual), "<>" (não igual) ou "Like" (correspondência de padrões).  
  
 O valor do critério pode ser uma cadeia de caracteres, um número de ponto flutuante ou uma data. Os valores de cadeia de caracteres são delimitados por aspas simples ou marcas "#" (sinal numérico) (por exemplo, "estado = ' WA '" ou "estado = #WA #"). Os valores de data são delimitados com marcas "#" (sinal numérico) (por exemplo, "start_date > #7/22/97 #").  
  
 Se o operador de comparação for "Like", o valor da cadeia de caracteres poderá conter um asterisco (*) para localizar uma ou mais ocorrências de qualquer caractere ou Subcadeia de caracteres. Por exemplo, "estado like\*" "corresponde a Maine e a Massachusetts. Você também pode usar asteriscos à esquerda e à direita para localizar uma subcadeia de caracteres que está contida nos valores. Por exemplo, "estado como"\*como\*"" corresponde a Alasca, Arkansas e Massachusetts.  
  
 Os asteriscos só podem ser usados no final de uma cadeia de caracteres de critérios ou juntos no início e no final de uma cadeia de caracteres de critério, conforme mostrado anteriormente. Você não pode usar o asterisco como um curinga principal (' * Str ') ou curinga inserido (\*r '). Isso causará um erro.  
  
### <a name="seek-and-index"></a>Busca e índice  
 Use o método **Seek** junto com a propriedade **index** se o provedor subjacente oferecer suporte a índices no objeto **Recordset** . Use o método de [suporte](../../../ado/reference/ado-api/supports-method.md)**(adSeek)** para determinar se o provedor subjacente dá suporte à **busca**e ao método de **suporte (adIndex)** para determinar se o provedor oferece suporte a índices. (Por exemplo, o [provedor de OLE DB para Microsoft Jet](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-microsoft-jet.md) dá suporte a **busca** e **índice**.)  
  
 Se o **Seek** não localizar a linha desejada, nenhum erro ocorrerá e a linha será posicionada no final do **conjunto de registros**. Defina a propriedade **index** para o índice desejado antes de executar esse método.  
  
 Esse método tem suporte apenas com cursores do lado do servidor. Não há suporte para busca quando o valor da propriedade [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) do objeto **Recordset** é **adUseClient**.  
  
 Esse método pode ser usado somente quando o objeto **Recordset** tiver sido aberto com um valor [CommandTypeEnum](../../../ado/reference/ado-api/commandtypeenum.md) de **adCmdTableDirect**.  
  
## <a name="filtering-the-results"></a>Filtrando os resultados  
 O método **Find** limita a pesquisa ao conteúdo de um campo. O método **Seek** requer que você tenha um índice e também tenha outras limitações. Se você precisar pesquisar em vários campos que não sejam a base de um índice ou se seu provedor não oferecer suporte a índices, você poderá limitar os resultados usando a propriedade **Filter** do objeto **Recordset** .  
  
 Use a propriedade **Filter** para desconectar seletivamente os registros em um objeto **Recordset** . O **conjunto de registros** filtrado se torna o cursor atual, o que significa que os registros que não atendem aos critérios de **filtro** não estão disponíveis no **conjunto de registros** até que o **filtro** seja removido. Outras propriedades que retornam valores com base no cursor atual são afetadas, como **AbsolutePosition**, **AbsolutePage**, **RecordCount**e **PageCount**. Isso ocorre porque a definição da propriedade **Filter** para um valor específico moverá o registro atual para o primeiro registro que satisfaça o novo valor.  
  
 A propriedade **Filter** usa um argumento Variant. Esse valor representa um dos três métodos para usar a propriedade **Filter** : uma cadeia de caracteres de critérios, uma constante **FilterGroupEnum** ou uma matriz de indicadores. Para obter mais informações, consulte Filtrando com uma cadeia de caracteres de critérios, filtrando com uma constante e filtrando com indicadores mais adiante neste tópico.  
  
> [!NOTE]
>  Quando você conhece os dados que deseja selecionar, geralmente é mais eficiente abrir um **conjunto de registros** com uma instrução SQL que filtra efetivamente o conjunto de resultados, em vez de depender da propriedade de **filtro** .  
  
 Para remover um filtro de um **conjunto de registros**, use a constante **adFilterNone** . Definir a propriedade **Filter** para uma cadeia de caracteres de comprimento zero ("") tem o mesmo efeito que usar a constante **adFilterNone** .  
  
### <a name="filtering-with-a-criteria-string"></a>Filtrando com uma cadeia de caracteres de critérios  
 A cadeia de caracteres de critérios consiste em cláusulas no *valor do operador Form FieldName* ( `"LastName = 'Smith'"`por exemplo,). Você pode criar cláusulas compostas concatenando cláusulas individuais com **and** (por exemplo `"LastName = 'Smith' AND FirstName = 'John'"`,) e **or** (por exemplo `"LastName = 'Smith' OR LastName = 'Jones'"`,). Use as seguintes diretrizes para cadeias de caracteres de critérios:  
  
-   *FieldName* deve ser um nome de campo válido do **conjunto de registros**. Se o nome do campo contiver espaços, você deverá colocar o nome entre colchetes.  
  
-   O *operador* deve ser um dos seguintes: **\<**, **>**, ** \< **, **>=**, **<>** **=**, ou **like**.  
  
-   *Valor* é o valor com o qual você irá comparar os valores de campo (por `'Smith'`exemplo `#8/24/95#`, `12.345`,, `$50.00`ou). Use aspas simples (') com cadeias de caracteres e sinais`#`de sustenido () com datas. Para números, você pode usar pontos decimais, sinais de dólar e notação científica. Se o *operador* for **como**, o *valor* poderá usar caracteres curinga. Somente o asterisco (\*) e o sinal de porcentagem (%) caracteres curinga são permitidos e devem ser o último caractere na cadeia de caracteres. O *valor* não pode ser nulo.  
  
    > [!NOTE]
    >  Para incluir aspas simples (') no *valor*do filtro, use duas aspas simples para representar uma. Por exemplo, para filtrar em *' Malley*, a cadeia de caracteres de `"col1 = 'O''Malley'"`critérios deve ser. Para incluir aspas simples no início e no final do valor do filtro, coloque a cadeia de caracteres em sinais de sustenido (#). Por exemplo, para filtrar em *' 1 '*, a cadeia de caracteres de `"col1 = #'1'#"`critérios deve ser.  
  
 Não há precedência entre **e** e **ou**. As cláusulas podem ser agrupadas entre parênteses. No entanto, você não pode agrupar cláusulas Unidas por um **ou** e, em seguida, unir o grupo a outra cláusula com um e, da seguinte maneira.  
  
```  
(LastName = 'Smith' OR LastName = 'Jones') AND FirstName = 'John'  
```  
  
 Em vez disso, você criaria esse filtro da seguinte maneira.  
  
```  
(LastName = 'Smith' AND FirstName = 'John') OR (LastName = 'Jones' AND FirstName = 'John')  
```  
  
 Em uma cláusula **like** , você pode usar um caractere curinga no início e no final do padrão (por exemplo, `LastName Like '*mit*'`) ou somente no final do padrão (por exemplo, `LastName Like 'Smit*'`).  
  
### <a name="filtering-with-a-constant"></a>Filtrando com uma constante  
 As constantes a seguir estão disponíveis para filtrar **conjuntos de registros**.  
  
|Constante|DESCRIÇÃO|  
|--------------|-----------------|  
|**adFilterAffectedRecords**|Filtros para exibir somente os registros afetados pela última chamada de **exclusão**, **ressincronização**, **UpdateBatch**ou **CancelBatch** .|  
|**adFilterConflictingRecords**|Filtros para exibir os registros que falharam na última atualização do lote.|  
|**adFilterFetchedRecords**|Filtros para exibir os registros no cache atual – ou seja, os resultados da última chamada para recuperar registros do banco de dados.|  
|**adFilterNone**|Remove o filtro atual e restaura todos os registros para exibição.|  
|**adFilterPendingRecords**|Filtros para exibir somente os registros que foram alterados, mas que ainda não foram enviados ao servidor. Aplicável somente para o modo de atualização do lote.|  
  
 As constantes de filtro facilitam a resolução de conflitos de registro individuais durante o modo de atualização do lote, permitindo que você exiba, por exemplo, somente os registros que foram afetados durante a última chamada do método **UpdateBatch** , conforme mostrado no exemplo a seguir.  
  
 `Attribute VB_Name = "modExaminingData"`  
  
### <a name="filtering-with-bookmarks"></a>Filtrando com indicadores  
 Por fim, você pode passar uma matriz variante de indicadores para a propriedade de **filtro** . O cursor resultante conterá somente os registros cujo indicador foi passado para a propriedade. O exemplo de código a seguir cria uma matriz de indicadores dos registros em um **conjunto de registros** que tem um "B" no campo *NomeDoProduto* . Em seguida, ele passa a matriz para a propriedade **Filter** e exibe informações sobre o **conjunto de registros**filtrado resultante.  
  
```  
'BeginFilterBkmk  
Dim vBkmkArray() As Variant  
Dim i As Integer  
  
'Recordset created using "SELECT * FROM Products" as command.  
'So, we will check to see if ProductName has a capital B, and  
'if so, add to the array.  
i = 0  
Do While Not objRs.EOF  
    If InStr(1, objRs("ProductName"), "B") Then  
        ReDim Preserve vBkmkArray(i)  
        vBkmkArray(i) = objRs.Bookmark  
        i = i + 1  
        Debug.Print objRs("ProductName")  
    End If  
    objRs.MoveNext  
Loop  
  
'Filter using the array of bookmarks.  
objRs.Filter = vBkmkArray  
  
objRs.MoveFirst  
Do While Not objRs.EOF  
    Debug.Print objRs("ProductName")  
    objRs.MoveNext  
Loop  
'EndFilterBkmk  
```  
  
## <a name="creating-a-clone-of-a-recordset"></a>Criando um clone de um conjunto de registros  
 Use o método **clone** para criar vários objetos de **conjunto de registros** duplicados, especialmente se você quiser manter mais de um registro atual em um determinado conjunto de registros. O uso do método **clone** é mais eficiente do que criar e abrir um novo objeto **Recordset** com a mesma definição do original.  
  
 O registro atual de um clone recém-criado é definido originalmente como o primeiro registro. O ponteiro de registro atual em um **conjunto de registros** clonado não é sincronizado com o original ou vice-versa. Você pode navegar independentemente em cada **conjunto de registros**.  
  
 As alterações feitas em um objeto **Recordset** são visíveis em todos os seus clones, independentemente do tipo de cursor. No entanto, depois de executar a [consulta](../../../ado/reference/ado-api/requery-method.md) novamente no **conjunto de registros**original, os clones não serão mais sincronizados com o original.  
  
 O fechamento do **conjunto de registros** original não fecha suas cópias, nem fecha uma cópia, fecha o original ou qualquer uma das outras cópias.  
  
 Você pode clonar um objeto **Recordset** somente se ele oferecer suporte a indicadores. Os valores de indicador são intercambiáveis; ou seja, uma referência de indicador de um objeto **Recordset** refere-se ao mesmo registro em qualquer um de seus clones.
