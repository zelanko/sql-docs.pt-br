---
title: Trabalhando com conjuntos de registros | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Recordset object [ADO]
ms.assetid: bdf9a56a-de4a-44de-9111-2f11ab7b16ea
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: b29d34907c7e4dcccc8494101c819cca05c02066
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/09/2018
---
# <a name="working-with-recordsets"></a>Trabalhando com conjuntos de registros
O **registros** objeto possui recursos internos que permitem a você reorganizar a ordem dos dados no conjunto de resultados, para procurar um registro específico com base em critérios fornecidos por você e até mesmo para otimizar as operações de pesquisa usando os índices. Se esses recursos estão disponíveis para uso depende do provedor e, em alguns casos, como do [índice](../../../ado/reference/ado-api/index-property.md) propriedade — a estrutura da fonte de dados em si.  
  
## <a name="arranging-data"></a>Organizando dados  
 Com frequência, a maneira mais eficiente ordenar os dados em seu **registros** especificando uma cláusula ORDER BY no comando SQL usado para retornar resultados para ele. No entanto, talvez você precise alterar a ordem dos dados em um **registros** que já foi criado. Você pode usar o **classificação** propriedade para estabelecer a ordem em que linhas de uma **registros** são atravessadas. Além disso, o **filtro** propriedade determina quais linhas são podem ser acessados quando percorrer as linhas.  
  
 O **classificação** propriedade define ou retorna um **cadeia de caracteres** valor que indica o campo de nomes no **registros** na qual classificar. Cada nome é separado por uma vírgula e, opcionalmente, é seguido por um espaço e a palavra-chave **ASC** (que classifica o campo em ordem crescente) ou **DESC** (que classifica o campo em ordem decrescente). Por padrão, se nenhuma palavra-chave for especificado, o campo é classificado em ordem crescente.  
  
 A operação de classificação é eficiente, porque os dados não é fisicamente reorganizados, mas são acessados na ordem especificada por um índice.  
  
 O **classificação** propriedade requer o [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) propriedade a ser definida **adUseClient**. Um índice temporário será criado para cada campo especificado no **classificação** propriedade se um índice já não existe.  
  
 Definindo o **classificação** redefinirá as linhas à sua ordem original e excluir índices temporários propriedade como uma cadeia de caracteres vazia. Os índices existentes não serão excluídos.  
  
 Suponha que um **registros** contém três campos denominados *firstName*, *middleInitial*, e *lastName*. Definir o **classificação** propriedade para a cadeia de caracteres "`lastName DESC, firstName ASC`", que pedir o **conjunto de registros** por sobrenome em ordem decrescente e, em seguida, por nome em ordem crescente. A inicial do meio é ignorada.  
  
 Nenhum campo referenciado em uma cadeia de caracteres de critérios de classificação pode ser nomeado "ASC" ou "DESC" porque esses nomes em conflito com as palavras-chave **ASC** e **DESC**. Atribuir a um campo que tem um nome conflitante um alias usando o **AS** palavra-chave na consulta que retorna o **registros**.  
  
 Para obter mais informações sobre **registros** filtragem, consulte "Filtrar os resultados" posteriormente neste tópico.  
  
## <a name="finding-a-specific-record"></a>Localizar um registro específico  
 ADO fornece o [localizar](../../../ado/reference/ado-api/find-method-ado.md) e [busca](../../../ado/reference/ado-api/seek-method.md) métodos para localizar um registro específico em um **registros**. O **localizar** método uma variedade de provedores com suporte, mas é limitado a um critério de pesquisa único. O **busca** método oferece suporte a pesquisas em vários critérios, mas não é suportado por vários provedores.  
  
 Índices em campos podem melhorar o desempenho do **localizar** método e **classificação** e **filtro** propriedades do **registros** objeto. Você pode criar um índice interno para uma **campo** objeto definindo seu dinâmico [otimizar](../../../ado/reference/ado-api/optimize-property-dynamic-ado.md) propriedade. Essa propriedade dinâmica é adicionada para o **propriedades** coleção do **campo** objeto quando você define o [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) propriedade para **adUseClient**. Lembre-se de que esse índice é interno ao ADO, você não pode acessá-lo ou usá-lo para qualquer outra finalidade. Além disso, esse índice é diferente de [índice](../../../ado/reference/ado-api/index-property.md) propriedade do **registros** objeto.  
  
 O **localizar** método rapidamente localiza um valor em uma coluna (campo) de um **registros**. Frequentemente, você pode melhorar a velocidade do **localizar** método em uma coluna usando o **otimizar** propriedade para criar um índice nela.  
  
 O **localizar** método limita sua pesquisa para o conteúdo de um campo. O **busca** método requer que você tem um índice e tem também outras limitações. Se você deve pesquisar em vários campos que não são a base de um índice, ou se o provedor não oferece suporte a índices, você pode limitar seus resultados usando o **filtro** propriedade o **registros** objeto.  
  
### <a name="find"></a>Localizar  
 O **localizar** método pesquisa um **registros** para a linha que satisfaz o critério especificado. Opcionalmente, a direção da pesquisa, linha inicial e o deslocamento da linha inicial pode ser especificada. Se o critério for atendido, a posição da linha atual é definida no registro encontrado; Caso contrário, a posição é definida ao final (ou início) da **registros**, dependendo da direção da pesquisa.  
  
 Apenas um nome de coluna única pode ser especificado para o critério. Em outras palavras, esse método não oferece suporte a pesquisas de várias colunas.  
  
 O operador de comparação para o critério pode ser"**>**"(maior que),"**\<**" (menor que), "=" (igual), "> =" (maior ou igual), "< =" (menor ou igual), " <> "(não igual), ou"Como"(correspondência de padrão).  
  
 O valor padrão pode ser uma cadeia de caracteres, número de ponto flutuante ou data. Os valores de cadeia de caracteres são delimitados com aspas simples ou marcas "#" (sinal numérico) (por exemplo, "estado = 'WA'" ou "estado = WA # #"). Valores de data são delimitados por marcas de "#" (sinal numérico) (por exemplo, "start_date > # # 22/7/97").  
  
 Se o operador de comparação é "como", o valor de cadeia de caracteres pode conter um asterisco (*) para localizar uma ou mais ocorrências de qualquer caractere ou uma subcadeia de caracteres. Por exemplo, "estado como estou\*'" corresponde a rio grande do Norte e Massachusetts. Você também pode usar asteriscos à esquerda e à direita para localizar uma subcadeia de caracteres que está contida dentro dos valores. Por exemplo, "estado como '\*como\*'" corresponde a Alaska, Arkansas e Massachusetts.  
  
 Asteriscos podem ser usados somente no final de uma cadeia de caracteres de critérios ou juntos no início e no final de uma cadeia de caracteres de critérios, como mostrado anteriormente. Você não pode usar o asterisco como um caractere curinga à esquerda ('* str') ou inserida curinga ('s\*r'). Isso causará um erro.  
  
### <a name="seek-and-index"></a>Busca e índice  
 Use o **busca** método junto com o **índice** propriedade se o provedor subjacente que dá suporte a índices no **registros** objeto. Use o [dá suporte a](../../../ado/reference/ado-api/supports-method.md)**(adSeek)** método para determinar se o provedor subjacente oferece suporte a **busca**e o **Supports(adIndex)** método para determinar se o provedor oferece suporte a índices. (Por exemplo, o [OLE DB Provider for Microsoft Jet](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-microsoft-jet.md) dá suporte a **busca** e **índice**.)  
  
 Se **busca** não localizar a linha desejada, nenhum erro ocorrerá e a linha é posicionado no final do **registros**. Definir o **índice** propriedade para o índice desejada antes de executar esse método.  
  
 Esse método tem suporte apenas com cursores do lado do servidor. Busca não é suportado quando o [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) valor da propriedade de **Recordset** objeto é **adUseClient**.  
  
 Esse método pode ser usado somente quando o **registros** objeto tenha sido aberto com um [CommandTypeEnum](../../../ado/reference/ado-api/commandtypeenum.md) valor **adCmdTableDirect**.  
  
## <a name="filtering-the-results"></a>Filtrar os resultados  
 O **localizar** método limita sua pesquisa para o conteúdo de um campo. O **busca** método requer que você tem um índice e tem também outras limitações. Se você deve pesquisar em vários campos que não são a base de um índice ou se o provedor não oferece suporte a índices, você pode limitar seus resultados usando o **filtro** propriedade o **registros** objeto.  
  
 Use o **filtro** propriedade seletivamente retire registros em um **registros** objeto. Filtradas **registros** torna-se o cursor atual, o que significa que os registros que não atendem a **filtro** critérios não estão disponíveis no **registros** até que o **Filtro** é removido. Outras propriedades que retornam valores com base no cursor atual são afetadas, como **AbsolutePosition**, **AbsolutePage**, **RecordCount**, e  **PageCount**. Isso é porque a definição de **filtro** propriedade com um valor específico moverá o registro atual para o primeiro registro que satisfaz o novo valor.  
  
 O **filtro** propriedade aceita um argumento variant. Esse valor representa um dos três métodos para usar o **filtro** propriedade: uma cadeia de caracteres de critérios, uma **FilterGroupEnum** constante ou uma matriz de indicadores. Para obter mais informações, consulte filtragem com uma cadeia de caracteres de critérios de filtragem com uma constante e filtragem com indicadores, posteriormente neste tópico.  
  
> [!NOTE]
>  Quando você conhece os dados que você deseja selecionar, geralmente é mais eficiente para abrir um **registros** com uma instrução SQL que efetivamente filtra o conjunto de resultados, em vez de depender do **filtro** propriedade.  
  
 Para remover um filtro de um **registros**, use o **adFilterNone** constante. Definindo o **filtro** propriedade como uma cadeia de caracteres de comprimento zero ("") tem o mesmo efeito que usar o **adFilterNone** constante.  
  
### <a name="filtering-with-a-criteria-string"></a>Com uma cadeia de caracteres de critérios de filtragem  
 A cadeia de caracteres consiste em cláusulas no formulário *FieldName operador valor* (por exemplo, `"LastName = 'Smith'"`). Você pode criar cláusulas compostas concatenando cláusulas individuais com **AND** (por exemplo, `"LastName = 'Smith' AND FirstName = 'John'"`) e **ou** (por exemplo, `"LastName = 'Smith' OR LastName = 'Jones'"`). Use as seguintes diretrizes para cadeias de caracteres de critérios:  
  
-   *FieldName* deve ser um nome de campo válido do **registros**. Se o nome do campo contiver espaços, você deve colocar o nome entre colchetes.  
  
-   *Operador* deve ser um dos seguintes:  **\<** ,  **>** ,  **\< =** ,  **>=**  ,  **<>** ,  **=** , ou **como**.  
  
-   *Valor* é o valor com o qual você irá comparar os valores de campo (por exemplo, `'Smith'`, `#8/24/95#`, `12.345`, ou `$50.00`). Use aspas simples (') com cadeias de caracteres e sinais numéricos (`#`) com datas. Para números, você pode usar a notação científica, cifrões e pontos decimais. Se *operador* é **como**, *valor* pode usar caracteres curinga. Somente o asterisco (\*) e sinal de porcentagem (%) curinga são permitidos caracteres e devem ser o último caractere na cadeia de caracteres. *Valor* não pode ser nulo.  
  
    > [!NOTE]
    >  Para incluir aspas simples (') no filtro *valor*, use duas aspas simples para representar uma. Por exemplo, para filtrar em *o ' Malley*, a cadeia de caracteres deve ser `"col1 = 'O''Malley'"`. Para incluir aspas simples no início e final do valor do filtro, coloque a cadeia de caracteres entre sinais sustenido (#). Por exemplo, para filtrar em *'1'*, a cadeia de caracteres deve ser `"col1 = #'1'#"`.  
  
 Não há nenhum precedência entre **AND** e **ou**. As cláusulas podem ser agrupadas dentro dos parênteses. No entanto, você não pode agrupar cláusulas unidas por uma **ou** e, em seguida, ingressar no grupo para outra cláusula com um AND, da seguinte maneira.  
  
```  
(LastName = 'Smith' OR LastName = 'Jones') AND FirstName = 'John'  
```  
  
 Em vez disso, você poderia construir esse filtro da seguinte maneira.  
  
```  
(LastName = 'Smith' AND FirstName = 'John') OR (LastName = 'Jones' AND FirstName = 'John')  
```  
  
 Em um **como** cláusula, você pode usar um caractere curinga no início e no final do padrão (por exemplo, `LastName Like '*mit*'`) ou apenas no final do padrão (por exemplo, `LastName Like 'Smit*'`).  
  
### <a name="filtering-with-a-constant"></a>Filtrando com uma constante  
 As constantes a seguir estão disponíveis para filtragem **conjuntos de registros**.  
  
|Constante|Description|  
|--------------|-----------------|  
|**adFilterAffectedRecords**|Filtros para exibir apenas os registros afetados pela última **excluir**, **Resync**, **UpdateBatch**, ou **CancelBatch** chamar.|  
|**adFilterConflictingRecords**|Filtros para exibir os registros que falharam na última atualização em lotes.|  
|**adFilterFetchedRecords**|Filtros para exibir os registros no cache atual — ou seja, os resultados da última chamada para recuperar os registros do banco de dados.|  
|**adFilterNone**|Remove o filtro atual e restaura todos os registros para exibição.|  
|**adFilterPendingRecords**|Os filtros para exibir somente os registros que foram alterados mas ainda não foram enviados ao servidor. Aplicável somente para o modo de atualização em lotes.|  
  
 As constantes de filtro tornam mais fácil resolver conflitos de registro individuais durante o modo de atualização em lotes, permitindo que você exiba, por exemplo, somente os registros que foram afetados durante a última **UpdateBatch** chamada de método, como mostra a exemplo a seguir.  
  
 `Attribute VB_Name = "modExaminingData"`  
  
### <a name="filtering-with-bookmarks"></a>Filtrando com indicadores  
 Por fim, você pode passar uma matriz de variant de marcadores para o **filtro** propriedade. O cursor resultante conterá somente os registros cujo indicador foi passado para a propriedade. O exemplo de código a seguir cria uma matriz de indicadores de registros de um **registros** com "B" *ProductName* campo. Ele passa a matriz de **filtro** propriedade e exibe informações sobre o resultante filtrado **registros**.  
  
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
 Use o **Clone** duplicado de método para criar vários **registros** objetos, especialmente se você deseja manter mais de um registro atual em um determinado conjunto de registros. Usando o **Clone** método é mais eficiente do que criar e abrir um novo **registros** objeto com a mesma definição original.  
  
 O registro atual de um clone criado recentemente é originalmente definido para o primeiro registro. O ponteiro do registro atual no clonado **registros** não está sincronizado com o original ou vice-versa. Você pode navegar independentemente em cada **registros**.  
  
 As alterações feitas a um **registros** objeto são visíveis em todos os seus clones independentemente do tipo de cursor. No entanto, após você executar [Requery](../../../ado/reference/ado-api/requery-method.md) no original **registros**, os clones não serão sincronizados com o original.  
  
 Fechando o original **registros** não fechar suas cópias, nem o fechamento fechar uma cópia original ou qualquer uma das outras cópias.  
  
 Você pode clonar um **registros** objeto apenas se ele dá suporte a indicadores. Valores de indicador são intercambiáveis; ou seja, uma referência de indicador de um **registros** objeto refere-se para o mesmo registro em qualquer um de seus clones.
