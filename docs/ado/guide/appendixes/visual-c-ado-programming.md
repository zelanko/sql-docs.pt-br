---
title: "Programação do Visual C++ ADO | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: guide
ms.technology: drivers
ms.custom: 
ms.date: 02/15/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
dev_langs: C++
helpviewer_keywords:
- ADO, Visual C++
- Visual C++ [ADO]
ms.assetid: 11233b96-e05c-4221-9aed-5f20944b0f1c
caps.latest.revision: "13"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 8decc959840898d0b82c86c0d955b29a7affddde
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="visual-c-ado-programming"></a>Programação de ADO do Visual C++
A referência de API ADO descreve a funcionalidade do ADO API (API) usando uma sintaxe semelhante para o Microsoft Visual Basic. Embora o público-alvo é todos os usuários, programadores ADO empregam diversas linguagens como Visual Basic, Visual C++ (com e sem o **#import** diretiva) e o Visual J++ (com o pacote de classe ADO/WFC).  

> [!NOTE]
> Suporte da Microsoft foi encerrado para o Visual J++ em 2004.

 Para acomodar essa diversidade de [ADO para índices de sintaxe do Visual C++](../../../ado/guide/appendixes/using-ado-with-microsoft-visual-c.md) fornecer uma sintaxe de específicos de linguagem Visual C++ com links para descrições comuns de funcionalidade, parâmetros, comportamentos excepcionais e assim por diante, na API Referência.  
  
 ADO é implementado com interfaces COM (Component Object Model). No entanto, é mais fácil para os programadores trabalhar com determinadas linguagens de programação que outros. Por exemplo, o quase todos os detalhes de uso COM são tratados implicitamente para programadores de Visual Basic, enquanto que os programadores de Visual C++ devem abordar a esses detalhes se.  
  
 As seções a seguir resumem detalhes para programadores de C e C++ usando o ADO e o **#import** diretiva. Ele se concentra em tipos de dados específicos COM (**Variant**, **BSTR**, e **SafeArray**) e o tratamento de erros ( com_error).  
  
## <a name="using-the-import-compiler-directive"></a>Usando a diretiva de compilador #import  
 O **#import** diretiva de compilador do Visual C++ simplifica o trabalho com as propriedades e métodos do ADO. A diretiva usa o nome de um arquivo que contém uma biblioteca de tipos, como o arquivo. dll ADO (Msado15.dll) e gera arquivos de cabeçalho que contém declarações typedef, ponteiros inteligentes para interfaces e constantes enumeradas. Cada interface está encapsulado ou encapsulada em uma classe.  
  
 Para cada operação dentro de uma classe (ou seja, uma chamada de método ou propriedade), há uma declaração para chamar a operação diretamente (ou seja, o formulário "bruto" da operação) e uma declaração para chamar a operação bruta e lança um erro COM se a operação falhar ao executar succ essfully. Se a operação é uma propriedade, normalmente há uma diretiva de compilador que cria uma sintaxe alternativa para a operação que tem sintaxe como o Visual Basic.  
  
 Operações de recuperar o valor de uma propriedade têm nomes do formulário, **obter***propriedade*. Operações que defina o valor de uma propriedade têm nomes do formulário, **colocar***propriedade*. Operações que defina o valor de uma propriedade com um ponteiro para um objeto ADO têm nomes do formulário, **PutRef***propriedade*.  
  
 Você pode obter ou definir uma propriedade com chamadas destas formas:  
  
```  
variable = objectPtr->GetProperty(); // get property value   
objectPtr->PutProperty(value);       // set property value  
objectPtr->PutRefProperty(&value);   // set property with object pointer  
```  
  
## <a name="using-property-directives"></a>Usando diretivas de propriedade  
 O **__declspec(property...)**  diretiva de compilador é uma extensão de linguagem específica do Microsoft C que declara uma função usada como uma propriedade para ter uma sintaxe alternativa. Como resultado, você pode definir ou obter valores de uma propriedade de forma semelhante ao Visual Basic. Por exemplo, você pode definir e obter uma propriedade deste modo:  
  
```  
objectPtr->property = value;        // set property value  
variable = objectPtr->property;     // get property value  
```  
  
 Observe que você não precisa de código:  
  
```  
objectPtr->PutProperty(value);      // set property value  
variable = objectPtr->GetProperty;  // get property value  
```  
  
 O compilador gerará apropriada **obter***-*, **colocar**-, ou **PutRef***propriedade* chamada com base no qual a sintaxe alternativa é declarada e se a propriedade está sendo lidos ou gravados.  
  
 O **__declspec(property...)**  diretiva de compilador só pode declarar **obter**, **colocar**, ou **obter** e **colocar** a sintaxe alternativa para uma função. Operações somente leitura só têm um **obter** declaração; operações de somente gravação só tem um **colocar** declaração; operações que são leitura e gravação ter **obter** e **colocar** declarações.  
  
 Apenas duas declarações são possíveis com esta diretiva; No entanto, cada propriedade pode ter três funções de propriedade: **obter***propriedade*, **colocar***propriedade*, e **PutRef**  *Propriedade*. Nesse caso, apenas duas formas da propriedade tem a sintaxe alternativa.  
  
 Por exemplo, o **comando** objeto **ActiveConnection** propriedade é declarada com uma sintaxe alternativa para **obter***ActiveConnection*e **PutRef***ActiveConnection*. O **PutRef**-sintaxe é uma boa opção porque, na prática, você normalmente deve colocar um aberto **Conexão** objeto (ou seja, um **Conexão** ponteiro de objeto) nesse propriedade. Por outro lado, o **registros** objeto tem **obter**-, **colocar**-, e **PutRef***ActiveConnection*operações, mas nenhuma sintaxe alternativa.  
  
## <a name="collections-the-getitem-method-and-the-item-property"></a>A propriedade do Item, o método GetItem e coleções  
 ADO define várias coleções, incluindo **campos**, **parâmetros**, **propriedades**, e **erros**. No Visual C++, o **GetItem (***índice***)** método retorna um membro da coleção. *Índice* é um **Variant**, o valor que é um índice numérico do membro na coleção, ou uma cadeia de caracteres que contém o nome do membro.  
  
 O **__declspec(property...)**  diretiva de compilador declara o **Item** a propriedade como uma sintaxe alternativa para cada coleção do fundamental **obter GetItem ()** método. A sintaxe alternativa usa colchetes e é semelhante a uma referência de matriz. Em geral, as duas formas a seguinte aparência:  
  
```  
  
      collectionPtr->GetItem(index);  
collectionPtr->Item[index];  
```  
  
 Por exemplo, atribuir um valor a um campo de um **registros** objeto, chamado ***rs***, derivada do **autores** tabela do **pubs** banco de dados. Use o **Item()** propriedade para acessar a terceira **campo** do **registros** objeto **campos** coleção (o coleções são indexadas no zero. Suponha que o terceiro campo é denominado ***au_fname***). Em seguida, chame o **Value ()** método no **campo** objeto para atribuir um valor de cadeia de caracteres.  
  
 Isso pode ser expresso em Visual Basic a seguir quatro maneiras (os últimos dois formulários são exclusivos para o Visual Basic; outros idiomas não têm equivalentes):  
  
```  
rs.Fields.Item(2).Value = "value"  
rs.Fields.Item("au_fname").Value = "value"  
rs(2) = "value"  
rs!au_fname = "value"  
```  
  
 É o equivalente no Visual C++ para os primeiros dois formulários acima:  
  
```  
rs->Fields->GetItem(long(2))->PutValue("value");   
rs->Fields->GetItem("au_fname")->PutValue("value");  
```  
  
 - ou - (a sintaxe alternativa para o **valor** propriedade também é mostrada)  
  
```  
rs->Fields->Item[long(2)]->Value = "value";  
rs->Fields->Item["au_fname"]->Value = "value";  
```  
  
 Para obter exemplos de iteração em uma coleção, consulte a seção "Coleções de ADO" de "Referência ADO".  
  
## <a name="com-specific-data-types"></a>Tipos de dados específicos de COM  
 Em geral, qualquer tipo de dados do Visual Basic que localizar na referência de API do ADO tem um equivalente de Visual C++. Isso inclui tipos de dados padrão, como **unsigned char** para um Visual Basic **bytes**, **curto** para **inteiro**, e  **longo** para **longo**. Examinar a sintaxe Indexesto veja exatamente o que é necessário para os operandos de um determinado método ou propriedade.  
  
 As exceções a essa regra são os tipos de dados específicos COM: **Variant**, **BSTR**, e **SafeArray**.  
  
### <a name="variant"></a>Variante  
 Um **Variant** é um tipo de dados estruturados que contém um membro de valor e um membro de tipo de dados. Um **Variant** pode conter uma ampla variedade de outros tipos de dados, inclusive outra variante, BSTR, Boolean, IDispatch ou IUnknown ponteiro, moeda, data e assim por diante. COM também fornece métodos que tornam mais fácil para convertem um tipo de dados para outro.  
  
 O **variant_t** classe encapsula e gerencia o **Variant** tipo de dados.  
  
 Quando a referência de API ADO diz um método ou operando da propriedade usa um valor, geralmente significa que o valor é passado um **variant_t**.  
  
 Essa regra é explicitamente verdadeiro quando o **parâmetros** seção nos tópicos de referência de API do ADO diz um operando é um **Variant**. Uma exceção é quando a documentação diz explicitamente o operando usa um tipo de dados padrão, como **longo** ou **bytes**, ou uma enumeração. Outra exceção é quando o operando leva um **cadeia de caracteres**.  
  
### <a name="bstr"></a>BSTR  
 Um **BSTR** (**B**asic **STR**ndo) é um tipo de dados estruturados que contém uma cadeia de caracteres e o comprimento da cadeia de caracteres. COM fornece métodos para alocar, manipular e liberar um **BSTR**.  
  
 O **bstr_t** classe encapsula e gerencia o **BSTR** tipo de dados.  
  
 Quando a referência de API ADO diz que um método ou propriedade usa um **cadeia de caracteres** valor, significa o valor está na forma de um **bstr_t**.  
  
### <a name="casting-variantt-and-bstrt-classes"></a>Projetando Classes variant_t e bstr_t  
 Geralmente não é necessário código explicitamente um **variant_t** ou **bstr_t** em um argumento para uma operação. Se o **variant_t** ou **bstr_t** classe tem um construtor que corresponda ao tipo de dados do argumento, o compilador gerará apropriada **variant_t** ou **bstr_t**.  
  
 No entanto, se o argumento for ambíguo, ou seja, o tipo de dados do argumento corresponde a mais de um construtor, você deve converter o argumento com o tipo de dados apropriado para chamar o construtor correto.  
  
 Por exemplo, a declaração para o **Recordset::Open** método é:  
  
```  
    HRESULT Open (  
        const _variant_t & Source,  
        const _variant_t & ActiveConnection,  
        enum CursorTypeEnum CursorType,  
        enum LockTypeEnum LockType,  
        long Options );  
```  
  
 O `ActiveConnection` argumento tem uma referência a um **variant_t**, que você pode codificar como uma cadeia de caracteres de conexão ou um ponteiro para um aberto **Conexão** objeto.  
  
 Corretas **variant_t** será construído implicitamente se você passar uma cadeia de caracteres, como "`DSN=pubs;uid=MyUserName;pwd=MyPassword;`", ou um ponteiro, como "`(IDispatch *) pConn`".  
  
> [!NOTE]
>  Se você estiver se conectando a um provedor de fonte de dados que oferece suporte à autenticação do Windows, você deve especificar **Trusted_Connection = yes** ou **segurança integrada = SSPI** em vez de ID de usuário e senha informações na cadeia de conexão.  
  
 Ou você pode codificar explicitamente um **variant_t** que contém um ponteiro, como "`_variant_t((IDispatch *) pConn, true)`". A conversão, `(IDispatch *)`, elimina a ambiguidade de outro construtor que usa um ponteiro para uma interface IUnknown.  
  
 É crucial, embora raramente mencionado o fato de que o ADO é uma interface IDispatch. Sempre que um ponteiro para um objeto ADO deve ser passado como um **Variant**, esse ponteiro deve ser convertido como um ponteiro para uma interface IDispatch.  
  
 O segundo argumento booliano do construtor com seu valor padrão opcional, os códigos de último caso explicitamente `true`. Esse argumento faz com que o **Variant** construtor chamar seu **AddRef**método (), que compensa ADO automaticamente chamando o **_variant_t::Release**método) Quando a chamada de método ou propriedade ADO for concluído.  
  
### <a name="safearray"></a>SafeArray  
 Um **SafeArray** é um tipo de dados estruturados que contém uma matriz de outros tipos de dados. Um **SafeArray** é chamado *seguro* porque ele contém informações sobre os limites de cada dimensão de matriz e limita o acesso aos elementos da matriz dentro desses limites.  
  
 Quando a referência de API ADO diz que um método ou propriedade leva ou retorna uma matriz, isso significa que o método ou propriedade leva ou retorna um **SafeArray**, não uma matriz de C/C++ nativo.  
  
 Por exemplo, o segundo parâmetro do **Conexão** objeto **OpenSchema** método requer uma matriz de **Variant** valores. Os **Variant** valores devem ser transmitidos como elementos de um **SafeArray**e que **SafeArray** deve ser definido como o valor de outro **Variant** . É que outros **Variant** que é passado como o segundo argumento de **OpenSchema**.  
  
 Mais exemplos, o primeiro argumento do **localizar** método é um **Variant** cujo valor é um unidimensional **SafeArray**; cada argumentos opcionais primeiro e segundo de **AddNew** é um unidimensional **SafeArray**; e o valor de retorno de **GetRows** método é um **Variant** cujo valor é um bidimensional **SafeArray**.  
  
## <a name="missing-and-default-parameters"></a>Ausente e o padrão de parâmetros  
 Visual Basic permite parâmetros em métodos ausentes. Por exemplo, o **registros** objeto **abrir** método tem cinco parâmetros, mas você pode ignorar parâmetros intermediários e deixa desativados à direita de parâmetros. Um padrão **BSTR** ou **Variant** será substituído dependendo do tipo de dados do operando ausente.  
  
 C/C++, todos os operandos devem ser especificados. Se você quiser especificar um parâmetro ausente cujo tipo de dados é uma cadeia de caracteres, especifique um **bstr_t** que contém uma cadeia de caracteres nula. Se você deseja especificar um parâmetro ausente cujo tipo de dados é um **Variant**, especifique um **variant_t** com um valor de DISP_E_PARAMNOTFOUND e um tipo de VT_ERROR. Como alternativa, especifique o equivalente **variant_t** constante, **vtMissing**, que é fornecido pelo **#import** diretiva.  
  
 Três métodos são exceções para o uso típico do **vtMissing**. Esses são os **Execute** métodos do **Conexão** e **comando** objetos e o **NextRecordset** método o **Registros** objeto. Estas são as suas assinaturas:  
  
```  
_RecordsetPtr <A HREF="mdmthcnnexecute.htm">Execute</A>( _bstr_t CommandText, VARIANT * RecordsAffected,   
        long Options );  // Connection  
_RecordsetPtr <A HREF="mdmthcmdexecute.htm">Execute</A>( VARIANT * RecordsAffected, VARIANT * Parameters,   
        long Options );  // Command  
_RecordsetPtr <A HREF="mdmthnextrec.htm">NextRecordset</A>( VARIANT * RecordsAffected );  // Recordset  
```  
  
 Os parâmetros *RecordsAffected* e *parâmetros*, são ponteiros para um **Variant**. *Parâmetros* é um parâmetro de entrada que especifica o endereço de um **Variant** que contém um único parâmetro ou matriz de parâmetros, o que irá modificar o comando que está sendo executado. *RecordsAffected* é um parâmetro de saída que especifica o endereço de um **Variant**, em que o número de linhas afetadas pelo método é retornado.  
  
 No **comando** objeto **Execute** método, indicam que não são especificados definindo *parâmetros* como `&vtMissing` (que é recomendado) ou o ponteiro nulo (ou seja, **nulo** ou zero (0)). Se *parâmetros* está definido para o ponteiro nulo, o método substitui internamente o equivalente de **vtMissing**e, em seguida, concluir a operação.  
  
 Todos os métodos, indicam que o número de registros afetados não deve ser retornado pela configuração *RecordsAffected* ao ponteiro nulo. Nesse caso, o ponteiro nulo não é tanto um parâmetro ausente como uma indicação de que o método deve descartar o número de registros afetados.  
  
 Assim, desses três métodos, é válido para o código algo como:  
  
```  
pConnection->Execute("commandText", NULL, adCmdText);   
pCommand->Execute(NULL, NULL, adCmdText);  
pRecordset->NextRecordset(NULL);  
```  
  
## <a name="error-handling"></a>Tratamento de erros  
 Em COM, a maioria das operações retornam um código de retorno de HRESULT que indica se uma função foi concluída com êxito. O **#import** diretiva gera o código de wrapper em torno de cada propriedade ou método "bruto" e verifica o HRESULT retornado. Se o HRESULT indica falha, o código de wrapper gerará um erro de COM pela chamada _com_issue_errorex() com o código de retorno HRESULT como um argumento. Objetos de erro podem ser capturados em uma **tente**-**catch** bloco. (Para a mesma da eficiência, capturar uma referência a um **com_error** objeto.)  
  
 Lembre-se de que esses são erros de ADO: eles são provenientes de falha de operação do ADO. Erros retornados pelo provedor subjacente aparecem como **erro** objetos no **Conexão** objeto **erros** coleção.  
  
 O **#import** diretiva cria apenas erro rotinas de manipulação de métodos e propriedades declaradas no arquivo. dll ADO. No entanto, você pode tirar proveito desse erro mesmo mecanismo de tratamento escrevendo seu próprio macro ou função embutida de verificação de erros. Consulte o tópico [extensões do Visual C++](../../../ado/guide/appendixes/visual-c-extensions-for-ado.md), ou o código nas seções a seguir para obter exemplos.  
  
## <a name="visual-c-equivalents-of-visual-basic-conventions"></a>Equivalentes do Visual C++ de convenções do Visual Basic  
 Este é um resumo das várias convenções na documentação do ADO, codificada em Visual Basic, bem como seus equivalentes no Visual C++.  
  
### <a name="declaring-an-ado-object"></a>Declarando um objeto ADO  
 No Visual Basic, uma variável de objeto ADO (neste caso um **registros** objeto) é declarado da seguinte maneira:  
  
```  
Dim rst As ADODB.Recordset  
```  
  
 A cláusula "`ADODB.Recordset`", é o ProgID do **registros** conforme definido no registro do objeto. Uma nova instância de um **registro** objeto for declarado da seguinte maneira:  
  
```  
Dim rst As New ADODB.Recordset  
```  
  
 -ou-  
  
```  
Dim rst As ADODB.Recordset  
Set rst = New ADODB.Recordset  
```  
  
 No Visual C++, o **#import** diretiva gera declarações de tipo de ponteiro inteligente para todos os objetos do ADO. Por exemplo, uma variável que aponta para um **Recordset** objeto é do tipo **_RecordsetPtr**e é declarado da seguinte maneira:  
  
```  
_RecordsetPtr  rs;  
```  
  
 Uma variável que aponta para uma nova instância de um **Recordset** objeto for declarado da seguinte maneira:  
  
```  
_RecordsetPtr  rs("ADODB.Recordset");  
```  
  
 -ou-  
  
```  
_RecordsetPtr  rs;  
rs.CreateInstance("ADODB.Recordset");  
```  
  
 -ou-  
  
```  
_RecordsetPtr  rs;  
rs.CreateInstance(__uuidof(_Recordset));  
```  
  
 Após o **CreateInstance** método é chamado, a variável pode ser usada da seguinte maneira:  
  
```  
rs->Open(...);  
```  
  
 Observe que em um caso, o "`.`" operador é usado como se a variável de uma instância de uma classe (`rs.CreateInstance`) e em outro caso, o "`->`" operador é usado como se a variável de um ponteiro para uma interface (`rs->Open`).  
  
 Uma variável pode ser usada de duas maneiras, porque o "`->`" operador está sobrecarregado para permitir que uma instância de uma classe para que atue como um ponteiro para uma interface. Um membro de classe particular da variável da instância contém um ponteiro para o **Recordset** interface; o "`->`" operador retorna esse ponteiro; e o ponteiro retornado acessa os membros a **Recordset**  objeto.  
  
### <a name="coding-a-missing-parameter--string"></a>Codificando um parâmetro ausente-cadeia de caracteres  
 Quando você precisa codificar a ausência de **cadeia de caracteres** operando no Visual Basic, você simplesmente omitir o operando. Você deve especificar o operando em Visual C++. Código de um **bstr_t** que tem uma cadeia de caracteres vazia como valor.  
  
```  
_bstr_t strMissing(L"");  
```  
  
### <a name="coding-a-missing-parameter--variant"></a>Codificando um parâmetro ausente-Variant  
 Quando você precisa codificar a ausência de **Variant** operando no Visual Basic, você simplesmente omitir o operando. Você deve especificar todos os operandos no Visual C++. A ausência de código **Variant** parâmetro com um **variant_t** definido como o valor especial, DISP_E_PARAMNOTFOUND e tipo, VT_ERROR. Como alternativa, especifique **vtMissing**, que é uma constante predefinida equivalente fornecida pelo **#import** diretiva.  
  
```  
_variant_t  vtMissingYours(DISP_E_PARAMNOTFOUND, VT_ERROR);   
```  
  
 - ou use-  
  
```  
...vtMissing...;  
```  
  
### <a name="declaring-a-variant"></a>Declarando uma variante  
 No Visual Basic, uma **Variant** é declarada com o **Dim** instrução da seguinte maneira:  
  
```  
Dim VariableName As Variant  
```  
  
 No Visual C++, declarar uma variável como tipo **variant_t**. Esquema alguns **variant_t** declarações são mostradas abaixo.  
  
> [!NOTE]
>  Essas declarações simplesmente dar uma ideia do que você faria o código no seu programa. Para obter mais informações, consulte os exemplos abaixo e a documentação Visual C + +.  
  
```  
_variant_t  VariableName(value);  
_variant_t  VariableName((data type cast) value);  
_variant_t  VariableName(value, VT_DATATYPE);  
_variant_t  VariableName(interface * value, bool fAddRef = true);  
```  
  
### <a name="using-arrays-of-variants"></a>Usando matrizes de variantes  
 No Visual Basic, matrizes de **variantes** podem ser codificados com o **Dim** instrução, ou você pode usar o **matriz** de função, conforme demonstrado no código de exemplo a seguir:  
  
```  
Public Sub ArrayOfVariants  
Dim cn As ADODB.Connection  
Dim rs As ADODB.Recordset  
Dim fld As ADODB.Field  
  
    cn.Open "DSN=pubs"  
    rs = cn.OpenSchema(adSchemaColumns, _  
        Array(Empty, Empty, "authors", Empty))  
    For Each fld in rs.Fields  
        Debug.Print "Name = "; fld.Name  
    Next fld  
    rs.Close  
    cn.Close  
End Sub  
```  
  
 O exemplo de Visual C++ a seguir demonstra como usar um **SafeArray** usado com um **variant_t**.  
  
#### <a name="notes"></a>Observações  
 As observações a seguir correspondem às seções comentadas no exemplo de código.  
  
1.  Novamente, a função embutida TESTHR() é definida para tirar proveito do mecanismo de tratamento de erros existente.  
  
2.  Você só precisa de uma matriz unidimensional, então você pode usar **SafeArrayCreateVector**, em vez de finalidade geral **SAFEARRAYBOUND** declaração e **SafeArrayCreate** função. Esta é a aparência que o código usando **SafeArrayCreate**:  
  
    ```  
       SAFEARRAYBOUND   sabound[1];  
       sabound[0].lLbound = 0;  
       sabound[0].cElements = 4;  
       pSa = SafeArrayCreate(VT_VARIANT, 1, sabound);  
    ```  
  
3.  O esquema identificado pela constante enumerada, **adSchemaColumns**, está associado a quatro colunas de restrição: TABLE_CATALOG, TABLE_SCHEMA, TABLE_NAME e nome da coluna. Portanto, uma matriz de **Variant** valores com quatro elementos é criado. Em seguida, um valor de restrição que corresponde à terceira coluna, TABLE_NAME, é especificado.  
  
     O **registros** que é retornado consiste em várias colunas, um subconjunto dos quais é as colunas de restrição. Os valores das colunas de restrição para cada linha retornada devem ser o mesmo que os valores de restrição correspondente.  
  
4.  Aqueles que estão familiarizados com **SafeArrays** pode ser surpreso que **SafeArrayDestroy**() não é chamado antes de sair. Na verdade, chamar **SafeArrayDestroy**() nesse caso fará com que uma exceção de tempo de execução. A razão é que o destruidor de `vtCriteria` chamará **VariantClear**() quando o **variant_t** sai do escopo, o que irá liberar o **SafeArray**. Chamando **SafeArrayDestroy**, sem limpar manualmente o **variant_t**, causaria o destruidor tentar limpar inválido **SafeArray** ponteiro.  
  
     Se **SafeArrayDestroy** foi chamado, o código teria esta aparência:  
  
    ```  
          TESTHR(SafeArrayDestroy(pSa));  
       vtCriteria.vt = VT_EMPTY;  
          vtCriteria.parray = NULL;  
    ```  
  
     No entanto, é muito mais simples permitir que o **variant_t** gerenciar o **SafeArray**.  
  
```  
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
  
### <a name="using-property-getputputref"></a>Usando a propriedade Get, Put/PutRef  
 No Visual Basic, o nome de uma propriedade não é qualificado por se for recuperado, atribuído ou atribuído a uma referência.  
  
```  
Public Sub GetPutPutRef  
Dim rs As New ADODB.Recordset  
Dim cn As New ADODB.Connection  
Dim sz as Integer  
cn.Open "Provider=sqloledb;Data Source=yourserver;" & _  
         "Initial Catalog=pubs;Integrated Security=SSPI;"  
rs.PageSize = 10  
sz = rs.PageSize  
rs.ActiveConnection = cn  
rs.Open "authors",,adOpenStatic  
' ...  
rs.Close  
cn.Close  
End Sub  
```  
  
 Este exemplo do Visual C++ demonstra o **obter**/**colocar**/**PutRef***propriedade*.  
  
#### <a name="notes"></a>Observações  
 As observações a seguir correspondem às seções comentadas no exemplo de código.  
  
1.  Este exemplo usa duas formas de um argumento de cadeia de caracteres ausente: uma constante explícita, **strMissing**e uma cadeia de caracteres que o compilador usará para criar um temporário **bstr_t** que vai existir para o escopo de  **Abra** método.  
  
2.  Não é necessário converter o operando de `rs->PutRefActiveConnection(cn)` para `(IDispatch *)` porque o tipo do operando já está `(IDispatch *)`.  
  
```  
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
  
### <a name="using-getitemx-and-itemx"></a>Usando o Item [x] e GetItem(x)  
 Este exemplo do Visual Basic demonstra a sintaxe padrão e alternativa de **Item**().  
  
```  
Public Sub GetItemItem  
Dim rs As New ADODB.Recordset  
Dim name as String  
rs = rs.Open "authors", "DSN=pubs;", adOpenDynamic, _  
         adLockBatchOptimistic, adTable  
name = rs(0)  
' -or-  
name = rs.Fields.Item(0)  
rs(0) = "Test"  
rs.UpdateBatch  
' Restore name  
rs(0) = name  
rs.UpdateBatch  
rs.Close  
End Sub  
```  
  
 Este exemplo do Visual C++ demonstra **Item**.  
  
> [!NOTE]
>  A observação a seguir corresponde a sessões com comentários no código de exemplo: quando a coleção é acessada com **Item**, o índice, **2**, deve ser convertido em **longo** para um construtor apropriado será invocado.  
  
```  
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
  
### <a name="casting-ado-object-pointers-with-idispatch-"></a>Convertendo ponteiros do objeto ADO com (IDispatch *)  
 Demonstra como usar o exemplo a seguir do Visual C++ (IDispatch *) para ponteiros do objeto ADO cast.  
  
#### <a name="notes"></a>Observações  
 As observações a seguir correspondem às seções comentadas no exemplo de código.  
  
1.  Especifique um aberto **Conexão** objeto explicitamente codificado **Variant**. Converter com (IDispatch \*) para o construtor correto será invocado. Além disso, defina explicitamente o segundo **variant_t** parâmetro para o valor padrão de **true**, portanto, a contagem de referência de objeto esteja correto quando o **Recordset::Open** termina a operação.  
  
2.  A expressão `(_bstr_t)`, não é uma conversão, mas um **variant_t** operador extrai um **bstr_t** cadeia de caracteres do **Variant** retornado por **valor** .  
  
 A expressão `(char*)`, não é uma conversão, mas um **bstr_t** operador que extrai um ponteiro para a cadeia de caracteres encapsulada em uma **bstr_t** objeto.  
  
 Esta seção de código demonstra alguns comportamentos útil de **variant_t** e **bstr_t** operadores.  
  
```  
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
