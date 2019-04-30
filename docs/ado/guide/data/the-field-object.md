---
title: O objeto de campo | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: e152c3147ab7c316494c6891424c0a7c8173f002
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63062655"
---
# <a name="the-field-object"></a>O objeto Field
Cada **campo** objeto normalmente corresponde a uma coluna em uma tabela de banco de dados. No entanto, uma **campo** também pode representar um ponteiro para outro **conjunto de registros**, chamado de um capítulo. Exceções, como colunas de capítulo, serão abordadas posteriormente neste guia.  
  
 Use o **valor** propriedade de **campo** objetos para definir ou retornar dados para o registro atual. Dependendo da funcionalidade de provedor expõe, algumas coleções, métodos ou propriedades de um **campo** objeto pode não estar disponível.  
  
 Com as coleções, métodos e propriedades de um **campo** do objeto, você pode fazer o seguinte:  
  
-   Retornar o nome de um campo usando o **nome** propriedade.  
  
-   Exibir ou alterar os dados no campo usando o **valor** propriedade. **Valor** é a propriedade padrão de **campo** objeto.  
  
-   Retornar as características básicas de um campo usando o **tipo**, **Precision**, e **NumericScale** propriedades.  
  
-   Retornar o tamanho declarado de um campo usando o **DefinedSize** propriedade.  
  
-   Retornar o tamanho real dos dados em um determinado campo usando o **ActualSize** propriedade.  
  
-   Determinar quais tipos de funcionalidade são suportados para um determinado campo, usando o **atributos** propriedade e **propriedades** coleção.  
  
-   Manipular os valores dos campos que contêm dados binários longos ou de caracteres longa, usando o **AppendChunk** e **GetChunk** métodos.  
  
 Resolver as discrepâncias nos valores de campo durante a atualização em lotes usando o **OriginalValue** e **UnderlyingValue** propriedades, se o provedor oferece suporte a atualizações em lotes.  
  
## <a name="describing-a-field"></a>Que descreve um campo  
 Os tópicos a seguir será discutem as propriedades do [campo](../../../ado/reference/ado-api/field-object.md) objeto que representam informações que descrevem o **campo** objeto em si – ou seja, os metadados sobre o campo. Essas informações podem ser usadas para determinar muito sobre o esquema do **conjunto de registros**. Essas propriedades incluem **tipo**, **DefinedSize** e **ActualSize**, **nome**, e **NumericScale**e **precisão**.  
  
### <a name="discovering-the-data-type"></a>Descobrir o tipo de dados  
 O **tipo** propriedade indica o tipo de dados do campo. O tipo de dados enumerados constantes que são compatíveis com o ADO são descritas em [DataTypeEnum](../../../ado/reference/ado-api/datatypeenum.md) na *referência do programador do ADO*.  
  
 Para tipos numéricos, de ponto flutuante **adNumeric**, você pode obter mais informações. O **NumericScale** propriedade indica o número de dígitos à direita do ponto decimal será usado para representar os valores para o **campo**. O **precisão** propriedade especifica o número máximo de dígitos usados para representar valores para o **campo**.  
  
### <a name="determining-field-size"></a>Determinando o tamanho do campo  
 Use o **DefinedSize** propriedade para determinar a capacidade de dados de uma **campo** objeto.  
  
 Use o **ActualSize** propriedade para retornar o comprimento real de uma **campo** valor do objeto. Todos os campos, o **ActualSize** propriedade é somente leitura. Se o ADO não é possível determinar o comprimento de **campo** valor do objeto, o **ActualSize** propriedade retorna **adUnknown**.  
  
 O **DefinedSize** e **ActualSize** propriedades têm finalidades diferentes. Por exemplo, considere uma **campo** objeto com um tipo declarado do **adVarChar** e um **DefinedSize** valor da propriedade de 50, que contém um único caractere. O **ActualSize** é de valor de propriedade que retorna o comprimento em bytes do caractere único.  
  
### <a name="determining-field-contents"></a>Determinando o conteúdo do campo  
 O identificador da coluna da fonte de dados é representado pela **nome** propriedade da **campo**. O **valor** propriedade da **campo** objeto retorna ou define o conteúdo de dados real do campo. Isso é a propriedade padrão.  
  
 Para alterar os dados em um campo, defina as **valor** propriedade igual a um novo valor do tipo correto. O tipo de cursor deve oferecer suporte a atualizações para alterar o conteúdo de um campo. Validação de banco de dados não é feita aqui no modo de lote, portanto, será necessário verificar se há erros quando você chama **UpdateBatch** nesse caso. Alguns provedores também oferecem suporte ADO **campo** do objeto **UnderlyingValue** e **OriginalValue** propriedades para ajudar a resolver conflitos durante a tentativa Execute atualizações em lotes. Para obter detalhes sobre como resolver esses conflitos, consulte [editando dados](../../../ado/guide/data/editing-data.md).  
  
> [!NOTE]
>  **Recordset Field** valores não podem ser definidos ao anexar novo **campos** para um **conjunto de registros**. Em vez disso, novos **campos** pode ser anexado a um fechado **conjunto de registros**. Em seguida, a **conjunto de registros** deve ser aberto e, em seguida, só podem ser atribuídos valores esses **campos**.  
  
### <a name="getting-more-field-information"></a>Obtendo mais informações de campo  
 Objetos do ADO têm dois tipos de propriedades: interna e dinâmicos. Neste ponto, apenas as propriedades internas do **campo** objeto foram discutidos.  
  
 Propriedades internas são as propriedades implementadas no ADO e fica imediatamente disponíveis para qualquer novo objeto, usando o `MyObject.Property` sintaxe. Eles não aparecem como **propriedade** objetos em um objeto **propriedades** coleção.  
  
 Propriedades dinâmicas são definidas pelo provedor de dados subjacente e aparecem na **propriedades** coleção do objeto ADO apropriado. Por exemplo, uma propriedade específica do provedor pode indicar se um **Recordset** objeto dá suporte a transações ou atualizando. Essas propriedades adicionais serão exibido como **propriedade** objetos em que **conjunto de registros** do objeto **propriedades** coleção. Propriedades dinâmicas podem ser referenciadas apenas por meio da coleção, usando a sintaxe `MyObject.Properties(0)` ou `MyObject.Properties("Name")`.  
  
 Você não pode excluir um desses tipos de propriedade.  
  
 Dinâmico **propriedade** objeto tem quatro propriedades internas de seu próprio:  
  
-   O **nome** propriedade é uma cadeia de caracteres que identifica a propriedade.  
  
-   O **tipo** propriedade é um inteiro que especifica o tipo de dados de propriedade.  
  
-   O **valor** propriedade é uma variante que contém a configuração da propriedade. **Valor** é a propriedade padrão para um **propriedade** objeto.  
  
-   O **atributos** propriedade é um **longo** valor que indica as características da propriedade específica do provedor.  
  
 O **propriedades** coleta para o **campo** objeto contém metadados adicionais sobre o campo. O conteúdo desta coleção variar dependendo do provedor. O exemplo de código a seguir examina o **propriedades** coleção da amostra **Recordset** introduzido no início desta seção. Ele primeiro procura o conteúdo da coleção. Esse código usa o [OLE DB Provider for SQL Server](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-sql-server.md), portanto, o **propriedades** coleção contém informações relevantes para esse provedor.  
  
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
 Use o [AppendChunk](../../../ado/reference/ado-api/appendchunk-method-ado.md) método em um **campo** objeto preenchê-lo com dados binários longos ou de caractere. Em situações em que a memória do sistema é limitada, você pode usar o **AppendChunk** método para manipular valores longos em partes em vez de em sua totalidade.  
  
 Se o **adFldLong** bit na **atributos** propriedade de um **campo** objeto é definido como **True**, você pode usar o  **AppendChunk** método para esse campo.  
  
 A primeira **AppendChunk** chamar em um **campo** objeto grava dados no campo, substituindo quaisquer dados existentes. Subsequentes **AppendChunk** chamadas adicionam aos dados existentes. Se você está anexando dados a um campo e, em seguida, você pode definir ou ler o valor de outro campo no registro atual, o ADO pressupõe que você esteja concluído acrescentando dados para o primeiro campo. Se você chamar o **AppendChunk** método no primeiro campo novamente, ADO interpreta a chamada como um novo **AppendChunk** operação e substitui os dados existentes. Acessar campos em outros **conjunto de registros** objetos que não são clones do primeiro **conjunto de registros** objeto não interromperá **AppendChunk** operações.  
  
 Use o **GetChunk** método em um **campo** objeto para recuperar parte ou todos os seus dados binários longos ou de caractere. Em situações em que a memória do sistema é limitada, você pode usar o **GetChunk** método para manipular valores longos em partes, em vez de em sua totalidade.  
  
 Os dados que um **GetChunk** chamada retorna é atribuído a *variável*. Se *tamanho* é maior do que os dados restantes, o **GetChunk** método retorna apenas os dados restantes sem preenchimento *variável* com espaços vazios. Se o campo estiver vazio, o **GetChunk** método retorna um valor nulo.  
  
 Cada subsequentes **GetChunk** chamada recupera dados a partir de onde o anterior **GetChunk** chamada parou. No entanto, se você está recuperando dados de um campo e, em seguida, definir ou ler o valor de outro campo no registro atual, o ADO presume que você concluiu a recuperação de dados do primeiro campo. Se você chamar o **GetChunk** método no primeiro campo novamente, ADO interpreta a chamada como um novo **GetChunk** operação e começa a ler desde o início dos dados. Acessar campos em outros **conjunto de registros** objetos que não são clones do primeiro **conjunto de registros** objeto não interromperá **GetChunk** operações.  
  
 Se o **adFldLong** bit na **atributos** propriedade de um **campo** objeto é definido como **True**, você pode usar o **GetChunk**  método para esse campo.  
  
 Se não houver nenhum registro atual quando você usa o **GetChunk** ou **AppendChunk** método em um **campo** do objeto, ocorrerá o erro 3021 (nenhum registro atual).  
  
 Para obter um exemplo de como usar esses métodos para manipular dados binários, consulte o [método AppendChunk](../../../ado/reference/ado-api/appendchunk-method-ado.md) e [método GetChunk](../../../ado/reference/ado-api/getchunk-method-ado.md) exemplos para o *referência do programador do ADO*.
