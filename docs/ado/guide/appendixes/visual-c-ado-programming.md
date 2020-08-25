---
description: Programação ADO do Visual C++
title: Visual C++ Programação ADO | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/08/2018
ms.reviewer: ''
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- ADO, Visual C++
- Visual C++ [ADO]
ms.assetid: 11233b96-e05c-4221-9aed-5f20944b0f1c
author: rothja
ms.author: jroth
ms.openlocfilehash: 66d06630a6bc39c49b9a3e55276bed574869d40d
ms.sourcegitcommit: 33e774fbf48a432485c601541840905c21f613a0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/25/2020
ms.locfileid: "88806768"
---
# <a name="visual-c-ado-programming"></a>Programação ADO do Visual C++
A referência da API do ADO descreve a funcionalidade da API (interface de programação de aplicativo) do ADO usando uma sintaxe semelhante à do Microsoft Visual Basic. Embora o público-alvo seja todos os usuários, os programadores do ADO empregam diversas linguagens, como Visual Basic, Visual C++ (com e sem a diretiva de **#import** ) e Visual J++ (com o pacote de classe ADO/WFC).  

> [!NOTE]
> A Microsoft terminou o suporte para Visual J++ em 2004.

 Para acomodar essa diversidade, o [ADO para Visual C++ índices de sintaxe](./using-ado-with-microsoft-visual-c.md) fornece Visual C++ sintaxe específica à linguagem com links para descrições comuns de funcionalidade, parâmetros, comportamentos excepcionais e assim por diante, na referência da API.  
  
 O ADO é implementado com as interfaces COM (Component Object Model). No entanto, é mais fácil para os programadores trabalharem com com em determinadas linguagens de programação do que outros. Por exemplo, quase todos os detalhes do uso de COM são tratados implicitamente para programadores de Visual Basic, enquanto Visual C++ programadores devem participar desses detalhes.  
  
 As seções a seguir resumem os detalhes dos programadores C e C++ usando o ADO e a diretiva **#import** . Ele se concentra em tipos de dados específicos para COM (**Variant**, **BSTR**e **SafeArray**) e tratamento de erro (_com_error).  
  
## <a name="using-the-import-compiler-directive"></a>Usando a diretiva de compilador #import  
 A diretiva de compilador **#import** Visual C++ simplifica o trabalho com os métodos e as propriedades do ADO. A diretiva usa o nome de um arquivo que contém uma biblioteca de tipos, como o ADO. dll (Msado15.dll), e gera arquivos de cabeçalho contendo declarações de typedef, ponteiros inteligentes para interfaces e constantes enumeradas. Cada interface é encapsulada, ou encapsulada, em uma classe.  
  
 Para cada operação dentro de uma classe (ou seja, um método ou uma chamada de propriedade), há uma declaração para chamar a operação diretamente (ou seja, a forma "bruta" da operação) e uma declaração para chamar a operação bruta e gerar um erro COM se a operação não for executada com êxito. Se a operação for uma propriedade, geralmente há uma diretiva de compilador que cria uma sintaxe alternativa para a operação que tem sintaxe como Visual Basic.  
  
 As operações que recuperam o valor de uma propriedade têm nomes do formulário, **obter**_Propriedade_. As operações que definem o valor de uma propriedade têm nomes do formulário, **Put**_Property_. As operações que definem o valor de uma propriedade com um ponteiro para um objeto ADO têm nomes do formulário,_Propriedade_ **PutRef**.  
  
 Você pode obter ou definir uma propriedade com chamadas desses formulários:  
  
```cpp
variable = objectPtr->GetProperty(); // get property value   
objectPtr->PutProperty(value);       // set property value  
objectPtr->PutRefProperty(&value);   // set property with object pointer  
```
  
## <a name="using-property-directives"></a>Usando diretivas de propriedade  
 A diretiva de compilador **__declspec (Property...)** é uma extensão de linguagem C específica da Microsoft que declara uma função usada como propriedade para ter uma sintaxe alternativa. Como resultado, você pode definir ou obter valores de uma propriedade de forma semelhante a Visual Basic. Por exemplo, você pode definir e obter uma propriedade dessa maneira:  
  
```cpp
objectPtr->property = value;        // set property value  
variable = objectPtr->property;     // get property value  
```
  
 Observe que você não precisa codificar:  
  
```cpp
objectPtr->PutProperty(value);      // set property value  
variable = objectPtr->GetProperty;  // get property value  
```
  
 O compilador irá gerar a **Get** _-_ chamada de_Propriedade_ Get, **Put**-ou **PutRef**apropriada com base em qual sintaxe alternativa é declarada e se a propriedade está sendo lida ou gravada.  
  
 A diretiva de compilador **__declspec (Property...)** só pode declarar a sintaxe de **Get**, **Put**ou **Get** e **Put** alternativa para uma função. As operações somente leitura têm apenas uma declaração **Get** ; as operações somente gravação têm uma declaração **Put** ; as operações que são de leitura e gravação têm as declarações **Get** e **Put** .  
  
 Somente duas declarações são possíveis com essa diretiva; no entanto, cada propriedade pode ter três funções **Get**_de propriedade: Propriedade_Get,_Propriedade_ **Put**e_Propriedade_ **PutRef**. Nesse caso, somente duas formas da propriedade têm a sintaxe alternativa.  
  
 Por exemplo, a propriedade **ActiveConnection** do objeto **Command** é declarada com uma sintaxe alternativa para **Get**_ActiveConnection_ e **PutRef**_ActiveConnection_. A sintaxe **PutRef**é uma boa opção porque, na prática, normalmente você desejará colocar um objeto de **conexão** aberta (ou seja, um ponteiro de objeto de **conexão** ) nessa propriedade. Por outro lado, o objeto **Recordset** tem operações de_ActiveConnection_ **Get**-, **Put**-e **PutRef**, mas nenhuma sintaxe alternativa.  
  
## <a name="collections-the-getitem-method-and-the-item-property"></a>Coleções, o método GetItem e a propriedade item  

 O ADO define várias coleções, incluindo **campos**, **parâmetros**, **Propriedades**e **erros**. Em Visual C++, o método **GetItem (_index_)** retorna um membro da coleção. *Índice* é uma **variante**, o valor que é um índice numérico do membro na coleção ou uma cadeia de caracteres que contém o nome do membro.  
  
 A diretiva de compilador **__declspec (Property...)** declara a propriedade **Item** como uma sintaxe alternativa para o método **GetItem ()** fundamental de cada coleção. A sintaxe alternativa usa colchetes e é semelhante a uma referência de matriz. Em geral, os dois formulários são semelhantes ao seguinte:  
  
```cpp
  
      collectionPtr->GetItem(index);  
collectionPtr->Item[index];  
```
  
 Por exemplo, atribua um valor a um campo de um objeto **Recordset** , chamado **_RS_**, derivado da tabela **autores** do banco de dados **pubs** . Use a propriedade **Item ()** para acessar o terceiro **campo** da coleção de **campos** de objeto de **conjunto de registros** (as coleções são indexadas de zero; suponha que o terceiro campo seja denominado **_au \_ fname_**). Em seguida, chame o método **Value ()** no objeto **Field** para atribuir um valor de cadeia de caracteres.  
  
 Isso pode ser expresso em Visual Basic das quatro maneiras a seguir (as duas últimas formas são exclusivas para Visual Basic; outras linguagens não têm equivalentes):  
  
```cpp
rs.Fields.Item(2).Value = "value"  
rs.Fields.Item("au_fname").Value = "value"  
rs(2) = "value"  
rs!au_fname = "value"  
```
  
 O equivalente em Visual C++ aos dois primeiros formulários acima é:  
  
```cpp
rs->Fields->GetItem(long(2))->PutValue("value");   
rs->Fields->GetItem("au_fname")->PutValue("value");  
```
  
 -ou-(a sintaxe alternativa para a propriedade **Value** também é mostrada)  
  
```cpp
rs->Fields->Item[long(2)]->Value = "value";  
rs->Fields->Item["au_fname"]->Value = "value";  
```
  
 Para obter exemplos de iteração por meio de uma coleção, consulte a seção "coleções do ADO" de "referência do ADO".  
  
## <a name="com-specific-data-types"></a>Tipos de dados específicos de COM  
 Em geral, qualquer tipo de dados Visual Basic que você encontrar na referência da API do ADO tem um equivalente Visual C++. Isso inclui tipos de dados padrão como **Char não assinado** para um **byte**de Visual Basic, **curto** para **inteiro**e **longo** para **longo**. Examine os índices de Sintaxepara ver exatamente o que é necessário para os operandos de um determinado método ou propriedade.  
  
 As exceções a essa regra são os tipos de dados específicos para COM: **Variant**, **BSTR**e **SafeArray**.  
  
### <a name="variant"></a>Variante  
 Uma **variante** é um tipo de dados estruturado que contém um membro de valor e um membro de tipo de dados. Uma **variante** pode conter uma ampla variedade de outros tipos de dados, incluindo outra variante, BSTR, Boolean, IDispatch ou IUnknown pointer, Currency, Date e assim por diante. COM também fornece métodos que facilitam a conversão de um tipo de dados em outro.  
  
 A classe **_variant_t** encapsula e gerencia o tipo de dados **Variant** .  
  
 Quando a referência da API do ADO diz que um operando de método ou propriedade usa um valor, isso geralmente significa que o valor é passado em um **_variant_t**.  
  
 Essa regra é explicitamente verdadeira quando a seção de **parâmetros** nos tópicos da referência da API do ADO diz que um operando é uma **variante**. Uma exceção é quando a documentação diz explicitamente que o operando usa um tipo de dados padrão, como **longo** ou **byte**, ou uma enumeração. Outra exceção é quando o operando usa uma **cadeia de caracteres**.  
  
### <a name="bstr"></a>BSTR  
 Um **BSTR** (**@** ASIC **Str**ing) é um tipo de dados estruturado que contém uma cadeia de caracteres e o comprimento da cadeia de caracteres. COM fornece métodos para alocar, manipular e liberar um **BSTR**.  
  
 A classe **_bstr_t** encapsula e gerencia o tipo de dados **BSTR** .  
  
 Quando a referência da API do ADO diz que um método ou propriedade usa um valor de **cadeia de caracteres** , isso significa que o valor está na forma de um **_bstr_t**.  
  
### <a name="casting-_variant_t-and-_bstr_t-classes"></a>Conversão de classes de _variant_t e de _bstr_t  
 Geralmente, não é necessário codificar explicitamente um **_variant_t** ou **_bstr_t** em um argumento para uma operação. Se a classe **_variant_t** ou **_bstr_t** tiver um construtor que corresponda ao tipo de dados do argumento, o compilador irá gerar o **_variant_t** ou **_bstr_t**apropriado.  
  
 No entanto, se o argumento for ambíguo, ou seja, o tipo de dados do argumento corresponder a mais de um construtor, você deverá converter o argumento com o tipo de dados apropriado para invocar o Construtor correto.  
  
 Por exemplo, a declaração para o método **Recordset:: Open** é:  
  
```cpp
    HRESULT Open (  
        const _variant_t & Source,  
        const _variant_t & ActiveConnection,  
        enum CursorTypeEnum CursorType,  
        enum LockTypeEnum LockType,  
        long Options );  
```
  
 O `ActiveConnection` argumento usa uma referência a uma **_variant_t**, que você pode codificar como uma cadeia de conexão ou um ponteiro para um objeto de **conexão** aberta.  
  
 O **_variant_t** correto será construído implicitamente se você passar uma cadeia de caracteres como " `DSN=pubs;uid=MyUserName;pwd=MyPassword;` ", ou um ponteiro como " `(IDispatch *) pConn` ".  
  
> [!NOTE]
>  Se você estiver se conectando a um provedor de fonte de dados que dá suporte à autenticação do Windows, especifique **Trusted_Connection = Sim** ou **segurança integrada = SSPI** , em vez de ID de usuário e informações de senha na cadeia de conexão.  
  
 Ou você pode codificar explicitamente um **_variant_t** contendo um ponteiro como " `_variant_t((IDispatch *) pConn, true)` ". A conversão, `(IDispatch *)` resolve a ambiguidade com outro construtor que usa um ponteiro para uma interface IUnknown.  
  
 É um fato crucial, embora raramente mencionado, que o ADO é uma interface IDispatch. Sempre que um ponteiro para um objeto ADO deve ser passado como uma **variante**, esse ponteiro deve ser convertido como um ponteiro para uma interface IDispatch.  
  
 O último caso codifica explicitamente o segundo argumento booliano do construtor com seu valor padrão opcional de `true` . Esse argumento faz com que o construtor de **variante** chame seu método **AddRef**(), que compensa o ADO chamando automaticamente o método **_variant_t:: Release**() quando o método ADO ou a chamada de propriedade for concluída.  
  
### <a name="safearray"></a>SafeArray  
 Um **SafeArray** é um tipo de dados estruturado que contém uma matriz de outros tipos de dados. Um **SafeArray** é chamado de *Safe* porque contém informações sobre os limites de cada dimensão de matriz e limita o acesso a elementos de matriz dentro desses limites.  
  
 Quando a referência da API do ADO diz que um método ou propriedade usa ou retorna uma matriz, isso significa que o método ou a propriedade usa ou retorna um **SafeArray**, não uma matriz C/C++ nativa.  
  
 Por exemplo, o segundo parâmetro do método **OpenSchema** do objeto de **conexão** requer uma matriz de valores **variantes** . Esses valores de **variante** devem ser passados como elementos de um **SafeArray**e esse **SafeArray** deve ser definido como o valor de outra **variante**. É essa outra **variante** que é passada como o segundo argumento de **OpenSchema**.  
  
 Como outros exemplos, o primeiro argumento do método **Find** é uma **variante** cujo valor é um **SafeArray**unidimensional; cada um dos argumentos de primeiro e segundo opcionais de **AddNew** é um **SafeArray**unidimensional; e o valor de retorno do método **GetRows** é uma **variante** cujo valor é um **SafeArray**bidimensional.  
  
## <a name="missing-and-default-parameters"></a>Parâmetros ausentes e padrão  
 Visual Basic permite parâmetros ausentes em métodos. Por exemplo, o método **Open** do objeto **Recordset** tem cinco parâmetros, mas você pode ignorar os parâmetros intermediários e deixar os parâmetros à direita. Um **BSTR** ou **Variant** padrão será substituído dependendo do tipo de dados do operando ausente.  
  
 Em C/C++, todos os operandos devem ser especificados. Se você quiser especificar um parâmetro ausente cujo tipo de dados é uma cadeia de caracteres, especifique um **_bstr_t** que contenha uma cadeia de caracteres nula. Se você quiser especificar um parâmetro ausente cujo tipo de dados é uma **variante**, especifique um **_variant_t** com um valor de DISP_E_PARAMNOTFOUND e um tipo de VT_ERROR. Como alternativa, especifique o equivalente **_variant_t** constante, **vtMissing**, que é fornecido pela diretiva **#import** .  
  
 Três métodos são exceções ao uso típico de **vtMissing**. Esses são os métodos **Execute** dos objetos **Connection** e **Command** e o método **NextRecordset** do objeto **Recordset** . Estas são as assinaturas:  
  
```cpp
_RecordsetPtr <A HREF="mdmthcnnexecute.htm">Execute</A>( _bstr_t CommandText, VARIANT * RecordsAffected,   
        long Options );  // Connection  
_RecordsetPtr <A HREF="mdmthcmdexecute.htm">Execute</A>( VARIANT * RecordsAffected, VARIANT * Parameters,   
        long Options );  // Command  
_RecordsetPtr <A HREF="mdmthnextrec.htm">NextRecordset</A>( VARIANT * RecordsAffected );  // Recordset  
```
  
 Os parâmetros, *RecordsAffected* e *Parameters*, são ponteiros para uma **variante**. *Parâmetros* é um parâmetro de entrada que especifica o endereço de uma **variante** que contém um único parâmetro, ou matriz de parâmetros, que modificará o comando que está sendo executado. *RecordsAffected* é um parâmetro de saída que especifica o endereço de uma **variante**, em que o número de linhas afetadas pelo método é retornado.  
  
 No método **Command** Object **Execute** , indique que nenhum parâmetro é especificado definindo *parâmetros* como `&vtMissing` (o que é recomendado) ou para o ponteiro NULL (ou seja, **NULL** ou zero (0)). Se os *parâmetros* forem definidos como o ponteiro NULL, o método substituirá internamente o equivalente de **vtMissing**e concluirá a operação.  
  
 Em todos os métodos, indique que o número de registros afetados não deve ser retornado pela definição de *RecordsAffected* para o ponteiro NULL. Nesse caso, o ponteiro NULL não é muito um parâmetro ausente como uma indicação de que o método deve descartar o número de registros afetados.  
  
 Portanto, para esses três métodos, é válido codificar algo como:  
  
```cpp
pConnection->Execute("commandText", NULL, adCmdText);   
pCommand->Execute(NULL, NULL, adCmdText);  
pRecordset->NextRecordset(NULL);  
```
  
## <a name="error-handling"></a>Tratamento de erros  
 No COM, a maioria das operações retorna um código de retorno HRESULT que indica se uma função foi concluída com êxito. A diretiva **#import** gera código wrapper em cada método "RAW" ou propriedade e verifica o HRESULT retornado. Se o HRESULT indicar falha, o código do wrapper lançará um erro COM chamando _com_issue_errorex () com o código de retorno HRESULT como um argumento. Objetos de erro com podem ser capturados em um bloco **try** - **Catch** . (Para fins de eficiência, pegue uma referência a um objeto **_com_error** .)  
  
 Lembre-se de que são erros do ADO: eles resultam da falha da operação do ADO. Os erros retornados pelo provedor subjacente aparecem como objetos de **erro** na coleção de **erros** do objeto de **conexão** .  
  
 A diretiva **#import** cria apenas rotinas de tratamento de erros para métodos e propriedades declarados no ADO. dll. No entanto, você pode aproveitar esse mesmo mecanismo de tratamento de erros escrevendo sua própria macro de verificação de erro ou função embutida. Consulte o tópico, [Visual C++ Extensions](./visual-c-extensions-for-ado.md)ou o código nas seções a seguir para obter exemplos.  
  
## <a name="visual-c-equivalents-of-visual-basic-conventions"></a>Visual C++ equivalentes de convenções de Visual Basic  
 Veja a seguir um resumo de várias convenções na documentação do ADO, codificados em Visual Basic, bem como seus equivalentes no Visual C++.  
  
### <a name="declaring-an-ado-object"></a>Declarando um objeto ADO  
 No Visual Basic, uma variável de objeto ADO (neste caso, para um objeto **Recordset** ) é declarada da seguinte maneira:  
  
```vb
Dim rst As ADODB.Recordset  
```
  
 A cláusula " `ADODB.Recordset` ", é o ProgID do objeto **Recordset** , conforme definido no registro. Uma nova instância de um objeto de **registro** é declarada da seguinte maneira:  
  
```vb
Dim rst As New ADODB.Recordset  
```
  
 - ou -  
  
```vb
Dim rst As ADODB.Recordset  
Set rst = New ADODB.Recordset  
```
  
 Em Visual C++, a diretiva **#import** gera declarações de tipo de ponteiro inteligente para todos os objetos ADO. Por exemplo, uma variável que aponta para um objeto **_Recordset** é do tipo **_RecordsetPtr**e é declarada da seguinte maneira:  
  
```cpp
_RecordsetPtr  rs;  
```
  
 Uma variável que aponta para uma nova instância de um objeto **_Recordset** é declarada da seguinte maneira:  
  
```cpp
_RecordsetPtr  rs("ADODB.Recordset");  
```
  
 - ou -  
  
```cpp
_RecordsetPtr  rs;  
rs.CreateInstance("ADODB.Recordset");  
```
  
 - ou -  
  
```cpp
_RecordsetPtr  rs;  
rs.CreateInstance(__uuidof(_Recordset));  
```
  
 Depois que o método **CreateInstance** é chamado, a variável pode ser usada da seguinte maneira:  
  
```cpp
rs->Open(...);  
```
  
 Observe que, em um caso, o `.` operador "" é usado como se a variável fosse uma instância de uma classe ( `rs.CreateInstance` ) e, em outro caso, o `->` operador "" é usado como se a variável fosse um ponteiro para uma interface ( `rs->Open` ).  
  
 Uma variável pode ser usada de duas maneiras porque o `->` operador "" está sobrecarregado para permitir que uma instância de uma classe se comporte como um ponteiro para uma interface. Um membro da classe particular da variável de instância contém um ponteiro para a interface **_Recordset** ; o `->` operador "" retorna esse ponteiro; e o ponteiro retornado acessa os membros do objeto **_Recordset** .  
  
### <a name="coding-a-missing-parameter---string"></a>Codificando uma cadeia de caracteres de parâmetro ausente  
 Quando você precisa codificar um operando de **cadeia de caracteres** ausente no Visual Basic, simplesmente omita o operando. Você deve especificar o operando em Visual C++. Codifique um **_bstr_t** que tem uma cadeia de caracteres vazia como um valor.  
  
```cpp
_bstr_t strMissing(L"");  
```
  
### <a name="coding-a-missing-parameter---variant"></a>Codificando um parâmetro ausente-Variant  
 Quando você precisa codificar um operando de **variante** ausente no Visual Basic, simplesmente omita o operando. Você deve especificar todos os operandos em Visual C++. Codifique um parâmetro **Variant** ausente com um **_variant_t** definido como o valor especial, DISP_E_PARAMNOTFOUND e tipo VT_ERROR. Como alternativa, especifique **vtMissing**, que é uma constante predefinida equivalente fornecida pela diretiva **#import** .  
  
```cpp
_variant_t  vtMissingYours(DISP_E_PARAMNOTFOUND, VT_ERROR);   
```
  
 -ou use-  
  
```cpp
...vtMissing...;  
```
  
### <a name="declaring-a-variant"></a>Declarando uma variante  
 No Visual Basic, uma **variante** é declarada com a instrução **Dim** da seguinte maneira:  
  
```vb
Dim VariableName As Variant  
```
  
 Em Visual C++, declare uma variável como tipo **_variant_t**. Algumas declarações **_variant_t** esquemáticos de esquema são mostradas abaixo.  
  
> [!NOTE]
>  Essas declarações simplesmente fornecem uma ideia do que você codificaria em seu próprio programa. Para obter mais informações, consulte os exemplos abaixo e a documentação do Visual C + +.  
  
```cpp
_variant_t  VariableName(value);  
_variant_t  VariableName((data type cast) value);  
_variant_t  VariableName(value, VT_DATATYPE);  
_variant_t  VariableName(interface * value, bool fAddRef = true);  
```
  
### <a name="using-arrays-of-variants"></a>Usando matrizes de variantes  
 No Visual Basic, as matrizes de **variantes** podem ser codificadas com a instrução **Dim** ou você pode usar a função de **matriz** , conforme demonstrado no seguinte código de exemplo:  
  
```vb
Public Sub ArrayOfVariants  
Dim cn As ADODB.Connection  
Dim rs As ADODB.Recordset  
Dim fld As ADODB.Field  
  
    cn.Open "DSN=pubs"  
    rs = cn.OpenSchema(adSchemaColumns, _  
        Array(Empty, Empty, "authors", Empty))  
    For Each fld in rs.Fields  
        Debug.Print "Name = "; fld.Name  
    Next fld  
    rs.Close  
    cn.Close  
End Sub  
```
  
 O exemplo a seguir Visual C++ demonstra como usar um **SafeArray** usado com um **_variant_t**.  
  
#### <a name="notes"></a>Observações  
 As observações a seguir correspondem a seções comentadas no exemplo de código.  
  
1.  Mais uma vez, a função embutida TESTHR () é definida para tirar proveito do mecanismo de tratamento de erros existente.  
  
2.  Você só precisa de uma matriz unidimensional, então você pode usar **SafeArrayCreateVector**, em vez da Declaração **SAFEARRAYBOUND** de uso geral e da função **SafeArrayCreate** . Veja a seguir o que esse código seria semelhante ao uso de **SafeArrayCreate**:  
  
    ```cpp
       SAFEARRAYBOUND   sabound[1];  
       sabound[0].lLbound = 0;  
       sabound[0].cElements = 4;  
       pSa = SafeArrayCreate(VT_VARIANT, 1, sabound);  
    ```
  
3.  O esquema identificado pela constante enumerada, **adSchemaColumns**, está associado a quatro colunas de restrição: TABLE_CATALOG, TABLE_SCHEMA, TABLE_NAME e column_name. Portanto, uma matriz de valores **variantes** com quatro elementos é criada. Em seguida, um valor de restrição que corresponde à terceira coluna, TABLE_NAME, é especificado.  
  
     O **conjunto de registros** retornado consiste em várias colunas, um subconjunto das quais são as colunas de restrição. Os valores das colunas de restrição para cada linha retornada devem ser iguais aos valores de restrição correspondentes.  
  
4.  Aqueles familiarizados com **SAFEARRAYs** podem se surpreender para que **SafeArrayDestroy**() não seja chamado antes da saída. Na verdade, chamar **SafeArrayDestroy**() nesse caso causará uma exceção em tempo de execução. O motivo é que o destruidor para `vtCriteria` chamará **VariantClear**() quando o **_variant_t** sair do escopo, o que liberará o **SafeArray**. Chamar **SafeArrayDestroy**, sem limpar manualmente o **_variant_t**, faria com que o destruidor tentasse limpar um ponteiro **SafeArray** inválido.  
  
     Se **SafeArrayDestroy** foram chamados, o código ficaria assim:  
  
    ```cpp
          TESTHR(SafeArrayDestroy(pSa));  
       vtCriteria.vt = VT_EMPTY;  
          vtCriteria.parray = NULL;  
    ```
  
     No entanto, é muito mais simples permitir que o **_variant_t** gerencie o **SafeArray**.  
  
```cpp
// Visual_CPP_ADO_Prog_1.cpp  
// compile with: /EHsc  
#import "msado15.dll" no_namespace rename("EOF", "EndOfFile")  
  
// Note 1  
inline void TESTHR( HRESULT _hr ) {   
   if FAILED(_hr)   
      _com_issue_error(_hr);   
}  
  
int main() {  
   CoInitialize(NULL);  
   try {  
      _RecordsetPtr pRs("ADODB.Recordset");  
      _ConnectionPtr pCn("ADODB.Connection");  
      _variant_t vtTableName("authors"), vtCriteria;  
      long ix[1];  
      SAFEARRAY *pSa = NULL;  
  
      pCn->Provider = "sqloledb";  
      pCn->Open("Data Source='(local)';Initial Catalog='pubs';Integrated Security=SSPI", "", "", adConnectUnspecified);  
      // Note 2, Note 3  
      pSa = SafeArrayCreateVector(VT_VARIANT, 1, 4);  
      if (!pSa)   
         _com_issue_error(E_OUTOFMEMORY);  
  
      // Specify TABLE_NAME in the third array element (index of 2).   
      ix[0] = 2;        
      TESTHR(SafeArrayPutElement(pSa, ix, &vtTableName));  
  
      // There is no Variant constructor for a SafeArray, so manually set the   
      // type (SafeArray of Variant) and value (pointer to a SafeArray).  
  
      vtCriteria.vt = VT_ARRAY | VT_VARIANT;  
      vtCriteria.parray = pSa;  
  
      pRs = pCn->OpenSchema(adSchemaColumns, vtCriteria, vtMissing);  
  
      long limit = pRs->GetFields()->Count;  
      for ( long x = 0 ; x < limit ; x++ )  
         printf( "%d: %s\n", x + 1, ((char*) pRs->GetFields()->Item[x]->Name) );  
      // Note 4  
      pRs->Close();  
      pCn->Close();  
   }  
   catch (_com_error &e) {  
      printf("Error:\n");  
      printf("Code = %08lx\n", e.Error());  
      printf("Code meaning = %s\n", (char*) e.ErrorMessage());  
      printf("Source = %s\n", (char*) e.Source());  
      printf("Description = %s\n", (char*) e.Description());  
   }  
   CoUninitialize();  
}  
```
  
### <a name="using-property-getputputref"></a>Usando a propriedade Get/Put/PutRef  
 Em Visual Basic, o nome de uma propriedade não é qualificado por se ela é recuperada, atribuída ou atribuída a uma referência.  
  
```vb
Public Sub GetPutPutRef  
Dim rs As New ADODB.Recordset  
Dim cn As New ADODB.Connection  
Dim sz as Integer  
cn.Open "Provider=sqloledb;Data Source=yourserver;" & _  
         "Initial Catalog=pubs;Integrated Security=SSPI;"  
rs.PageSize = 10  
sz = rs.PageSize  
rs.ActiveConnection = cn  
rs.Open "authors",,adOpenStatic  
' ...  
rs.Close  
cn.Close  
End Sub  
```
  
 Este exemplo de Visual C++ demonstra **Get**a propriedade get / **Put** / **PutRef**_Property_.  
  
#### <a name="notes"></a>Observações  
 As observações a seguir correspondem a seções comentadas no exemplo de código.  
  
1.  Este exemplo usa duas formas de um argumento de cadeia de caracteres ausente: uma constante explícita, **strMissing**, e uma cadeia de caracteres que o compilador usará para criar um **_bstr_t** temporário que existirá para o escopo do método **Open** .  
  
2.  Não é necessário converter o operando de `rs->PutRefActiveConnection(cn)` para `(IDispatch *)` porque o tipo do operando já é `(IDispatch *)` .  
  
```cpp
// Visual_CPP_ado_prog_2.cpp  
// compile with: /EHsc  
#import "msado15.dll" no_namespace rename("EOF", "EndOfFile")  
  
int main() {  
   CoInitialize(NULL);  
   try {  
      _ConnectionPtr cn("ADODB.Connection");  
      _RecordsetPtr rs("ADODB.Recordset");  
      _bstr_t strMissing(L"");  
      long oldPgSz = 0, newPgSz = 5;  
  
      // Note 1  
      cn->Provider = "sqloledb";  
      cn->Open("Data Source='(local)';Initial Catalog=pubs;Integrated Security=SSPI;", strMissing, "", adConnectUnspecified);  
  
      oldPgSz = rs->GetPageSize();  
      // -or-  
      // oldPgSz = rs->PageSize;  
  
      rs->PutPageSize(newPgSz);  
      // -or-  
      // rs->PageSize = newPgSz;  
  
      // Note 2  
      rs->PutRefActiveConnection( cn );  
      rs->Open("authors", vtMissing, adOpenStatic, adLockReadOnly, adCmdTable);  
      printf("Original pagesize = %d, new pagesize = %d\n", oldPgSz, rs->GetPageSize());  
      rs->Close();  
      cn->Close();  
  
   }  
   catch (_com_error &e) {  
      printf("Description = %s\n", (char*) e.Description());  
   }  
   ::CoUninitialize();  
}  
```
  
### <a name="using-getitemx-and-itemx"></a>Usando GetItem (x) e item [x]  
 Este exemplo de Visual Basic demonstra a sintaxe padrão e alternativa para **Item**().  
  
```vb
Public Sub GetItemItem  
Dim rs As New ADODB.Recordset  
Dim name as String  
rs = rs.Open "authors", "DSN=pubs;", adOpenDynamic, _  
         adLockBatchOptimistic, adTable  
name = rs(0)  
' -or-  
name = rs.Fields.Item(0)  
rs(0) = "Test"  
rs.UpdateBatch  
' Restore name  
rs(0) = name  
rs.UpdateBatch  
rs.Close  
End Sub  
```
  
 Este Visual C++ exemplo demonstra o **Item**.  
  
> [!NOTE]
>  A observação a seguir corresponde às seções comentadas no exemplo de código: quando a coleção é acessada com **Item**, o índice, **2**, deve ser convertido para **Long** , de modo que um construtor apropriado será invocado.  
  
```cpp
// Visual_CPP_ado_prog_3.cpp  
// compile with: /EHsc  
#import "msado15.dll" no_namespace rename("EOF", "EndOfFile")  
  
void main() {  
   CoInitialize(NULL);  
   try {  
      _ConnectionPtr cn("ADODB.Connection");  
      _RecordsetPtr rs("ADODB.Recordset");  
      _variant_t vtFirstName;  
  
      cn->Provider = "sqloledb";  
      cn->Open("Data Source='(local)';Initial Catalog=pubs;Integrated Security=SSPI;", "", "", adConnectUnspecified);  
  
      rs->PutRefActiveConnection( cn );  
      rs->Open("authors", vtMissing, adOpenStatic, adLockOptimistic, adCmdTable);  
      rs->MoveFirst();  
  
      // Note 1. Get a field.  
      vtFirstName = rs->Fields->GetItem((long)2)->GetValue();  
      // -or-  
      vtFirstName = rs->Fields->Item[(long)2]->Value;  
  
      printf( "First name = '%s'\n", (char*)( (_bstr_t)vtFirstName) );  
  
      rs->Fields->GetItem((long)2)->Value = L"TEST";  
      rs->Update(vtMissing, vtMissing);  
  
      // Restore name  
      rs->Fields->GetItem((long)2)->PutValue(vtFirstName);  
      // -or-  
      rs->Fields->GetItem((long)2)->Value = vtFirstName;  
      rs->Update(vtMissing, vtMissing);  
      rs->Close();  
   }  
   catch (_com_error &e) {  
      printf("Description = '%s'\n", (char*) e.Description());  
   }  
   ::CoUninitialize();  
}  
```
  
### <a name="casting-ado-object-pointers-with-idispatch-"></a>Convertendo ponteiros de objeto ADO com (IDispatch *)  
 O exemplo a seguir Visual C++ demonstra como usar (IDispatch *) para converter ponteiros de objeto ADO.  
  
#### <a name="notes"></a>Observações  
 As observações a seguir correspondem a seções comentadas no exemplo de código.  
  
1.  Especifique um objeto de **conexão** aberta em uma **variante**codificada explicitamente. Converta-o com (IDispatch \* ) para que o Construtor correto seja invocado. Além disso, defina explicitamente o segundo parâmetro **_variant_t** como o valor padrão **true**, de modo que a contagem de referência de objeto estará correta quando a operação **Recordset:: Open** terminar.  
  
2.  A expressão, `(_bstr_t)` , não é uma conversão, mas um operador de **_variant_t** que extrai uma cadeia de caracteres de **_bstr_t** da **variante** retornada pelo **valor**.  
  
 A expressão, `(char*)` , não é uma conversão, mas um operador de **_bstr_t** que extrai um ponteiro para a cadeia de caracteres encapsulada em um objeto **_bstr_t** .  
  
 Esta seção de código demonstra alguns dos comportamentos úteis dos operadores de **_variant_t** e **_bstr_t** .  
  
```cpp
// Visual_CPP_ado_prog_4.cpp  
// compile with: /EHsc  
#import "msado15.dll" no_namespace rename("EOF", "EndOfFile")  
  
int main() {  
   CoInitialize(NULL);  
   try {  
      _ConnectionPtr pConn("ADODB.Connection");  
      _RecordsetPtr pRst("ADODB.Recordset");  
  
      pConn->Provider = "sqloledb";  
      pConn->Open("Data Source='(local)';Initial Catalog='pubs';Integrated Security=SSPI", "", "", adConnectUnspecified);  
  
      // Note 1.  
      pRst->Open("authors", _variant_t((IDispatch *) pConn, true), adOpenStatic, adLockReadOnly, adCmdTable);  
      pRst->MoveLast();  
  
      // Note 2.  
      printf("Last name is '%s %s'\n",   
         (char*) ((_bstr_t) pRst->GetFields()->GetItem("au_fname")->GetValue()),  
         (char*) ((_bstr_t) pRst->Fields->Item["au_lname"]->Value));  
  
      pRst->Close();  
      pConn->Close();  
   }  
   catch (_com_error &e) {  
      printf("Description = '%s'\n", (char*) e.Description());  
   }     
   ::CoUninitialize();  
}  
```