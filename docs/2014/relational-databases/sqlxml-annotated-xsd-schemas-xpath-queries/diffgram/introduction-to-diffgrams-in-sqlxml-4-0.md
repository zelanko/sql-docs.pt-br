---
title: Introdução a DiffGrams em SQLXML 4.0 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.topic: reference
helpviewer_keywords:
- annotations [SQLXML]
- DiffGrams [SQLXML], about DiffGrams
ms.assetid: 1902d67f-baf3-46e6-a36c-b24b5ba6f8ea
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: f7f94ac060cc4f76472c56c284636c09349261de
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48160766"
---
# <a name="introduction-to-diffgrams-in-sqlxml-40"></a>Introdução a DiffGrams em SQLXML 4.0
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
 O nome deste elemento **DataInstance**, é usado para fins de explicação nesta documentação. Por exemplo, se DiffGram fosse gerado a partir de um conjunto de dados no .NET Framework, o valor da **nome** propriedade do conjunto de dados seria usada como o nome deste elemento. Esse bloco contém todos os dados relevantes depois da alteração, possivelmente incluindo dados que não foram modificados. A lógica de processamento de DiffGram ignora os elementos nesse bloco para o qual o **diffgr: HasChanges** atributo não for especificado.  
  
 **\<diffgr:before>**  
 Este bloco opcional contém as instâncias do registro original (elementos) que devem ser atualizadas ou excluídas. O banco de dados tabelas que estão sendo modificadas (atualizadas ou excluídas) por DiffGram deve aparecer como elementos de nível superior na  **\<antes de >** bloco.  
  
 **\<diffgr:errors>**  
 Este bloco opcional é ignorado lógica de processamento de DiffGram.  
  
## <a name="diffgram-annotations"></a>Anotações de DiffGram  
 Essas anotações são definidas no namespace DiffGram **"urn: schemas-microsoft-com: XML-diffgram-01"**:  
  
 **id**  
 Esse atributo é usado para emparelhar os elementos a  **\<antes de >** e o  **\<DataInstance >** blocos.  
  
 **hasChanges**  
 Para uma inserção ou uma operação de atualização, o DiffGram deve especificar esse atributo com o valor **inserido** ou **modificado**. Se esse atributo não estiver presente, o elemento correspondente na  **\<DataInstance >** é ignorada pelo processamento lógica e nenhuma atualização é executadas. Para obter exemplos de funcionamento, consulte [exemplos de DiffGram &#40;SQLXML 4.0&#41;](diffgram-examples-sqlxml-4-0.md).  
  
 **parentID**  
 Este atributo é usado para especificar relações pai/filho entre os elementos em DiffGram. Esse atributo só exibido no \<antes > bloco. Ele é usado pelo SQLXML durante a aplicação das atualizações. A relação pai/filho é usada para determinar a ordem na qual os elementos de DiffGram são processados.  
  
## <a name="understanding-the-diffgram-processing-logic"></a>Compreendendo a lógica de processamento de DiffGram  
 A lógica de processamento de DiffGram usa regras específicas para determinar se uma operação é de inserção, atualização ou exclusão. Essas regras são descritas na tabela a seguir.  
  
|Operação|Description|  
|---------------|-----------------|  
|Insert|Um DiffGram indica uma operação de inserção quando um elemento aparece na  **\<DataInstance >** bloco, mas não em correspondente  **\<antes >** bloco e o **diffgr: HasChanges** atributo é especificado (**diffgr: HasChanges = inserido**) no elemento. Nesse caso, DiffGram insere a instância do registro que é especificada na  **\<DataInstance >** bloco no banco de dados.<br /><br /> Se o **diffgr: HasChanges** atributo não for especificado, o elemento é ignorado pela lógica de processamento e nenhuma inserção é executada. Para obter exemplos de funcionamento, consulte [exemplos de DiffGram &#40;SQLXML 4.0&#41;](diffgram-examples-sqlxml-4-0.md).|  
|Update|O DiffGram indica uma operação de atualização quando há um elemento na \<antes de > para o qual há um elemento correspondente no bloco do  **\<DataInstance >** bloco (ou seja, os dois elementos têm um **diffgr:ID="customer4** atributo com o mesmo valor) e o **diffgr: HasChanges** atributo é especificado com o valor **modificado** no elemento no  **\<DataInstance >** bloco.<br /><br /> Se o **diffgr: HasChanges** atributo não for especificado no elemento de  **\<DataInstance >** bloco, um erro será retornado pela lógica de processamento. Para obter exemplos de funcionamento, consulte [exemplos de DiffGram &#40;SQLXML 4.0&#41;](diffgram-examples-sqlxml-4-0.md).<br /><br /> Se **diffgr: parentID** é especificado na  **\<antes >** bloquear, a relação de pai-filho dos elementos que são especificados pelo **parentID** são usados em Determinando a ordem na qual os registros são atualizados.|  
|DELETE|Um DiffGram indica uma operação de exclusão quando um elemento aparece na  **\<antes de >** bloco, mas não em correspondente  **\<DataInstance >** bloco. Nesse caso, o DiffGram exclui a instância do registro que é especificada na  **\<antes de >** bloco do banco de dados. Para obter exemplos de funcionamento, consulte [exemplos de DiffGram &#40;SQLXML 4.0&#41;](diffgram-examples-sqlxml-4-0.md).<br /><br /> Se **diffgr: parentID** é especificado na  **\<antes >** bloquear, a relação de pai-filho dos elementos que são especificados pelo **parentID** são usados em Determinando a ordem na qual os registros são excluídos.|  
  
> [!NOTE]  
>  Parâmetros não podem ser passados para DiffGrams.  
  
  
