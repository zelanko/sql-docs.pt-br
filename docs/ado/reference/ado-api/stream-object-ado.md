---
description: Objeto Stream (ADO)
title: Objeto de fluxo (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 619d9d307e26829ffa74a24c6904fa84889f476f
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88988587"
---
# <a name="stream-object-ado"></a>Objeto Stream (ADO)
Representa um fluxo de dados ou texto binários.  
  
 Em hierarquias estruturadas em árvore, como um sistema de arquivos ou um sistema de email, um [registro](./record-object-ado.md) pode ter um fluxo binário padrão de bits associado a ele que contém o conteúdo do arquivo ou do email. Um objeto de **fluxo** pode ser usado para manipular campos ou registros que contêm esses fluxos de dados. Um objeto de **fluxo** pode ser obtido das seguintes maneiras:  
  
-   De uma URL apontando para um objeto (normalmente um arquivo) contendo dados binários ou de texto. Esse objeto pode ser um documento simples, um objeto de **registro** que representa um documento estruturado ou uma pasta.  
  
-   Abrindo o objeto de **fluxo** padrão associado a um objeto de **registro** . Você pode obter o fluxo padrão associado a um objeto de **registro** quando o **registro** é aberto, para eliminar uma viagem de ida e volta apenas para abrir o fluxo.  
  
-   Instanciando um objeto de **fluxo** . Esses objetos de **fluxo** podem ser usados para armazenar dados para fins de seu aplicativo. Ao contrário de um **fluxo** associado a uma URL, ou ao **fluxo** padrão de um **registro**, um **fluxo** instanciado não tem nenhuma associação com uma fonte subjacente por padrão.  
  
 Com os métodos e as propriedades de um objeto de **fluxo** , você pode fazer o seguinte:  
  
-   Abra um objeto de **fluxo** de um **registro** ou URL com o método [Open](./open-method-ado-stream.md) .  
  
-   Feche um **fluxo** com o método [Close](./close-method-ado.md) .  
  
-   Bytes de entrada ou texto para um **fluxo** com os métodos [Write](./write-method.md) e [WriteText](./writetext-method.md) .  
  
-   Bytes de leitura do **fluxo** com os métodos [Read](./read-method.md) e [READTEXT](./readtext-method.md) .  
  
-   Grave todos os dados de **fluxo** ainda no buffer do ADO para o objeto subjacente com o método [flush](./flush-method-ado.md) .  
  
-   Copie o conteúdo de um **fluxo** para outro **fluxo** com o método [CopyTo](./copyto-method-ado.md) .  
  
-   Controle como as linhas são lidas do arquivo de origem com o método de [ignorar](./skipline-method.md)e a propriedade [LineSeparator](./lineseparator-property-ado.md) .  
  
-   Determine o fim da posição do fluxo com a propriedade [EOS](./eos-property.md)e o método [SetEOS](./seteos-method.md) .  
  
-   Salve e restaure dados em arquivos com os métodos [SaveToFile](./savetofile-method.md)e [loaddefile](./loadfromfile-method-ado.md) .  
  
-   Especifique o conjunto de caracteres usado para armazenar o **fluxo** com a propriedade [charset](./charset-property-ado.md) .  
  
-   Pare uma operação de **fluxo** assíncrona com o método [Cancel](./cancel-method-ado.md) .  
  
-   Determine o número de bytes em um **fluxo** com a propriedade [size](./size-property-ado-stream.md) .  
  
-   Controle a posição atual dentro de um **fluxo** com a propriedade [Position](./position-property-ado.md) .  
  
-   Determine o tipo de dados em um **fluxo** com a propriedade [Type](./type-property-ado-stream.md) .  
  
-   Determine o estado atual do **fluxo** (fechado, aberto ou em execução) com a propriedade [State](./state-property-ado.md) .  
  
-   Especifique o modo de acesso para o **fluxo** com a propriedade [Mode](./mode-property-ado.md) .  
  
> [!NOTE]
>  As URLs que usam o esquema http invocarão automaticamente o [provedor do Microsoft OLE DB para publicação na Internet](../../guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md). Para obter mais informações, consulte [URLs absolutas e relativas](../../guide/data/absolute-and-relative-urls.md).  
  
 O objeto de **fluxo** é seguro para scripts.  
  
 Esta seção contém os seguintes tópicos.  
  
-   [Propriedades, métodos e eventos do objeto Stream](./stream-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Registros e fluxos](../../guide/data/records-and-streams.md)