---
title: Fluxo de objeto (ADO) | Microsoft Docs
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- Stream
helpviewer_keywords:
- Stream object [ADO]
ms.assetid: 0514531f-009d-4519-abc3-d727014a39f1
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: b074a26bdd82bd4356620dbd0b12dc0b7f1c75c7
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="stream-object-ado"></a>Objeto de fluxo (ADO)
Representa um fluxo de dados binários ou de texto.  
  
 Nas hierarquias estruturados em árvore como um sistema de arquivos ou um sistema de email, um [registro](../../../ado/reference/ado-api/record-object-ado.md) pode ter um fluxo de binário padrão de bits associados a ele que contém o conteúdo do arquivo ou email. Um **fluxo** objeto pode ser usado para manipular campos ou registros que contêm esses fluxos de dados. Um **fluxo** objeto pode ser obtido das seguintes maneiras:  
  
-   De uma URL que aponta para um objeto (geralmente um arquivo) que contém dados binários ou de texto. Esse objeto pode ser um documento simple, um **registro** objeto que representa um documento estruturado ou uma pasta.  
  
-   Abrindo o padrão **fluxo** objeto associado a um **registro** objeto. Você pode obter o fluxo padrão associado a um **registro** objeto quando o **registro** é aberto, para eliminar uma viagem apenas para abrir o fluxo.  
  
-   Instanciando um **fluxo** objeto. Essas **fluxo** objetos podem ser usados para armazenar dados para fins de seu aplicativo. Ao contrário de um **fluxo** associados a uma URL ou o padrão **fluxo** de um **registro**, um instanciado **fluxo** não possui uma associação com um fonte subjacente por padrão.  
  
 Com os métodos e propriedades de um **fluxo** do objeto, você pode fazer o seguinte:  
  
-   Abra um **fluxo** de objeto um **registro** ou URL com o [abrir](../../../ado/reference/ado-api/open-method-ado-stream.md) método.  
  
-   Fechar um **fluxo** com o [fechar](../../../ado/reference/ado-api/close-method-ado.md) método.  
  
-   Entrada de bytes ou texto para um **fluxo** com o [gravar](../../../ado/reference/ado-api/write-method.md) e [WriteText](../../../ado/reference/ado-api/writetext-method.md) métodos.  
  
-   Bytes de leitura de **fluxo** com o [leitura](../../../ado/reference/ado-api/read-method.md) e [ReadText](../../../ado/reference/ado-api/readtext-method.md) métodos.  
  
-   Gravar qualquer **fluxo** do buffer de dados ainda no ADO para o objeto subjacente com o [liberar](../../../ado/reference/ado-api/flush-method-ado.md) método.  
  
-   Copie o conteúdo de um **fluxo** para outro **fluxo** com o [CopyTo](../../../ado/reference/ado-api/copyto-method-ado.md) método.  
  
-   Controlar como as linhas são lidas do arquivo de origem com o [SkipLine](../../../ado/reference/ado-api/skipline-method.md)método e o [LineSeparator](../../../ado/reference/ado-api/lineseparator-property-ado.md) propriedade.  
  
-   Determinar a extremidade da posição do fluxo com o [EOS](../../../ado/reference/ado-api/eos-property.md)propriedade e [SetEOS](../../../ado/reference/ado-api/seteos-method.md) método.  
  
-   Salvar e restaurar dados em arquivos com o [SaveToFile](../../../ado/reference/ado-api/savetofile-method.md)e [LoadFromFile](../../../ado/reference/ado-api/loadfromfile-method-ado.md) métodos.  
  
-   Especifique o conjunto de caracteres usado para armazenar o **fluxo** com o [Charset](../../../ado/reference/ado-api/charset-property-ado.md) propriedade.  
  
-   Interromper assíncrona **fluxo** operação com o [Cancelar](../../../ado/reference/ado-api/cancel-method-ado.md) método.  
  
-   Determinar o número de bytes em uma **fluxo** com o [tamanho](../../../ado/reference/ado-api/size-property-ado-stream.md) propriedade.  
  
-   Controlar a posição atual dentro de um **fluxo** com o [posição](../../../ado/reference/ado-api/position-property-ado.md) propriedade.  
  
-   Determinar o tipo de dados em um **fluxo** com o [tipo](../../../ado/reference/ado-api/type-property-ado-stream.md) propriedade.  
  
-   Determinar o estado atual do **fluxo** (fechado, abrir, ou executar) com o [estado](../../../ado/reference/ado-api/state-property-ado.md) propriedade.  
  
-   Especificar o modo de acesso para o **fluxo** com o [modo](../../../ado/reference/ado-api/mode-property-ado.md) propriedade.  
  
> [!NOTE]
>  URLs usando o esquema http invocará automaticamente o [Microsoft OLE DB Provider para Internet Publishing](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md). Para obter mais informações, consulte [Absolute e URLs relativas](../../../ado/guide/data/absolute-and-relative-urls.md).  
  
 O **fluxo** objeto é seguro para script.  
  
 Esta seção contém os tópicos a seguir.  
  
-   [Eventos, métodos e propriedades do objeto de fluxo](../../../ado/reference/ado-api/stream-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Consulte também  
 [Registros e fluxos](../../../ado/guide/data/records-and-streams.md)
