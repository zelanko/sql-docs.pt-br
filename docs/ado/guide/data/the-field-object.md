---
title: O objeto Field | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- Field object [ADO]
ms.assetid: 7d1c4ad5-4be3-42ab-b516-e7133ca300bc
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 80e6576b236db44452c4e89b1d8f3bb8976ab120
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "67923980"
---
# <a name="the-field-object"></a>O objeto Field
Cada objeto de **campo** geralmente corresponde a uma coluna em uma tabela de banco de dados. No entanto, um **campo** também pode representar um ponteiro para outro **conjunto de registros**, chamado de capítulo. Exceções, como colunas de capítulo, serão abordadas posteriormente neste guia.  
  
 Use a propriedade **Value** dos objetos **Field** para definir ou retornar dados para o registro atual. Dependendo da funcionalidade que o provedor expõe, algumas coleções, métodos ou propriedades de um objeto de **campo** podem não estar disponíveis.  
  
 Com as coleções, os métodos e as propriedades de um objeto **Field** , você pode fazer o seguinte:  
  
-   Retornar o nome de um campo usando a propriedade **Name** .  
  
-   Exiba ou altere os dados no campo usando a propriedade **Value** . **Value** é a propriedade padrão do objeto **Field** .  
  
-   Retornar as características básicas de um campo usando as propriedades **Type**, **Precision**e **NumericScale** .  
  
-   Retornar o tamanho declarado de um campo usando a propriedade **DefinedSize** .  
  
-   Retornar o tamanho real dos dados em um determinado campo usando a propriedade **ActualSize** .  
  
-   Determine quais tipos de funcionalidade têm suporte para um determinado campo usando a propriedade **atributos** e a coleção **Propriedades** .  
  
-   Manipule os valores de campos que contêm dados binários longos ou longos de caracteres usando os métodos **AppendChunk** e **GetChunk** .  
  
 Resolva discrepâncias em valores de campo durante a atualização do lote usando as propriedades **OriginalValue** e **subdependvalue** , se o provedor oferecer suporte a atualizações em lotes.  
  
## <a name="describing-a-field"></a>Descrevendo um campo  
 Os tópicos a seguir discutirão as propriedades do objeto [Field](../../../ado/reference/ado-api/field-object.md) que representam informações que descrevem o próprio objeto **Field** , ou seja, metadados sobre o campo. Essas informações podem ser usadas para determinar muito sobre o esquema do **conjunto de registros**. Essas propriedades incluem **Type**, **DefinedSize** e **ActualSize**, **Name**e **NumericScale** e **Precision**.  
  
### <a name="discovering-the-data-type"></a>Descobrindo o tipo de dados  
 A propriedade **Type** indica o tipo de dados do campo. As constantes enumeradas de tipo de dados com suporte no ADO são descritas em [DataTypeEnum](../../../ado/reference/ado-api/datatypeenum.md) na *referência do programador do ADO*.  
  
 Para tipos numéricos de ponto flutuante, como **adNumeric**, você pode obter mais informações. A propriedade **NumericScale** indica quantos dígitos à direita do ponto decimal serão usados para representar valores para o **campo**. A propriedade **Precision** especifica o número máximo de dígitos usados para representar valores para o **campo**.  
  
### <a name="determining-field-size"></a>Determinando o tamanho do campo  
 Use a propriedade **DefinedSize** para determinar a capacidade de dados de um objeto de **campo** .  
  
 Use a propriedade **ActualSize** para retornar o comprimento real do valor de um objeto de **campo** . Para todos os campos, a propriedade **ActualSize** é somente leitura. Se o ADO não puder determinar o comprimento do valor do objeto **Field** , a propriedade **ActualSize** retornará **adUnknown**.  
  
 As propriedades **DefinedSize** e **ActualSize** têm finalidades diferentes. Por exemplo, considere um objeto **Field** com um tipo declarado de **adVarChar** e um valor de propriedade **DefinedSize** de 50, contendo um único caractere. O valor da propriedade **ActualSize** que ele retorna é o comprimento em bytes do único caractere.  
  
### <a name="determining-field-contents"></a>Determinando o conteúdo do campo  
 O identificador da coluna da fonte de dados é representado pela propriedade **Name** do **campo**. A propriedade **Value** do objeto **Field** retorna ou define o conteúdo real dos dados do campo. Essa é a propriedade padrão.  
  
 Para alterar os dados em um campo, defina a propriedade **valor** como igual a um novo valor do tipo correto. O tipo de cursor deve dar suporte a atualizações para alterar o conteúdo de um campo. A validação do banco de dados não é feita aqui no modo de lote, portanto, será necessário verificar se há erros ao chamar **UpdateBatch** nesse caso. Alguns provedores também dão suporte às propriedades **e** **OriginalValue** do objeto **Field** do ADO para ajudá-lo na resolução de conflitos quando você tenta executar atualizações em lotes. Para obter detalhes sobre como resolver esses conflitos, consulte [editando dados](../../../ado/guide/data/editing-data.md).  
  
> [!NOTE]
>  Os valores de **campo do conjunto de registros** não podem ser definidos ao acrescentar novos **campos** a um **conjunto de registros**. Em vez disso, novos **campos** podem ser anexados a um **conjunto de registros**fechado. Em seguida, o **conjunto de registros** deve ser aberto e, em seguida, os valores podem ser atribuídos a esses **campos**.  
  
### <a name="getting-more-field-information"></a>Obtendo mais informações sobre o campo  
 Os objetos ADO têm dois tipos de propriedades: interno e dinâmico. Até esse ponto, somente as propriedades internas do objeto **Field** foram discutidas.  
  
 As propriedades internas são aquelas implementadas no ADO e imediatamente disponibilizadas para qualquer novo objeto, usando a `MyObject.Property` sintaxe. Eles não aparecem como objetos de **Propriedade** na coleção de **Propriedades** de um objeto.  
  
 As propriedades dinâmicas são definidas pelo provedor de dados subjacente e aparecem na coleção de **Propriedades** do objeto ADO apropriado. Por exemplo, uma propriedade específica para o provedor pode indicar se um objeto **Recordset** dá suporte a transações ou atualizações. Essas propriedades adicionais serão exibidas como objetos de **Propriedade** na coleção de **Propriedades** do objeto **Recordset** . As propriedades dinâmicas podem ser referenciadas somente por meio da coleção `MyObject.Properties(0)` , `MyObject.Properties("Name")`usando a sintaxe ou.  
  
 Não é possível excluir qualquer tipo de propriedade.  
  
 Um objeto de **Propriedade** dinâmica tem quatro propriedades internas próprias:  
  
-   A propriedade **Name** é uma cadeia de caracteres que identifica a propriedade.  
  
-   A propriedade **Type** é um inteiro que especifica o tipo de dados Property.  
  
-   A propriedade **Value** é uma variante que contém a configuração de propriedade. **Valor** é a propriedade padrão para um objeto de **Propriedade** .  
  
-   A propriedade **Attributes** é um valor **longo** que indica as características da propriedade específica para o provedor.  
  
 A coleção de **Propriedades** do objeto **Field** contém metadados adicionais sobre o campo. O conteúdo dessa coleção varia dependendo do provedor. O exemplo de código a seguir examina a coleção **Properties** do **conjunto de registros** de exemplo introduzido no início desta seção. Primeiro, ele examina o conteúdo da coleção. Esse código usa o [provedor de OLE DB para SQL Server](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-sql-server.md), portanto, a coleção de **Propriedades** contém informações relevantes para esse provedor.  
  
```  
'BeginFieldProps  
    Dim objProp As ADODB.Property  
  
    For intLoop = 0 To (objFields.Count - 1)  
        Debug.Print objFields.Item(intLoop).Name  
  
        For Each objProp In objFields(intLoop).Properties  
            Debug.Print vbTab & objProp.Name & " = " & objProp.Value  
        Next objProp  
    Next intLoop  
'EndFieldProps  
```  
  
### <a name="dealing-with-binary-data"></a>Lidando com dados binários  
 Use o método [AppendChunk](../../../ado/reference/ado-api/appendchunk-method-ado.md) em um objeto **Field** para preenchê-lo com dados binários longos ou de caractere. Em situações em que a memória do sistema é limitada, você pode usar o método **AppendChunk** para manipular valores longos em partes, em vez de em sua totalidade.  
  
 Se o bit **adFldLong** na propriedade **Attributes** de um objeto **Field** for definido como **true**, você poderá usar o método **AppendChunk** para esse campo.  
  
 A primeira chamada **AppendChunk** em um objeto **Field** grava dados no campo, substituindo os dados existentes. As chamadas **AppendChunk** subsequentes são adicionadas aos dados existentes. Se você estiver acrescentando dados a um campo e, em seguida, definir ou ler o valor de outro campo no registro atual, o ADO assumirá que você terminou de acrescentar dados ao primeiro campo. Se você chamar o método **AppendChunk** no primeiro campo novamente, o ADO interpretará a chamada como uma nova operação **AppendChunk** e substituirá os dados existentes. O acesso a campos em outros objetos **Recordset** que não são clones do primeiro objeto **Recordset** não irá interromper as operações de **AppendChunk** .  
  
 Use o método **GetChunk** em um objeto **Field** para recuperar parte ou todos os seus dados binários ou de caractere longos. Em situações em que a memória do sistema é limitada, você pode usar o método **GetChunk** para manipular valores longos em partes, em vez de em sua totalidade.  
  
 Os dados retornados por uma chamada **GetChunk** são atribuídos à *variável*. Se o *tamanho* for maior que os dados restantes, o método **GetChunk** retornará apenas os dados restantes sem a *variável* de preenchimento com espaços vazios. Se o campo estiver vazio, o método **GetChunk** retornará um valor nulo.  
  
 Cada chamada **GetChunk** subsequente recupera dados a partir de onde a chamada **GetChunk** anterior parou. No entanto, se você estiver recuperando dados de um campo e, em seguida, definir ou ler o valor de outro campo no registro atual, o ADO pressupõe que você concluiu a recuperação de dados do primeiro campo. Se você chamar o método **GetChunk** no primeiro campo, o ADO interpretará a chamada como uma nova operação **GetChunk** e começará a ler a partir do início dos dados. O acesso a campos em outros objetos de **conjunto de registros** que não são clones do primeiro objeto **Recordset** não irá interromper as operações **GetChunk** .  
  
 Se o bit **adFldLong** na propriedade **Attributes** de um objeto **Field** for definido como **true**, você poderá usar o método **GetChunk** para esse campo.  
  
 Se não houver registro atual quando você usar o método **GetChunk** ou **AppendChunk** em um objeto **Field** , ocorrerá o erro 3021 (nenhum registro atual).  
  
 Para obter um exemplo de como usar esses métodos para manipular dados binários, consulte os exemplos de método [AppendChunk](../../../ado/reference/ado-api/appendchunk-method-ado.md) e [GetChunk](../../../ado/reference/ado-api/getchunk-method-ado.md) na *referência do programador do ADO*.
