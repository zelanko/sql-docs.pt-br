---
title: "Introdução a DiffGrams no SQLXML 4.0 | Microsoft Docs"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: sqlxml
ms.reviewer: 
ms.suite: sql
ms.technology:
- dbe-xml
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- annotations [SQLXML]
- DiffGrams [SQLXML], about DiffGrams
ms.assetid: 1902d67f-baf3-46e6-a36c-b24b5ba6f8ea
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 5743cbab13add72e27351c74424e09bc028496d9
ms.sourcegitcommit: 37f0b59e648251be673389fa486b0a984ce22c81
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/12/2018
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
  
 **\<DataInstance>**  
 O nome desse elemento, **DataInstance**, é usado para fins de explicação nesta documentação. Por exemplo, se DiffGram fosse gerado a partir de um conjunto de dados do .NET Framework, o valor da **nome** propriedade do conjunto de dados deve ser usada como o nome desse elemento. Esse bloco contém todos os dados relevantes depois da alteração, possivelmente incluindo dados que não foram modificados. A lógica de processamento de DiffGram ignora os elementos do bloco para o qual o **diffgr: HasChanges** atributo não for especificado.  
  
 **\<diffgr:before>**  
 Este bloco opcional contém as instâncias do registro original (elementos) que devem ser atualizadas ou excluídas. O banco de dados tabelas sendo modificadas (atualizadas ou excluídas) por DiffGram deve aparecer como elementos de nível superior a  **\<antes >** bloco.  
  
 **\<diffgr:errors>**  
 Este bloco opcional é ignorado lógica de processamento de DiffGram.  
  
## <a name="diffgram-annotations"></a>Anotações de DiffGram  
 Essas anotações são definidas no namespace DiffGram **"urn: schemas-microsoft-com: XML-diffgram-01"**:  
  
 **id**  
 Este atributo é usado para emparelhar os elementos de  **\<antes >** e o  **\<DataInstance >** blocos.  
  
 **hasChanges**  
 Para uma inserção ou uma operação de atualização, o DiffGram deve especificar esse atributo com o valor **inserido** ou **modificado**. Se esse atributo não estiver presente, o elemento correspondente no  **\<DataInstance >** é ignorado pelo processamento lógica e nenhuma atualização é executadas. Para obter exemplos de funcionamento, consulte [exemplos de DiffGram &#40; SQLXML 4.0 &#41; ](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/diffgram/diffgram-examples-sqlxml-4-0.md).  
  
 **parentID**  
 Este atributo é usado para especificar relações pai/filho entre os elementos em DiffGram. Esse atributo só aparece no \<antes > bloco. Ele é usado pelo SQLXML durante a aplicação das atualizações. A relação pai/filho é usada para determinar a ordem na qual os elementos de DiffGram são processados.  
  
## <a name="understanding-the-diffgram-processing-logic"></a>Compreendendo a lógica de processamento de DiffGram  
 A lógica de processamento de DiffGram usa regras específicas para determinar se uma operação é de inserção, atualização ou exclusão. Essas regras são descritas na tabela a seguir.  
  
|Operação|Description|  
|---------------|-----------------|  
|Insert (inserir)|Um DiffGram indica uma operação de inserção quando um elemento aparece no  **\<DataInstance >** bloco, mas não no correspondente  **\<antes >** bloco e o **diffgr: HasChanges** atributo for especificado (**diffgr: HasChanges = inserido**) no elemento. Nesse caso, o DiffGram insere a instância do Registro especificada no  **\<DataInstance >** bloco no banco de dados.<br /><br /> Se o **diffgr: HasChanges** atributo não for especificado, o elemento é ignorado pela lógica de processamento e nenhuma inserção é realizada. Para obter exemplos de funcionamento, consulte [exemplos de DiffGram &#40; SQLXML 4.0 &#41; ](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/diffgram/diffgram-examples-sqlxml-4-0.md).|  
|Update (atualizar)|O DiffGram indica uma operação de atualização quando há um elemento no \<antes > bloco para o qual há um elemento correspondente no  **\<DataInstance >** bloco (ou seja, dois elementos têm um **diffgr: ID** atributo com o mesmo valor) e o **diffgr: HasChanges** atributo é especificado com o valor **modificado** no elemento de  **\<DataInstance >** bloco.<br /><br /> Se o **diffgr: HasChanges** atributo não for especificado no elemento de  **\<DataInstance >** bloco, um erro será retornado pela lógica de processamento. Para obter exemplos de funcionamento, consulte [exemplos de DiffGram &#40; SQLXML 4.0 &#41; ](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/diffgram/diffgram-examples-sqlxml-4-0.md).<br /><br /> Se **diffgr:** é especificado no  **\<antes >** bloquear a relação de pai-filho dos elementos que são especificados pelo **parentID** são usados em determinar a ordem na qual os registros são atualizados.|  
|Delete (excluir)|Um DiffGram indica uma operação de exclusão quando um elemento aparece no  **\<antes >** bloco, mas não no correspondente  **\<DataInstance >** bloco. Nesse caso, o DiffGram exclui a instância do Registro especificada no  **\<antes >** blocos do banco de dados. Para obter exemplos de funcionamento, consulte [exemplos de DiffGram &#40; SQLXML 4.0 &#41; ](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/diffgram/diffgram-examples-sqlxml-4-0.md).<br /><br /> Se **diffgr:** é especificado no  **\<antes >** bloquear a relação de pai-filho dos elementos que são especificados pelo **parentID** são usados em determinar a ordem na qual os registros são excluídos.|  
  
> [!NOTE]  
>  Parâmetros não podem ser passados para DiffGrams.  
  
  
