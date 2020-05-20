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
author: rothja
ms.author: jroth
ms.openlocfilehash: e86bc925313a24a390dffc8f4e2d9e91e4db1c61
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2020
ms.locfileid: "82761584"
---
# <a name="using-ado-with-microsoft-visual-basic-and-visual-basic-for-applications"></a>Usando o ADO com o Microsoft Visual Basic e Visual Basic for Applications
Configurar um projeto do ADO e escrever código ADO é semelhante se você usar Visual Basic ou Visual Basic for Applications. Este tópico aborda o uso do ADO com Visual Basic e Visual Basic for Applications e observações sobre qualquer diferença.

## <a name="referencing-the-ado-library"></a>Referenciando a biblioteca do ADO
 A biblioteca ADO deve ser referenciada pelo seu projeto.

#### <a name="to-reference-ado-from-microsoft-visual-basic"></a>Para fazer referência ao ADO do Microsoft Visual Basic

1.  Em Visual Basic, no menu **projeto** , selecione **referências...**.

2.  Selecione **biblioteca do Microsoft ActiveX Data Objects x. x** na lista. Verifique se pelo menos as seguintes bibliotecas também estão selecionadas:

    -   Visual Basic for Applications

    -   Procedimentos e objetos do Visual Basic Runtime

    -   Objetos e procedimentos do Visual Basic

    -   Automação OLE

3.  Clique em **OK**.

 Você pode usar o ADO tão facilmente com Visual Basic for Applications, usando o Microsoft Access, por exemplo.

#### <a name="to-reference-ado-from-microsoft-access"></a>Para fazer referência ao ADO do Microsoft Access

1.  No Microsoft Access, selecione ou crie um módulo na guia **módulos** da janela **banco de dados** .

2.  No menu **ferramentas** , selecione **referências...**.

3.  Selecione **biblioteca do Microsoft ActiveX Data Objects x. x** na lista. Verifique se pelo menos as seguintes bibliotecas também estão selecionadas:

    -   Visual Basic for Applications

    -   Biblioteca de objetos do Microsoft Access 8,0 (ou posterior)

    -   Biblioteca de objetos do Microsoft DAO 3,5 (ou posterior)

4.  Clique em **OK**.

## <a name="creating-ado-objects-in-visual-basic"></a>Criando objetos ADO no Visual Basic
 Para criar uma variável de automação e uma instância de um objeto para essa variável, você pode usar dois métodos: **Dim** ou **CreateObject**.

### <a name="dim"></a>Escura
 Você pode usar a **nova** palavra-chave com **Dim** para declarar e criar instâncias de objetos ADO em uma única etapa:

```
Dim conn As New ADODB.Connection
```

 Como alternativa, a declaração de instrução **Dim** e a instanciação de objeto também podem ser duas etapas:

```
Dim conn As ADODB.Connection
Set conn = New ADODB.Connection
```

> [!NOTE]
>  Não é necessário usar explicitamente o `ADODB` ProgID com a instrução **Dim** , supondo que você tenha referenciado corretamente a biblioteca do ADO em seu projeto. No entanto, usá-lo garante que você não terá conflitos de nomenclatura com outras bibliotecas.

> [!NOTE]
>  Por exemplo, se você incluir referências ao ADO e ao DAO no mesmo projeto, deverá incluir um qualificador para especificar qual modelo de objeto usar ao instanciar objetos **Recordset** , como no código a seguir:

```
Dim adoRS As ADODB.Recordset
Dim daoRS As DAO.Recordset
```

### <a name="createobject"></a>CreateObject
 Com o método **CreateObject** , a declaração e a instanciação de objeto devem ser duas etapas discretas:

```
Dim conn1
Set conn1 = CreateObject("ADODB.Connection") As Object
```

 Os objetos instanciados com **CreateObject** são de associação tardia, o que significa que eles não são fortemente tipados e a conclusão da linha de comando está desabilitada. No entanto, ele permite ignorar a referência à biblioteca do ADO do seu projeto e permite que você crie uma instância de versões específicas de objetos. Por exemplo:

```
Set conn1 = CreateObject("ADODB.Connection.2.0") As Object
```

 Você também pode fazer isso criando especificamente uma referência à biblioteca de tipos do ADO versão 2,0 e criando o objeto.

 Criar uma instância de objetos usando o método **CreateObject** normalmente é mais lento do que usar a instrução **Dim** .

## <a name="handling-events"></a>Tratando eventos
 Para manipular eventos ADO no Microsoft Visual Basic, você deve declarar uma variável em nível de módulo usando a palavra-chave **WithEvents** . A variável só pode ser declarada como parte de um módulo de classe e deve ser declarada no nível do módulo. Para obter uma discussão mais completa sobre como lidar com eventos ADO, consulte [manipulando eventos ADO](../../../ado/guide/data/handling-ado-events.md).

## <a name="visual-basic-examples"></a>Exemplos de Visual Basic
 Muitos exemplos de Visual Basic estão incluídos na documentação do ADO. Para obter mais informações, consulte [exemplos de código ADO no Microsoft Visual Basic](../../../ado/reference/ado-api/ado-code-examples-in-visual-basic.md).

## <a name="see-also"></a>Consulte Também
 [Microsoft ActiveX Data Objects (ADO)](../../../ado/microsoft-activex-data-objects-ado.md) [usando ADO com Microsoft Visual C++](../../../ado/guide/appendixes/using-ado-with-microsoft-visual-c.md) [usando ADO com linguagens de script](../../../ado/guide/appendixes/using-ado-with-scripting-languages.md)
