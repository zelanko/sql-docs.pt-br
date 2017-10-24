---
title: Usando o ADO com o Microsoft Visual Basic | Microsoft Docs
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: H1Hack27Feb2017
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- VB
helpviewer_keywords:
- ADO, Visual Basic
- Visual Basic [ADO]
ms.assetid: 9dfb6784-037d-4f9d-bb7f-b506b4498573
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 8c88dbb57318fe960eab28c463b8c46a5546ffd5
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="using-ado-with-microsoft-visual-basic-and-visual-basic-for-applications"></a>Usando o ADO com o Microsoft Visual Basic e Visual Basic para aplicativos
Configurando um projeto de ADO e escrever código ADO assemelha-se você usar o Visual Basic ou Visual Basic for Applications. Este tópico endereços usando o ADO com Visual Basic e Visual Basic para aplicativos e observa as diferenças.

## <a name="referencing-the-ado-library"></a>Referência de biblioteca do ADO
 A biblioteca do ADO deve ser referenciada pelo seu projeto.

#### <a name="to-reference-ado-from-microsoft-visual-basic"></a>A referência ADO do Microsoft Visual Basic

1.  No Visual Basic, do **projeto** menu, selecione **referências... **.

2.  Selecione **Microsoft ActiveX Data Objects x. x biblioteca** da lista. Verifique se pelo menos as bibliotecas a seguir também são selecionadas:

    -   Visual Basic for Applications

    -   Procedimentos e objetos de tempo de execução do Visual Basic

    -   Procedimentos e objetos do Visual Basic

    -   Automação OLE

3.  Clique em **OK**.

 Você pode usar ADO facilmente com o Visual Basic para aplicativos, usando o Microsoft Access, por exemplo.

#### <a name="to-reference-ado-from-microsoft-access"></a>A referência ADO do Microsoft Access

1.  No Microsoft Access, selecione ou crie um módulo a partir de **módulos** guia o **banco de dados** janela.

2.  Sobre o **ferramentas** menu, selecione **referências... **.

3.  Selecione **Microsoft ActiveX Data Objects x. x biblioteca** da lista. Verifique se pelo menos as bibliotecas a seguir também são selecionadas:

    -   Visual Basic for Applications

    -   Biblioteca de objetos do Microsoft Access 8.0 (ou posterior)

    -   Biblioteca de objetos do Microsoft DAO 3.5 (ou posterior)

4.  Clique em **OK**.

## <a name="creating-ado-objects-in-visual-basic"></a>Criando objetos ADO no Visual Basic
 Para criar uma variável de automação e uma instância de um objeto para aquela variável, você pode usar dois métodos: **Dim** ou **CreateObject**.

### <a name="dim"></a>Dim
 Você pode usar o **novo** palavra-chave with **Dim** declarar e criar instâncias de objetos ADO em uma única etapa:

```
Dim conn As New ADODB.Connection
```

 Como alternativa, o **Dim** instanciação de declaração e o objeto de instrução também pode ser duas etapas:

```
Dim conn As ADODB.Connection
Set conn = New ADODB.Connection
```

> [!NOTE]
>  Não é necessário usar explicitamente o `ADODB` progid com o **Dim** instrução, supondo que você referenciou corretamente a biblioteca do ADO no seu projeto. No entanto, usá-lo garante que não haverá conflitos de nomenclatura com outras bibliotecas.

> [!NOTE]
>  Por exemplo, se você incluir referências ao ADO e DAO no mesmo projeto, você deve incluir um qualificador para especificar qual modelo de objeto a ser usado ao criar uma instância **registros** objetos, como no código a seguir:

```
Dim adoRS As ADODB.Recordset
Dim daoRS As DAO.Recordset
```

### <a name="createobject"></a>CreateObject
 Com o **CreateObject** instanciação de método, a declaração e o objeto deve ser duas etapas distintas:

```
Dim conn1
Set conn1 = CreateObject("ADODB.Connection") As Object
```

 Com os objetos instanciados **CreateObject** são tardia, que significa que eles não são fortemente tipados e preenchimento de linha de comando está desabilitado. No entanto, permitem que você ignore fazem referência à biblioteca de ADO do seu projeto e permite que você instancie versões específicas de objetos. Por exemplo:

```
Set conn1 = CreateObject("ADODB.Connection.2.0") As Object
```

 Você também pode fazer isso criando especificamente uma referência para a biblioteca do ADO versão 2.0 do tipo e criar o objeto.

 Instanciando objetos usando o **CreateObject** método é geralmente mais lento do que o **Dim** instrução.

## <a name="handling-events"></a>Manipulação de eventos
 Para manipular eventos de ADO no Visual Basic, você deve declarar uma variável de nível de módulo usando o **WithEvents** palavra-chave. A variável pode ser declarada apenas como parte de um módulo de classe e deve ser declarada no nível de módulo. Para obter uma discussão mais completa de manipulação de eventos de ADO, consulte [manipulando eventos de ADO](../../../ado/guide/data/handling-ado-events.md).

## <a name="visual-basic-examples"></a>Exemplos do Visual Basic
 Muitos exemplos do Visual Basic são incluídos na documentação do ADO. Para obter mais informações, consulte [exemplos de código ADO no Microsoft Visual Basic](../../../ado/reference/ado-api/ado-code-examples-in-visual-basic.md).

## <a name="see-also"></a>Consulte também
 [Microsoft ActiveX Data Objects (ADO)](../../../ado/microsoft-activex-data-objects-ado.md) [usando o ADO com o Microsoft Visual C++](../../../ado/guide/appendixes/using-ado-with-microsoft-visual-c.md) [usando o ADO com linguagens de script](../../../ado/guide/appendixes/using-ado-with-scripting-languages.md)

