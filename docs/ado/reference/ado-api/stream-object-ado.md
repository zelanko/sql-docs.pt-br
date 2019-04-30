---
title: Stream (ADO) do objeto | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Stream
helpviewer_keywords:
- Stream object [ADO]
ms.assetid: 0514531f-009d-4519-abc3-d727014a39f1
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 976e822482efc530e3b055f61c242ee03a30e012
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63179836"
---
# <a name="stream-object-ado"></a>Objeto Stream (ADO)
Representa um fluxo de dados binários ou texto.  
  
 Em hierarquias de árvore estruturada como um sistema de arquivos ou um sistema de email, uma [registro](../../../ado/reference/ado-api/record-object-ado.md) pode ter um fluxo de binário padrão de bits associado a ele que contém o conteúdo do arquivo ou email. Um **Stream** objeto pode ser usado para manipular registros que contêm esses fluxos de dados ou campos. Um **Stream** objeto pode ser obtido das seguintes maneiras:  
  
-   De uma URL que aponta para um objeto (geralmente um arquivo) que contém dados binários ou de texto. Esse objeto pode ser um documento simples, uma **registro** objeto que representa um documento estruturado ou uma pasta.  
  
-   Abrindo o padrão **Stream** objeto associado a um **registro** objeto. Você pode obter o fluxo padrão associado a um **registro** objeto quando o **registro** for aberta, para eliminar a ida e vinda apenas para abrir o fluxo.  
  
-   Instanciando um **Stream** objeto. Eles **Stream** objetos podem ser usados para armazenar dados para fins de seu aplicativo. Ao contrário de um **Stream** associado com uma URL ou o padrão **Stream** de um **registro**, um instanciado **Stream** não tem associação com um fonte subjacente por padrão.  
  
 Com os métodos e propriedades de um **Stream** do objeto, você pode fazer o seguinte:  
  
-   Abra uma **Stream** do objeto de um **registro** ou uma URL com o [aberto](../../../ado/reference/ado-api/open-method-ado-stream.md) método.  
  
-   Fechar uma **Stream** com o [fechar](../../../ado/reference/ado-api/close-method-ado.md) método.  
  
-   Entrada de bytes ou texto para um **Stream** com o [escrever](../../../ado/reference/ado-api/write-method.md) e [WriteText](../../../ado/reference/ado-api/writetext-method.md) métodos.  
  
-   Bytes de leitura a **Stream** com o [leitura](../../../ado/reference/ado-api/read-method.md) e [ReadText](../../../ado/reference/ado-api/readtext-method.md) métodos.  
  
-   Grave qualquer **Stream** dados ainda em ADO do buffer para o objeto subjacente com o [liberar](../../../ado/reference/ado-api/flush-method-ado.md) método.  
  
-   Copie o conteúdo de um **Stream** para outra **Stream** com o [CopyTo](../../../ado/reference/ado-api/copyto-method-ado.md) método.  
  
-   Controlar como as linhas são lidas do arquivo de origem com o [SkipLine](../../../ado/reference/ado-api/skipline-method.md)método e o [LineSeparator](../../../ado/reference/ado-api/lineseparator-property-ado.md) propriedade.  
  
-   Determinar o final da posição do fluxo com o [EOS](../../../ado/reference/ado-api/eos-property.md)propriedade e [SetEOS](../../../ado/reference/ado-api/seteos-method.md) método.  
  
-   Salvar e restaurar dados em arquivos com o [SaveToFile](../../../ado/reference/ado-api/savetofile-method.md)e [LoadFromFile](../../../ado/reference/ado-api/loadfromfile-method-ado.md) métodos.  
  
-   Especifique o conjunto de caracteres usado para armazenar o **Stream** com o [Charset](../../../ado/reference/ado-api/charset-property-ado.md) propriedade.  
  
-   Interromper assíncrona **Stream** operação com o [Cancelar](../../../ado/reference/ado-api/cancel-method-ado.md) método.  
  
-   Determinar o número de bytes em uma **Stream** com o [tamanho](../../../ado/reference/ado-api/size-property-ado-stream.md) propriedade.  
  
-   Controlar a posição atual dentro de um **Stream** com o [posição](../../../ado/reference/ado-api/position-property-ado.md) propriedade.  
  
-   Determinar o tipo de dados em um **Stream** com o [tipo](../../../ado/reference/ado-api/type-property-ado-stream.md) propriedade.  
  
-   Determinar o estado atual do **Stream** (fechado, abrir ou executar) com o [estado](../../../ado/reference/ado-api/state-property-ado.md) propriedade.  
  
-   Especifique o modo de acesso para o **Stream** com o [modo](../../../ado/reference/ado-api/mode-property-ado.md) propriedade.  
  
> [!NOTE]
>  URLs usando o esquema http invocará automaticamente o [Microsoft OLE DB Provider para publicação na Internet](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md). Para obter mais informações, consulte [absoluta e relativa URLs](../../../ado/guide/data/absolute-and-relative-urls.md).  
  
 O **Stream** objeto é seguro para script.  
  
 Esta seção contém os tópicos a seguir.  
  
-   [Eventos, métodos e propriedades do objeto Stream](../../../ado/reference/ado-api/stream-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Consulte também  
 [Registros e fluxos](../../../ado/guide/data/records-and-streams.md)
