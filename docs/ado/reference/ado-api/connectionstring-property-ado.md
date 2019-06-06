---
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
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: d31b9ff3a60b746309224b0e0f9669cef229f234
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/05/2019
ms.locfileid: "66695960"
---
# <a name="connectionstring-property-ado"></a>Propriedade ConnectionString (ADO)
Indica as informações usadas para estabelecer uma conexão a uma fonte de dados.  
  
## <a name="settings-and-return-values"></a>As configurações e valores de retorno  
 Define ou retorna um **cadeia de caracteres** valor.  
  
## <a name="remarks"></a>Comentários  
 Use o **ConnectionString** propriedade para especificar uma fonte de dados, passando uma cadeia de caracteres de conexão detalhada que contém uma série de *argumento* *= valor* instruções separadas por ponto e vírgula.  
  
 ADO dá suporte a cinco argumentos para o **ConnectionString** propriedade; qualquer outra passagem de argumentos diretamente para o provedor sem qualquer processamento pelo ADO. O oferece suporte ao ADO de argumentos são da seguinte maneira.  
  
|Argumento|Descrição|  
|--------------|-----------------|  
|*Provider=*|Especifica o nome de um provedor a ser usado para a conexão.|  
|*Nome do arquivo =*|Especifica o nome de um arquivo específico do provedor (por exemplo, um objeto de fonte de dados persistentes) que contém informações de conexão predefinidos.|  
|*Provedor remoto =*|Especifica o nome de um provedor a ser usado ao abrir uma conexão de cliente. (Apenas serviço de dados remotos.)|  
|*Servidor remoto =*|Especifica o nome do caminho do servidor a ser usado ao abrir uma conexão de cliente. (Apenas serviço de dados remotos.)|  
|*URL=*|Especifica a cadeia de caracteres de conexão como uma URL absoluta que identifica um recurso, como um arquivo ou diretório.|  
  
 Depois de definir a **ConnectionString** propriedade e abra o [Conexão](../../../ado/reference/ado-api/connection-object-ado.md) do objeto, o provedor pode alterar o conteúdo da propriedade, por exemplo, mapeando os nomes de argumentos definidos pelo ADO para seus equivalentes para o provedor específico.  
  
 O **ConnectionString** propriedade herda automaticamente o valor usado para o *ConnectionString* argumento do [abrir](../../../ado/reference/ado-api/open-method-ado-connection.md) método, portanto, você pode substituir o atual  **ConnectionString** propriedade durante o **aberto** chamada de método.  
  
 Porque o *nome do arquivo* argumento faz com que o ADO para carregar o provedor associado, você não pode passar tanto a *provedor* e *nome do arquivo* argumentos.  
  
 O **ConnectionString** propriedade é leitura/gravação quando a conexão é fechada e somente leitura quando ele é aberto.  
  
 Duplicatas de um argumento na **ConnectionString** são ignoradas. A última instância de qualquer argumento é usada.  
  
> [!NOTE]
>  **Uso do serviço de dados remotos** quando usado em um lado do cliente **Conexão** objeto, o **ConnectionString** propriedade pode incluir somente o *provedor remoto* e *servidor remoto* parâmetros.  
  
 A tabela a seguir lista o provedor do ADO padrão para cada sistema de operacional Windows:  
  
|Provedor do ADO padrão|Sistema de operacional do Windows|  
|--------------------------|------------------------------|  
|MSDASQL<br /><br /> (Para melhorar a legibilidade do código-fonte, especificar explicitamente o nome do provedor na cadeia de conexão.)|Windows 2000 (32 bits)<br /><br /> Windows XP (32 bits)<br /><br /> Windows 2003 Server (32 bits)<br /><br /> Windows Vista (32 bits)<br /><br /> Windows Vista Service Pack 1 ou posterior (32 bits e 64 bits)<br /><br /> Versões do Windows após o Windows Vista (32 bits e 64 bits)|  
|Nenhum padrão.<br /><br /> Quando um aplicativo ADO é executado nos seguintes sistemas operacionais e não especifica explicitamente o provedor, o ADO retorna o seguinte erro: "ADODB. Conexão: provedor não for especificado e não há nenhum provedor padrão designado "|Windows 2000 (64 bits)<br /><br /> Windows XP (64 bits)<br /><br /> Windows 2003 Server (64 bits)<br /><br /> Windows Vista (64 bits)|  
  
## <a name="applies-to"></a>Aplica-se a  
 [Objeto Connection (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)  
  
## <a name="see-also"></a>Consulte também  
 [ConnectionString, ConnectionTimeout e exemplo de propriedades de estado (VB)](../../../ado/reference/ado-api/connectionstring-connectiontimeout-and-state-properties-example-vb.md)   
 [ConnectionString, ConnectionTimeout e exemplo de propriedades de estado (VC + +)](../../../ado/reference/ado-api/connectionstring-connectiontimeout-and-state-properties-example-vc.md)   
 [Apêndice a: provedores](../../../ado/guide/appendixes/appendix-a-providers.md)
