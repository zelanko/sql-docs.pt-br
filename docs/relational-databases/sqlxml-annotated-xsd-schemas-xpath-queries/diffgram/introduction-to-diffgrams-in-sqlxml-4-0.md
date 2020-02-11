---
title: Introdução a DiffGrams em SQLXML 4.0
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
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 3994a9d0bc863367edf5b1844772b94a63f19d4d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "75257250"
---
# <a name="introduction-to-diffgrams-in-sqlxml-40"></a>Introdução a DiffGrams em SQLXML 4.0
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
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
  
 **\<>de DataInstance**  
 O nome desse elemento, **DataInstance**, é usado para fins explicativos nesta documentação. Por exemplo, se o DiffGram foi gerado a partir de um conjunto de um DataSet no .NET Framework, o valor da propriedade **Name** do conjunto de valores seria usado como o nome desse elemento. Esse bloco contém todos os dados relevantes depois da alteração, possivelmente incluindo dados que não foram modificados. A lógica de processamento de DiffGram ignora os elementos neste bloco para os quais o atributo **diffgr: hasChanges** não está especificado.  
  
 **\<diffgr: antes de>**  
 Este bloco opcional contém as instâncias do registro original (elementos) que devem ser atualizadas ou excluídas. Todas as tabelas de banco de dados que estão sendo modificadas (atualizadas ou excluídas) pelo DiffGram devem aparecer como elementos de nível superior no bloco ** \<before>** .  
  
 **\<diffgr: erros>**  
 Este bloco opcional é ignorado lógica de processamento de DiffGram.  
  
## <a name="diffgram-annotations"></a>Anotações de DiffGram  
 Essas anotações são definidas no namespace DiffGram **"urn: schemas-microsoft-com: XML-DiffGram-01"**:  
  
 **sessão**  
 Esse atributo é usado para emparelhar os elementos nos blocos ** \<antes>** e ** \<DataInstance>** .  
  
 **hasChanges**  
 Para uma operação de inserção ou de atualização, o DiffGram deve especificar esse atributo com o valor **inserido** ou **modificado**. Se esse atributo não estiver presente, o elemento correspondente na ** \<>de DataInstance** será ignorado pela lógica de processamento e nenhuma atualização será executada. Para obter exemplos de trabalho, consulte [exemplos de DiffGram &#40;SQLXML 4,0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/diffgram/diffgram-examples-sqlxml-4-0.md).  
  
 **parentID**  
 Este atributo é usado para especificar relações pai/filho entre os elementos em DiffGram. Esse atributo aparece apenas no bloco \<before>. Ele é usado pelo SQLXML durante a aplicação das atualizações. A relação pai/filho é usada para determinar a ordem na qual os elementos de DiffGram são processados.  
  
## <a name="understanding-the-diffgram-processing-logic"></a>Compreendendo a lógica de processamento de DiffGram  
 A lógica de processamento de DiffGram usa regras específicas para determinar se uma operação é de inserção, atualização ou exclusão. Essas regras são descritas na tabela a seguir.  
  
|Operação|DESCRIÇÃO|  
|---------------|-----------------|  
|Insert|Um DiffGram indica uma operação de inserção quando um elemento é exibido no bloco de ** \<>de DataInstance** , mas não no bloco correspondente ** \<antes>** e o atributo **diffgr: hasChanges** é especificado (**diffgr: hasChanges = inserted**) no elemento. Nesse caso, o DiffGram insere a instância de registro que é especificada no bloco de ** \<>de DataInstance** no banco de dados.<br /><br /> Se o atributo **diffgr: hasChanges** não for especificado, o elemento será ignorado pela lógica de processamento e nenhuma inserção será executada. Para obter exemplos de trabalho, consulte [exemplos de DiffGram &#40;SQLXML 4,0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/diffgram/diffgram-examples-sqlxml-4-0.md).|  
|Atualizar|O DiffGram indica uma operação de atualização quando há um elemento no bloco \<before> para o qual há um elemento correspondente no ** \<bloco de>de DataInstance** (ou seja, ambos os elementos têm um atributo **diffgr: ID** com o mesmo valor) e o atributo **diffgr: hasChanges** é especificado com o valor **modificado** no elemento no ** \<bloco de>DataInstance** .<br /><br /> Se o atributo **diffgr: hasChanges** não for especificado no elemento no ** \<bloco de>DataInstance** , um erro será retornado pela lógica de processamento. Para obter exemplos de trabalho, consulte [exemplos de DiffGram &#40;SQLXML 4,0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/diffgram/diffgram-examples-sqlxml-4-0.md).<br /><br /> Se **diffgr: parentID** for especificado no bloco ** \<before>** , a relação pai-filho dos elementos especificados por **parentID** será usada para determinar a ordem na qual os registros são atualizados.|  
|Excluir|Um DiffGram indica uma operação de exclusão quando um elemento é exibido no bloco ** \<anterior>** , mas não no bloco de ** \<>de DataInstance** correspondente. Nesse caso, o DiffGram exclui a instância de registro especificada no bloco ** \<before>** do banco de dados. Para obter exemplos de trabalho, consulte [exemplos de DiffGram &#40;SQLXML 4,0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/diffgram/diffgram-examples-sqlxml-4-0.md).<br /><br /> Se **diffgr: parentID** for especificado no bloco ** \<before>** , a relação pai-filho dos elementos especificados por **parentID** será usada para determinar a ordem na qual os registros são excluídos.|  
  
> [!NOTE]  
>  Parâmetros não podem ser passados para DiffGrams.  
  
  
