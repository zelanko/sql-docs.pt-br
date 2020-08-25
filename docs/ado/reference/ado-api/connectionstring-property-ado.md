---
description: Propriedade ConnectionString (ADO)
title: Propriedade ConnectionString (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Connection15::ConnectionString
helpviewer_keywords:
- ConnectionString property [ADO]
ms.assetid: 3be75b75-4d36-4479-ab64-9a456869252a
author: rothja
ms.author: jroth
ms.openlocfilehash: f7adb671b42d17b4abe13733fd912234e79560e3
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88775895"
---
# <a name="connectionstring-property-ado"></a>Propriedade ConnectionString (ADO)
Indica as informações usadas para estabelecer uma conexão com uma fonte de dados.  
  
## <a name="settings-and-return-values"></a>Configurações e valores de retorno  
 Define ou retorna um valor de **cadeia de caracteres** .  
  
## <a name="remarks"></a>Comentários  
 Use a propriedade **ConnectionString** para especificar uma fonte de dados passando uma cadeia de conexão detalhada que contém uma série de instruções *Argument* *= Value* separadas por ponto e vírgula.  
  
 O ADO dá suporte a cinco argumentos para a propriedade **ConnectionString** ; quaisquer outros argumentos são passados diretamente para o provedor sem nenhum processamento pelo ADO. Os argumentos que o ADO suporta são os seguintes.  
  
|Argumento|Descrição|  
|--------------|-----------------|  
|*Provedor =*|Especifica o nome de um provedor a ser usado para a conexão.|  
|*Nome do arquivo =*|Especifica o nome de um arquivo específico do provedor (por exemplo, um objeto de fonte de dados persistente) que contém informações de conexão predefinidas.|  
|*Provedor remoto =*|Especifica o nome de um provedor a ser usado ao abrir uma conexão do lado do cliente. (Somente serviço de dados remotos.)|  
|*Servidor remoto =*|Especifica o nome do caminho do servidor a ser usado ao abrir uma conexão do lado do cliente. (Somente serviço de dados remotos.)|  
|*URL =*|Especifica a cadeia de conexão como uma URL absoluta que identifica um recurso, como um arquivo ou diretório.|  
  
 Depois de definir a propriedade **ConnectionString** e abrir o objeto [Connection](./connection-object-ado.md) , o provedor pode alterar o conteúdo da propriedade, por exemplo, mapeando os nomes de argumento definidos pelo ADO para seus equivalentes para o provedor específico.  
  
 A propriedade **ConnectionString** automaticamente herda o valor usado para o argumento *ConnectionString* do método [Open](./open-method-ado-connection.md) , de modo que você pode substituir a propriedade **ConnectionString** atual durante a chamada do método **Open** .  
  
 Como o argumento de *nome de arquivo* faz com que o ADO carregue o provedor associado, você não pode passar os argumentos do *provedor* e do *nome do arquivo* .  
  
 A propriedade **ConnectionString** é de leitura/gravação quando a conexão é fechada e somente leitura quando é aberta.  
  
 Duplicatas de um argumento na propriedade **ConnectionString** são ignoradas. A última instância de qualquer argumento é usada.  
  
> [!NOTE]
>  **Uso do serviço de dados remoto** Quando usado em um objeto de **conexão** do lado do cliente, a propriedade **ConnectionString** pode incluir somente os parâmetros do *provedor remoto* e do *servidor remoto* .  
  
 A tabela a seguir lista o provedor ADO padrão para cada sistema operacional Windows:  
  
|Provedor ADO padrão|Sistema operacional Windows|  
|--------------------------|------------------------------|  
|MSDASQL<br /><br /> (Para melhorar a legibilidade do código-fonte, especifique explicitamente o nome do provedor na cadeia de conexão.)|Windows 2000 (32 bits)<br /><br /> Windows XP (32 bits)<br /><br /> Windows 2003 Server (32 bits)<br /><br /> Windows Vista (32 bits)<br /><br /> Windows Vista Service Pack 1 ou posterior (32 bits e 64 bits)<br /><br /> Versões do Windows após o Windows Vista (32 bits e 64 bits)|  
|Sem padrão.<br /><br /> Quando um aplicativo ADO é executado nos sistemas operacionais a seguir e não especifica explicitamente o provedor, o ADO retorna o seguinte erro: "ADODB. Conexão: o provedor não foi especificado e não há um provedor padrão designado "|Windows 2000 (64 bits)<br /><br /> Windows XP (64 bits)<br /><br /> Windows 2003 Server (64 bits)<br /><br /> Windows Vista (64 bits)|  
  
## <a name="applies-to"></a>Aplica-se A  
 [Objeto Connection (ADO)](./connection-object-ado.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo das propriedades ConnectionString, ConnectionTimeout e State (VB)](./connectionstring-connectiontimeout-and-state-properties-example-vb.md)   
 [Exemplo das propriedades ConnectionString, ConnectionTimeout e State (VC + +)](./connectionstring-connectiontimeout-and-state-properties-example-vc.md)   
 [Apêndice A: Provedores](../../guide/appendixes/appendix-a-providers.md)