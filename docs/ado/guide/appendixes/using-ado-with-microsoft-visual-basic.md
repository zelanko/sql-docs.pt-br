---
title: Usando o ADO com o Microsoft Visual Basic | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
dev_langs:
- VB
helpviewer_keywords:
- ADO, Visual Basic
- Visual Basic [ADO]
ms.assetid: 9dfb6784-037d-4f9d-bb7f-b506b4498573
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d409f874e9fcec059c01ddef91d83d8a70fdeb47
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62864512"
---
# <a name="using-ado-with-microsoft-visual-basic-and-visual-basic-for-applications"></a>Usando o ADO com o Microsoft Visual Basic e Visual Basic for Applications
Configurando um projeto do ADO e escrever código em ADO são semelhante se você usar o Visual Basic ou Visual Basic for Applications. Este tópico aborda usando o ADO com o Visual Basic e Visual Basic for Applications e observa as diferenças.

## <a name="referencing-the-ado-library"></a>Referência à biblioteca do ADO
 A biblioteca do ADO deve ser referenciada pelo seu projeto.

#### <a name="to-reference-ado-from-microsoft-visual-basic"></a>Para fazer referência a ADO do Microsoft Visual Basic

1.  No Visual Basic, do **Project** menu, selecione **referências...** .

2.  Selecione **Microsoft ActiveX Data Objects x. x biblioteca** na lista. Verifique se pelo menos as seguintes bibliotecas também são selecionadas:

    -   Visual Basic for Applications

    -   Procedimentos e objetos de tempo de execução do Visual Basic

    -   Procedimentos e objetos do Visual Basic

    -   Automação OLE

3.  Clique em **OK**.

 Você pode usar ADO facilmente com o Visual Basic para aplicativos, usando o Microsoft Access, por exemplo.

#### <a name="to-reference-ado-from-microsoft-access"></a>Para fazer referência a ADO do Microsoft Access

1.  No Microsoft Access, selecione ou crie um módulo a partir o **módulos** guia o **banco de dados** janela.

2.  Sobre o **ferramentas** menu, selecione **referências...** .

3.  Selecione **Microsoft ActiveX Data Objects x. x biblioteca** na lista. Verifique se pelo menos as seguintes bibliotecas também são selecionadas:

    -   Visual Basic for Applications

    -   Biblioteca de objetos do Microsoft Access 8.0 (ou posterior)

    -   Biblioteca de objetos do Microsoft DAO 3.5 (ou posterior)

4.  Clique em **OK**.

## <a name="creating-ado-objects-in-visual-basic"></a>Criando objetos do ADO no Visual Basic
 Para criar uma variável de automação e uma instância de um objeto para essa variável, você pode usar dois métodos: **Dim** ou **CreateObject**.

### <a name="dim"></a>Dim
 Você pode usar o **New** palavra-chave with **Dim** declarar e criar instâncias de objetos do ADO em uma única etapa:

```
Dim conn As New ADODB.Connection
```

 Como alternativa, o **Dim** instanciação de declaração e objeto de instrução também pode ser de duas etapas:

```
Dim conn As ADODB.Connection
Set conn = New ADODB.Connection
```

> [!NOTE]
>  Não é necessário usar explicitamente o `ADODB` progid com o **Dim** instrução, supondo que você referenciou corretamente a biblioteca do ADO em seu projeto. No entanto, usá-lo garante que você não terá conflitos de nomenclatura com outras bibliotecas.

> [!NOTE]
>  Por exemplo, se você incluir referências ao ADO e ao DAO no mesmo projeto, você deve incluir um qualificador para especificar qual modelo de objeto a ser usado ao criar uma instância **Recordset** objetos, como no código a seguir:

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

 Com os objetos instanciados **CreateObject** são com associação tardia, que significa que eles não são fortemente tipados e preenchimento de linha de comando está desabilitado. No entanto, permitir que você ignore a referência à biblioteca do ADO do seu projeto e permite que você crie uma instância versões específicas de objetos. Por exemplo: 

```
Set conn1 = CreateObject("ADODB.Connection.2.0") As Object
```

 Você também pode fazer isso criando especificamente uma referência para a biblioteca do ADO versão 2.0 do tipo e criar o objeto.

 Instanciando objetos usando o **CreateObject** método é geralmente mais lento do que o **Dim** instrução.

## <a name="handling-events"></a>Manipulação de eventos
 Para tratar eventos ADO no Microsoft Visual Basic, você deve declarar uma variável de nível de módulo usando o **WithEvents** palavra-chave. A variável pode ser declarada somente como parte de um módulo de classe e deve ser declarada no nível de módulo. Para obter uma discussão mais completa de manipulação de eventos ADO, consulte [manipulação de eventos ADO](../../../ado/guide/data/handling-ado-events.md).

## <a name="visual-basic-examples"></a>Exemplos do Visual Basic
 Muitos exemplos de Visual Basic são incluídos na documentação do ADO. Para obter mais informações, consulte [exemplos de código ADO no Microsoft Visual Basic](../../../ado/reference/ado-api/ado-code-examples-in-visual-basic.md).

## <a name="see-also"></a>Consulte também
 [Microsoft ActiveX Data Objects (ADO)](../../../ado/microsoft-activex-data-objects-ado.md) [usando o ADO com o Microsoft Visual C++](../../../ado/guide/appendixes/using-ado-with-microsoft-visual-c.md) [usando o ADO com linguagens de script](../../../ado/guide/appendixes/using-ado-with-scripting-languages.md)
