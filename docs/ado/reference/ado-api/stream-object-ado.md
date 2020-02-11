---
title: Objeto de fluxo (ADO) | Microsoft Docs
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
ms.openlocfilehash: c70a22a3048c769aac343d51e621e4d755d3baeb
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67916726"
---
# <a name="stream-object-ado"></a>Objeto Stream (ADO)
Representa um fluxo de dados ou texto binários.  
  
 Em hierarquias estruturadas em árvore, como um sistema de arquivos ou um sistema de email, um [registro](../../../ado/reference/ado-api/record-object-ado.md) pode ter um fluxo binário padrão de bits associado a ele que contém o conteúdo do arquivo ou do email. Um objeto de **fluxo** pode ser usado para manipular campos ou registros que contêm esses fluxos de dados. Um objeto de **fluxo** pode ser obtido das seguintes maneiras:  
  
-   De uma URL apontando para um objeto (normalmente um arquivo) contendo dados binários ou de texto. Esse objeto pode ser um documento simples, um objeto de **registro** que representa um documento estruturado ou uma pasta.  
  
-   Abrindo o objeto de **fluxo** padrão associado a um objeto de **registro** . Você pode obter o fluxo padrão associado a um objeto de **registro** quando o **registro** é aberto, para eliminar uma viagem de ida e volta apenas para abrir o fluxo.  
  
-   Instanciando um objeto de **fluxo** . Esses objetos de **fluxo** podem ser usados para armazenar dados para fins de seu aplicativo. Ao contrário de um **fluxo** associado a uma URL, ou ao **fluxo** padrão de um **registro**, um **fluxo** instanciado não tem nenhuma associação com uma fonte subjacente por padrão.  
  
 Com os métodos e as propriedades de um objeto de **fluxo** , você pode fazer o seguinte:  
  
-   Abra um objeto de **fluxo** de um **registro** ou URL com o método [Open](../../../ado/reference/ado-api/open-method-ado-stream.md) .  
  
-   Feche um **fluxo** com o método [Close](../../../ado/reference/ado-api/close-method-ado.md) .  
  
-   Bytes de entrada ou texto para um **fluxo** com os métodos [Write](../../../ado/reference/ado-api/write-method.md) e [WriteText](../../../ado/reference/ado-api/writetext-method.md) .  
  
-   Bytes de leitura do **fluxo** com os métodos [Read](../../../ado/reference/ado-api/read-method.md) e [READTEXT](../../../ado/reference/ado-api/readtext-method.md) .  
  
-   Grave todos os dados de **fluxo** ainda no buffer do ADO para o objeto subjacente com o método [flush](../../../ado/reference/ado-api/flush-method-ado.md) .  
  
-   Copie o conteúdo de um **fluxo** para outro **fluxo** com o método [CopyTo](../../../ado/reference/ado-api/copyto-method-ado.md) .  
  
-   Controle como as linhas são lidas do arquivo de origem com o método de [ignorar](../../../ado/reference/ado-api/skipline-method.md)e a propriedade [LineSeparator](../../../ado/reference/ado-api/lineseparator-property-ado.md) .  
  
-   Determine o fim da posição do fluxo com a propriedade [EOS](../../../ado/reference/ado-api/eos-property.md)e o método [SetEOS](../../../ado/reference/ado-api/seteos-method.md) .  
  
-   Salve e restaure dados em arquivos com os métodos [SaveToFile](../../../ado/reference/ado-api/savetofile-method.md)e [loaddefile](../../../ado/reference/ado-api/loadfromfile-method-ado.md) .  
  
-   Especifique o conjunto de caracteres usado para armazenar o **fluxo** com a propriedade [charset](../../../ado/reference/ado-api/charset-property-ado.md) .  
  
-   Pare uma operação de **fluxo** assíncrona com o método [Cancel](../../../ado/reference/ado-api/cancel-method-ado.md) .  
  
-   Determine o número de bytes em um **fluxo** com a propriedade [size](../../../ado/reference/ado-api/size-property-ado-stream.md) .  
  
-   Controle a posição atual dentro de um **fluxo** com a propriedade [Position](../../../ado/reference/ado-api/position-property-ado.md) .  
  
-   Determine o tipo de dados em um **fluxo** com a propriedade [Type](../../../ado/reference/ado-api/type-property-ado-stream.md) .  
  
-   Determine o estado atual do **fluxo** (fechado, aberto ou em execução) com a propriedade [State](../../../ado/reference/ado-api/state-property-ado.md) .  
  
-   Especifique o modo de acesso para o **fluxo** com a propriedade [Mode](../../../ado/reference/ado-api/mode-property-ado.md) .  
  
> [!NOTE]
>  As URLs que usam o esquema http invocarão automaticamente o [provedor do Microsoft OLE DB para publicação na Internet](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md). Para obter mais informações, consulte [URLs absolutas e relativas](../../../ado/guide/data/absolute-and-relative-urls.md).  
  
 O objeto de **fluxo** é seguro para scripts.  
  
 Esta seção contém os seguintes tópicos:  
  
-   [Propriedades, métodos e eventos do objeto Stream](../../../ado/reference/ado-api/stream-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Registros e fluxos](../../../ado/guide/data/records-and-streams.md)
