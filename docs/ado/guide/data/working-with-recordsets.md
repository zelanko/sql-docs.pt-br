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
manager: craigg
ms.openlocfilehash: 39d8a1bdbc3a56cc03710bc6982b708235c47c45
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47762424"
---
# <a name="working-with-recordsets"></a>Trabalhar com conjuntos de registros
O **Recordset** objeto possui recursos internos que permitem a você reorganizar a ordem dos dados no conjunto de resultados, para procurar um registro específico com base em critérios fornecidos por você e até mesmo para otimizar as operações de pesquisa usando índices. Se esses recursos estão disponíveis para uso depende do provedor e em alguns casos —, como a do [índice](../../../ado/reference/ado-api/index-property.md) propriedade — a estrutura da fonte de dados em si.  
  
## <a name="arranging-data"></a>Organização de dados  
 Com frequência, a maneira mais eficiente para ordenar os dados no seu **Recordset** está especificando uma cláusula ORDER BY no comando SQL usado para retornar resultados para ele. No entanto, talvez você precise alterar a ordem dos dados em um **Recordset** que já foi criado. Você pode usar o **Sort** propriedade para estabelecer a ordem em quais linhas de uma **Recordset** são percorridas. Além disso, o **filtro** propriedade determina quais linhas são podem ser acessados ao percorrer as linhas.  
  
 O **Sort** propriedade define ou retorna um **cadeia de caracteres** nomes de valor que indica o campo no **Recordset** na qual classificar. Cada nome é separado por uma vírgula e, opcionalmente, é seguido por um espaço e a palavra-chave **ASC** (que classifica o campo em ordem crescente) ou **DESC** (que classifica o campo em ordem decrescente). Por padrão, se nenhuma palavra-chave for especificado, o campo é classificado em ordem crescente.  
  
 A operação de classificação é eficiente porque os dados não são reorganizados fisicamente, mas são acessados na ordem especificada por um índice.  
  
 O **Sort** propriedade requer que o [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) propriedade ser definida como **adUseClient**. Um índice temporário será criado para cada campo especificado na **classificação** propriedade se um índice não existir.  
  
 Definindo o **classificação** propriedade como uma cadeia de caracteres vazia será redefinir as linhas à sua ordem original e excluir índices temporários. Os índices existentes não serão excluídos.  
  
 Suponha que um **conjunto de registros** contém três campos denominados *firstName*, *middleInitial*, e *lastName*. Definir a **classificação** propriedade na cadeia de caracteres "`lastName DESC, firstName ASC`", qual será a ordem de **conjunto de registros** por sobrenome em ordem decrescente e, em seguida, por nome em ordem crescente. A inicial do meio será ignorada.  
  
 Nenhum campo referenciado em uma cadeia de caracteres de critérios de classificação pode ser nomeado "ASC" ou "DESC" porque esses nomes em conflito com as palavras-chave **ASC** e **DESC**. Atribuir a um campo que tem um nome conflitante um alias usando o **AS** palavra-chave na consulta que retorna os **conjunto de registros**.  
  
 Para obter mais informações sobre **Recordset** filtragem, consulte "Filtrando os resultados" posteriormente neste tópico.  
  
## <a name="finding-a-specific-record"></a>Localizar um registro específico  
 ADO fornece o [encontrar](../../../ado/reference/ado-api/find-method-ado.md) e [busca](../../../ado/reference/ado-api/seek-method.md) métodos para localizar um registro específico em um **conjunto de registros**. O **localizar** método é compatível com uma variedade de provedores, mas é limitado a um critério de pesquisa único. O **busca** método dá suporte a pesquisas em vários critérios, mas não é suportado por vários provedores.  
  
 Índices em campos bastante podem melhorar o desempenho do **encontrar** método e **classificação** e **filtro** propriedades do **Recordset** objeto. Você pode criar um índice de interno para um **campo** objeto definindo sua dinâmico [otimizar](../../../ado/reference/ado-api/optimize-property-dynamic-ado.md) propriedade. Essa propriedade dinâmica é adicionada para o **propriedades** coleção da **campo** objeto quando você definir o [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) propriedade para **adUseClient**. Lembre-se de que esse índice é interno ao ADO — você não pode acessá-la ou usá-lo para qualquer outra finalidade. Além disso, esse índice é diferente de [índice](../../../ado/reference/ado-api/index-property.md) propriedade da **Recordset** objeto.  
  
 O **encontrar** método localiza rapidamente um valor em uma coluna (campo) de um **conjunto de registros**. Com frequência, você pode melhorar a velocidade do **encontrar** método em uma coluna usando o **otimizar** propriedade para criar um índice nela.  
  
 O **localizar** método limita sua pesquisa para o conteúdo de um campo. O **busca** método requer que você tenha um índice e tem também outras limitações. Se você deve pesquisar em vários campos que não são a base de um índice ou se seu provedor não dá suporte a índices, você pode limitar seus resultados usando o **filtro** propriedade da **Recordset** objeto.  
  
### <a name="find"></a>Localizar  
 O **encontrar** método pesquisa um **Recordset** para a linha que satisfaz o critério especificado. Opcionalmente, a direção da pesquisa, a linha inicial e deslocamento da linha inicial pode ser especificada. Se o critério for atendido, a posição da linha atual é definida no registro encontrado; Caso contrário, a posição é definida até o final (ou inicial) do **Recordset**, dependendo da direção de pesquisa.  
  
 Somente um nome de coluna única pode ser especificado para o critério. Em outras palavras, esse método não dá suporte a pesquisas de várias colunas.  
  
 O operador de comparação para o critério pode ser"**>**"(maior que),"**\<**" (menor que), "=" (igual), "> =" (maior que ou igual), "< =" (menor ou igual), " <> "(não igual), ou"Como"(correspondência de padrões).  
  
 O valor de critério pode ser uma cadeia de caracteres, número de ponto flutuante ou data. Os valores de cadeia de caracteres são delimitados com aspas simples ou marcas de "#" (sinal numérico) (por exemplo, "estado = 'WA'" ou "estado = WA # #"). Valores de data são delimitados com marcas de "#" (sinal numérico) (por exemplo, "start_date > # 97 / #7/22").  
  
 Se o operador de comparação é "como", o valor de cadeia de caracteres pode conter um asterisco (*) para localizar uma ou mais ocorrências de qualquer caractere ou subcadeia de caracteres. Por exemplo, "estado, como estou\*'" corresponde a Maine e Massachusetts. Você também pode usar asteriscos à esquerda e à direita para localizar uma subcadeia de caracteres que está contida dentro dos valores. Por exemplo, "estado como '\*como\*'" corresponde a Alaska, Arkansas e Massachusetts.  
  
 Os asteriscos podem ser usados somente no final de uma cadeia de caracteres de critérios ou em conjunto no início e no final de uma cadeia de caracteres de critérios, como mostrado anteriormente. Você não pode usar o asterisco como curinga à esquerda ('* str') ou incorporados curinga ('s\*r'). Isso causará um erro.  
  
### <a name="seek-and-index"></a>Buscar e de índice  
 Use o **Seek** método junto com o **índice** propriedade se o provedor subjacente que dá suporte a índices no **Recordset** objeto. Use o [dá suporte a](../../../ado/reference/ado-api/supports-method.md)**(adSeek)** método para determinar se o provedor subjacente dá suporte à **busca**e o **Supports(adIndex)** método para determinar se o provedor dá suporte a índices. (Por exemplo, o [OLE DB Provider for Microsoft Jet](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-microsoft-jet.md) dá suporte a **busca** e **índice**.)  
  
 Se **Seek** não localizar a linha desejada, nenhum erro ocorre e a linha é posicionado no final o **conjunto de registros**. Defina as **índice** propriedade para o índice desejada antes de executar esse método.  
  
 Esse método é compatível apenas com cursores do lado do servidor. Busca não é suportado quando o [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) valor da propriedade a **conjunto de registros** objeto é **adUseClient**.  
  
 Esse método pode ser usado somente quando o **conjunto de registros** objeto tenha sido aberto com um [CommandTypeEnum](../../../ado/reference/ado-api/commandtypeenum.md) valor de **adCmdTableDirect**.  
  
## <a name="filtering-the-results"></a>Filtrando os resultados  
 O **localizar** método limita sua pesquisa para o conteúdo de um campo. O **busca** método requer que você tenha um índice e tem também outras limitações. Se você deve pesquisar em vários campos que não são a base de um índice ou se seu provedor não dá suporte a índices, você pode limitar seus resultados usando o **filtro** propriedade da **Recordset** objeto.  
  
 Use o **filtro** propriedade para bloquear seletivamente registros em uma **Recordset** objeto. Filtradas **conjunto de registros** torna-se o cursor atual, o que significa que os registros que não atendem a **filtro** critérios não estão disponíveis na **Recordset** até que o **Filtro** é removido. Outras propriedades que retornam valores com base no cursor atual são afetadas, como **AbsolutePosition**, **AbsolutePage**, **RecordCount**, e  **PageCount**. Isso é porque a definição de **filtro** propriedade como um valor específico se moverá o registro atual para o primeiro registro que satisfaz o novo valor.  
  
 O **filtro** propriedade usa um argumento variant. Esse valor representa um dos três métodos para usar o **filtro** propriedade: uma cadeia de caracteres de critérios, um **FilterGroupEnum** constante ou uma matriz de indicadores. Para obter mais informações, consulte filtragem com uma cadeia de caracteres de critérios, a filtragem com uma constante e Filtering com indicadores, posteriormente neste tópico.  
  
> [!NOTE]
>  Quando você conhece os dados que você deseja selecionar, ele normalmente é mais eficiente para abrir um **conjunto de registros** com uma instrução SQL que efetivamente filtra o conjunto de resultados, em vez de depender de **filtro** propriedade.  
  
 Para remover um filtro de uma **conjunto de registros**, use o **adFilterNone** constante. Definindo o **filtro** propriedade como uma cadeia de caracteres de comprimento zero ("") tem o mesmo efeito que usar o **adFilterNone** constante.  
  
### <a name="filtering-with-a-criteria-string"></a>Com uma cadeia de caracteres de critérios de filtragem  
 A cadeia de caracteres de critérios consiste em cláusulas no formulário *valor de operador FieldName* (por exemplo, `"LastName = 'Smith'"`). Você pode criar cláusulas compostas por meio da concatenação cláusulas individuais com **AND** (por exemplo, `"LastName = 'Smith' AND FirstName = 'John'"`) e **ou** (por exemplo, `"LastName = 'Smith' OR LastName = 'Jones'"`). Use as seguintes diretrizes para cadeias de caracteres de critérios:  
  
-   *FieldName* deve ser um nome de campo válido do **conjunto de registros**. Se o nome do campo contiver espaços, você deverá colocar o nome entre colchetes.  
  
-   *Operador* deve ser um dos seguintes: **\<**, **>**, **\< =**, **>=** , **<>**, **=**, ou **como**.  
  
-   *Valor* é o valor com o qual você irá comparar os valores de campo (por exemplo, `'Smith'`, `#8/24/95#`, `12.345`, ou `$50.00`). Use aspas simples (') com cadeias de caracteres e sinais numéricos (`#`) com datas. Para números, você pode usar a notação científica, cifrões e pontos decimais. Se *operador* é **como**, *valor* pode usar caracteres curinga. Somente o asterisco (\*) curinga (%) são permitidos caracteres de sinal de porcentagem e eles devem ser o último caractere na cadeia de caracteres. *Valor* não pode ser nulo.  
  
    > [!NOTE]
    >  Para incluir aspas simples (') no filtro *valor*, use duas aspas simples para representar um. Por exemplo, para filtrar por *o ' Malley*, a cadeia de caracteres de critérios deve ser `"col1 = 'O''Malley'"`. Para incluir aspas no início e final do valor do filtro, coloque a cadeia de caracteres entre sinais de sustenido (#). Por exemplo, para filtrar por *'1'*, a cadeia de caracteres de critérios deve ser `"col1 = #'1'#"`.  
  
 Não há nenhum precedência entre **AND** e **ou**. As cláusulas podem ser agrupadas dentro dos parênteses. No entanto, você não pode agrupar cláusulas unidas por uma **ou** e, em seguida, ingresse no grupo para outra cláusula com um AND, da seguinte maneira.  
  
```  
(LastName = 'Smith' OR LastName = 'Jones') AND FirstName = 'John'  
```  
  
 Em vez disso, você poderia construir esse filtro da seguinte maneira.  
  
```  
(LastName = 'Smith' AND FirstName = 'John') OR (LastName = 'Jones' AND FirstName = 'John')  
```  
  
 Em um **, como** cláusula, você pode usar um caractere curinga no início e no final do padrão (por exemplo, `LastName Like '*mit*'`) ou apenas no final do padrão (por exemplo, `LastName Like 'Smit*'`).  
  
### <a name="filtering-with-a-constant"></a>Filtrando com uma constante  
 As constantes a seguir estão disponíveis para filtragem **conjuntos de registros**.  
  
|Constante|Description|  
|--------------|-----------------|  
|**adFilterAffectedRecords**|Filtros para exibir apenas os registros afetados pela última **exclua**, **ressincronizar**, **UpdateBatch**, ou **CancelBatch** chamar.|  
|**adFilterConflictingRecords**|Filtros para exibir os registros que falharam na última atualização em lotes.|  
|**adFilterFetchedRecords**|Filtros para exibir os registros no cache atual — ou seja, os resultados da última chamada para recuperar os registros do banco de dados.|  
|**adFilterNone**|Remove o filtro atual e restaura todos os registros para exibição.|  
|**adFilterPendingRecords**|Filtros para exibir apenas os registros que foram alterados, mas ainda não foram enviados ao servidor. Aplicável somente para o modo de atualização em lotes.|  
  
 As constantes de filtro tornam mais fácil de resolver conflitos de registros individuais durante o modo de atualização em lotes, permitindo que você exiba, por exemplo, somente os registros que foram afetados durante a última **UpdateBatch** chamada de método, como mostra a exemplo a seguir.  
  
 `Attribute VB_Name = "modExaminingData"`  
  
### <a name="filtering-with-bookmarks"></a>Filtrando com indicadores  
 Por fim, você pode passar uma matriz de variantes de marcadores para o **filtro** propriedade. O cursor resultante conterá somente os registros cujo indicador foi passado para a propriedade. O exemplo de código a seguir cria uma matriz de indicadores de registros de uma **conjunto de registros** que têm um "B" *ProductName* campo. Ele passa a matriz para o **filtro** propriedade e exibirá informações sobre resultante filtrado **conjunto de registros**.  
  
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
  
## <a name="creating-a-clone-of-a-recordset"></a>Criar um Clone de um conjunto de registros  
 Use o **Clone** duplicado de método para criar vários **Recordset** objetos, especialmente se você desejar manter mais de um registro atual em um determinado conjunto de registros. Usando o **Clone** método é mais eficiente do que criar e abrir uma nova **Recordset** objeto com a mesma definição do original.  
  
 Originalmente, o registro atual de um clone criado recentemente é definido como o primeiro registro. O ponteiro de registro atual no clonado **Recordset** não está sincronizado com o original ou vice-versa. Você pode navegar de forma independente em cada **conjunto de registros**.  
  
 As alterações feitas a um **Recordset** objeto são visíveis em todos os seus clones, independentemente do tipo de cursor. No entanto, depois de executar [Requery](../../../ado/reference/ado-api/requery-method.md) no original **conjunto de registros**, os clones não serão sincronizados ao original.  
  
 Fechando o original **Recordset** não fecha suas cópias, nem o fechamento Feche uma cópia original ou qualquer uma das outras cópias.  
  
 Você pode clonar uma **Recordset** objeto apenas se ele dá suporte a indicadores. Valores de indicador são intercambiáveis; ou seja, uma referência de indicador de um **Recordset** objeto refere-se no mesmo registro em qualquer um de seus clones.
