---
title: Introdução a DiffGrams em SQLXML 4.0
description: Saiba mais sobre o formato, as anotações e a lógica de processamento de DiffGrams no SQLXML 4,0.
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- annotations [SQLXML]
- DiffGrams [SQLXML], about DiffGrams
ms.assetid: 1902d67f-baf3-46e6-a36c-b24b5ba6f8ea
author: MightyPen
ms.author: genemi
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 66a58dfb19cf8f53f775bac663d5ba3e6147711b
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97414865"
---
# <a name="introduction-to-diffgrams-in-sqlxml-40"></a>Introdução a DiffGrams em SQLXML 4.0
[!INCLUDE [SQL Server Azure SQL Database](../../../includes/applies-to-version/sql-asdb.md)]
  Este tópico fornece uma breve introdução a DiffGrams.  
  
## <a name="diffgram-format"></a>Formato DiffGram  
 Este é o formato geral de DiffGram:  
  
```  
<?xml version="1.0"?>  
<diffgr:diffgram   
         xmlns:msdata="urn:schemas-microsoft-com:xml-msdata"  
         xmlns:diffgr="urn:schemas-microsoft-com:xml-diffgram-v1"  
         xmlns:xsd="http://www.w3.org/2001/XMLSchema">  
   <DataInstance>  
      ...  
   </DataInstance>  
   [<diffgr:before>  
        ...  
   </diffgr:before>]  
  
   [<diffgr:errors>  
        ...  
   </diffgr:errors>]  
</diffgr:diffgram>  
```  
  
 O formato DiffGram consiste nestes blocos:  
  
 **\<DataInstance>**  
 O nome desse elemento, **DataInstance**, é usado para fins explicativos nesta documentação. Por exemplo, se o DiffGram foi gerado a partir de um conjunto de um DataSet no .NET Framework, o valor da propriedade **Name** do conjunto de valores seria usado como o nome desse elemento. Esse bloco contém todos os dados relevantes depois da alteração, possivelmente incluindo dados que não foram modificados. A lógica de processamento de DiffGram ignora os elementos neste bloco para os quais o atributo **diffgr: hasChanges** não está especificado.  
  
 **\<diffgr:before>**  
 Este bloco opcional contém as instâncias do registro original (elementos) que devem ser atualizadas ou excluídas. Todas as tabelas de banco de dados que estão sendo modificadas (atualizadas ou excluídas) pelo DiffGram devem aparecer como elementos de nível superior no **\<before>** bloco.  
  
 **\<diffgr:errors>**  
 Este bloco opcional é ignorado lógica de processamento de DiffGram.  
  
## <a name="diffgram-annotations"></a>Anotações de DiffGram  
 Essas anotações são definidas no namespace DiffGram **"urn: schemas-microsoft-com: XML-DiffGram-01"**:  
  
 **id**  
 Esse atributo é usado para emparelhar os elementos nos **\<before>** blocos e **\<DataInstance>** .  
  
 **hasChanges**  
 Para uma operação de inserção ou de atualização, o DiffGram deve especificar esse atributo com o valor **inserido** ou **modificado**. Se esse atributo não estiver presente, o elemento correspondente no **\<DataInstance>** será ignorado pela lógica de processamento e nenhuma atualização será executada. Para obter exemplos de trabalho, consulte [exemplos de DiffGram &#40;SQLXML 4,0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/diffgram/diffgram-examples-sqlxml-4-0.md).  
  
 **parentID**  
 Este atributo é usado para especificar relações pai/filho entre os elementos em DiffGram. Esse atributo aparece apenas no \<before> bloco. Ele é usado pelo SQLXML durante a aplicação das atualizações. A relação pai/filho é usada para determinar a ordem na qual os elementos de DiffGram são processados.  
  
## <a name="understanding-the-diffgram-processing-logic"></a>Compreendendo a lógica de processamento de DiffGram  
 A lógica de processamento de DiffGram usa regras específicas para determinar se uma operação é de inserção, atualização ou exclusão. Essas regras são descritas na tabela a seguir.  
  
|Operação|Descrição|  
|---------------|-----------------|  
|Inserir|Um DiffGram indica uma operação de inserção quando um elemento é exibido no **\<DataInstance>** bloco, mas não no **\<before>** bloco correspondente, e o atributo **diffgr: hasChanges** é especificado (**diffgr: hasChanges = inserted**) no elemento. Nesse caso, o DiffGram insere a instância de registro especificada no **\<DataInstance>** bloco no banco de dados.<br /><br /> Se o atributo **diffgr: hasChanges** não for especificado, o elemento será ignorado pela lógica de processamento e nenhuma inserção será executada. Para obter exemplos de trabalho, consulte [exemplos de DiffGram &#40;SQLXML 4,0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/diffgram/diffgram-examples-sqlxml-4-0.md).|  
|Atualizar|O DiffGram indica uma operação de atualização quando há um elemento no \<before> bloco para o qual há um elemento correspondente no **\<DataInstance>** bloco (ou seja, ambos os elementos têm um atributo **diffgr: ID** com o mesmo valor) e o atributo **diffgr: hasChanges** é especificado com o valor **modificado** no elemento no **\<DataInstance>** bloco.<br /><br /> Se o atributo **diffgr: hasChanges** não for especificado no elemento no **\<DataInstance>** bloco, um erro será retornado pela lógica de processamento. Para obter exemplos de trabalho, consulte [exemplos de DiffGram &#40;SQLXML 4,0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/diffgram/diffgram-examples-sqlxml-4-0.md).<br /><br /> Se **diffgr: parentID** for especificado no **\<before>** bloco, a relação pai-filho dos elementos especificados por **parentID** será usada para determinar a ordem na qual os registros são atualizados.|  
|Excluir|Um DiffGram indica uma operação de exclusão quando um elemento é exibido no **\<before>** bloco, mas não no **\<DataInstance>** bloco correspondente. Nesse caso, o DiffGram exclui a instância de registro especificada no **\<before>** bloco do banco de dados. Para obter exemplos de trabalho, consulte [exemplos de DiffGram &#40;SQLXML 4,0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/diffgram/diffgram-examples-sqlxml-4-0.md).<br /><br /> Se **diffgr: parentID** for especificado no **\<before>** bloco, a relação pai-filho dos elementos especificados por **parentID** será usada para determinar a ordem na qual os registros são excluídos.|  
  
> [!NOTE]  
>  Parâmetros não podem ser passados para DiffGrams.  
  
  
